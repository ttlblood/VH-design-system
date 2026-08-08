# 역적용 가이드 — 디자인 시스템 → 개발 앱

디자인 시스템(토큰)을 수정한 뒤, 실제 보카 헌트릭스 코드(웹/앱/확장)에 반영하는 방법입니다.
목표: **값을 한 곳(`tokens.css`)에서만 바꾸면 전체가 따라오게** 만드는 것.

---

## 0. 현재 "중구난방"의 원인 (진단)

| 증상 | 원인 | 해결 |
|---|---|---|
| 폰트 크기 키우면 화면마다 제각각 | `globals.css`의 `--font-size:11px` ↔ `index.css`의 `html{font-size:16px}` 충돌 | 16px 기준으로 통일 (`tokens.css`) |
| 브랜드색을 한 번에 못 바꿈 | `bg-purple-600`이 20+ 컴포넌트에 하드코딩 | `--primary` 토큰으로 중앙화 |
| 랜딩과 앱 색이 따로 놈 | `.landing-page` 스코프가 파랑 primary로 분리 | 의도된 분리 → 유지 (랜딩 제외 대상) |

---

## 1. 적용 순서 (권장, 점진적)

### STEP 1 — 토큰 파일 넣기 (외형 변화 거의 없음, 안전)
```
1) design-system/ 폴더를 src 와 나란히 둡니다
      VocaPowerAiFigma/
      ├── src/
      └── design-system/tokens.css
2) src/styles/globals.css 최상단에 추가:
      @import "../../design-system/tokens.css";
3) globals.css 의 :root { --font-size:11px; ... } 블록 삭제
   (색/폰트 토큰은 이제 tokens.css가 담당)
4) index.css 의 html{font-size:16px} 는 tokens.css와 동일하므로 그대로 두거나 제거
```
이 시점에서 색은 그대로(같은 HEX), 폰트 기준값만 16px로 정리됩니다.

### STEP 2 — 브랜드색 토큰화 (핵심)
shadcn `--primary`가 이제 보라(#9333EA)이므로, 하드코딩된 보라를 토큰으로 교체:

```
찾기 → 바꾸기 (전 컴포넌트 대상, 의미가 '주요 액션'일 때만)
  bg-purple-600            →  bg-primary
  hover:bg-purple-700      →  hover:bg-primary/90   (또는 그대로 두어도 동일 색)
  text-purple-600          →  text-primary
  border-purple-100        →  border-primary/… (또는 유지)
  bg-purple-50             →  bg-primary/5  또는 유지
```
> 급하지 않으면 STEP 2는 화면 단위로 나눠서 진행하세요. `bg-purple-600`을 안 바꿔도
> 색은 동일하게 나옵니다(같은 값). 다만 나중에 브랜드 변경 시 한 곳에서 안 됩니다.

### STEP 3 — 이후 브랜드/폰트 변경
`tokens.css`의 값만 수정 → 전체 반영.
```css
--primary: var(--purple-600);   /* 예: 다른 브랜드색으로 교체 시 여기 한 줄 */
--font-size-root: 16px;         /* 예: 전체 폰트 키우기 */
```

---

## 2. Tailwind 클래스 ↔ 토큰 매핑표

### 색상
| 지금 쓰는 클래스 | 의미 | 토큰 |
|---|---|---|
| `bg-purple-600` | 주요 버튼/활성 | `--primary` |
| `hover:bg-purple-700` | 주요 hover | `--primary-hover` |
| `bg-purple-50` | 선택칩/활성탭 배경 | `--primary-subtle` |
| `text-purple-600` | 브랜드 텍스트 | `--primary-subtle-foreground` |
| `border-purple-100` | 브랜드 옅은 경계 | `--primary-border` |
| `bg-gray-50` | 앱 캔버스 | `--background` |
| `bg-white` (카드) | 카드 표면 | `--card` |
| `text-gray-900` | 기본 텍스트 | `--foreground` |
| `text-gray-500` / `#717182` | 보조 텍스트 | `--muted-foreground` |
| `bg-[#f3f3f5]` | 입력 배경 | `--input-background` |
| `text-green-600` | 성공/정답 | `--success` |
| `text-blue-600` | 정보 | `--info` |
| `#d4183d` / `text-red-600` | 오류/삭제 | `--danger` |

### 타이포 (rem, 16px 기준)
| 클래스 | px | 용도 | 토큰 |
|---|---|---|---|
| `text-4xl` | 36 | 점수·히어로 | `--text-4xl` |
| `text-2xl` | 24 | 페이지 제목 | `--text-2xl` |
| `text-xl` | 20 | 섹션 제목·표제어 | `--text-xl` |
| `text-lg` | 18 | 소제목 | `--text-lg` |
| `text-base` | 16 | 본문 | `--text-base` |
| `text-sm` | 14 | 보조 | `--text-sm` |
| `text-xs` | 12 | 캡션·배지 | `--text-xs` |
| `font-medium/bold/extrabold/black` | 500/700/800/900 | — | `--font-weight-*` |

### 반경 · 그림자
| 클래스 | 용도 | 토큰 |
|---|---|---|
| `rounded-md` | 컨트롤(버튼·입력) | `--radius-md` (8px) |
| `rounded-xl` | 카드 | `--radius-xl` (14px) |
| `rounded-2xl` | 모달·큰 카드 | `--radius-2xl` (16px) |
| `rounded-full` | 칩·아바타·알약버튼 | `--radius-full` |
| `shadow-md` | 카드 hover | `--shadow-md` |
| `shadow-2xl` | 모달·시트 | `--shadow-2xl` |
| `shadow-purple-100/200` | CTA 컬러드 | `--shadow-brand` |

### 모션
| 클래스 | 토큰/키프레임 |
|---|---|
| `animate-fade-in` | `@keyframes fade-in` (300ms) |
| `animate-slide-up` | `@keyframes slide-up` (400ms, stagger `delay-100/200/300`) |
| `animate-scale-in` | `@keyframes scale-in` (200ms) |
| press | `scale(0.98)` 버튼 / `scale(0.94)` 아이콘 |

---

## 3. (선택) Tailwind v4에서 토큰과 연결하기

`@theme inline`으로 토큰을 Tailwind 색상 유틸에 노출하면 `bg-primary` 등을 그대로 쓸 수 있습니다.
`globals.css`의 기존 `@theme inline` 블록에서 `--color-primary: var(--primary);`가 이미 있으므로,
`tokens.css`가 `--primary`를 보라로 정의하는 순간 `bg-primary`가 보라가 됩니다.

```css
@theme inline {
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  /* 필요 시 status 토큰도 노출 */
  --color-success: var(--success);
  --color-info: var(--info);
}
```

---

## 4. 체크리스트
- [ ] STEP 1 적용 후 앱 스크린샷 비교 → 색 동일한지 확인
- [ ] 폰트 크기 한 번에 조정되는지 `--font-size-root`로 테스트
- [ ] `--primary` 한 줄 바꿔서 전 화면 브랜드색 반영되는지 테스트
- [ ] 랜딩 페이지(`.landing-page`)는 이 변경에서 제외됐는지 확인
- [ ] 확장프로그램(popup.tsx)도 `tokens.css` 불러오는지 확인 (이미 Pretendard 사용 중)
