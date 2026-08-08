# 보카 헌트릭스 디자인 시스템

웹 · 앱 · 확장프로그램이 공유하는 단일 소스. 개발 중인 앱(`../src`)의 실제 외형
(보라 브랜드 + shadcn/ui 구조)을 미러링하되, 코드 곳곳에 흩어져 있던 값을 토큰으로
중앙화했습니다. 랜딩 페이지(`.landing-page`, 파랑 계열)는 대상에서 제외.

## 위치

```
VocaPowerAiFigma/
├── src/                 ← 앱 코드
└── design-system/       ← 이 폴더 (디자인 시스템)
    ├── tokens.css       ← 앱에 이식하는 단일 소스
    ├── MAPPING.md       ← 역적용 가이드
    └── *.dc.html        ← 컴포넌트 카드 (브라우저로 바로 열림)
```

## 파일 구성

| 파일 | 역할 |
|---|---|
| `tokens.css` | **단일 소스.** 색·타이포·간격·반경·그림자·모션 토큰 + 공통 키프레임 |
| `MAPPING.md` | 역적용 가이드. 진단 → STEP별 이식 순서 → Tailwind 클래스↔토큰 매핑표 |
| `00 · 디자인 시스템 개요` | 허브. 각 카드로 링크 |
| `01 · Color` | 브랜드 · 램프(purple/gray/blue/green/red) · 시맨틱 토큰 |
| `02 · Typography` | Pretendard · 타입 스케일 · 굵기 · 역할별 적용 |
| `03 · Spacing, Radius, Elevation` | 4px 간격 · 반경 · 그림자 · 모션 |
| `04 · Button` | variant · size · state · 실전 CTA 패턴 |
| `05 · Forms` | TextField · Checkbox · Radio · Switch · Slider |
| `06 · Badge, Tag, Chip` | 상태 라벨 · 필터/키워드 칩 · 아바타 · 도트 |
| `07 · Card` | 표면 종류 · 통계/리스트 카드 · Alert · Toast · Modal |
| `08 · Domain - Word & Quiz` | 단어 목록 필터 · 단어 카드(반응형 다중 의미) · SRS 규칙 · 상세 모달 |
| `09 · Domain - Quiz` | 유형 선택 · 문제 풀이 · 정답/오답/시간초과 · 결과 |

## 앱 연결

`src/styles/globals.css` 최상단:

```css
@import "../../design-system/tokens.css";
```

그다음 `globals.css`의 기존 `:root { --font-size: 11px; ... }` 블록을 삭제합니다.
자세한 순서는 `MAPPING.md` STEP 1~3 참조.

## 핵심 결정

- **브랜드색 = purple-600 `#9333EA`** (hover `#7E22CE`). shadcn 기본 `--primary`(거의 검정)를
  보라로 재정의해 `bg-primary`가 곧 브랜드색이 되도록 함.
- **폰트 기준 16px.** 기존 `--font-size:11px`(globals.css) ↔ `html{16px}`(index.css) 충돌 제거.
- **서체 Pretendard**, 자간 -0.025em (한글 가독성).
- **아이콘 lucide-react** (앱과 동일 세트) — 이모지 사용 안 함.
- 카드는 경계선 *또는* 그림자. 라운드: 컨트롤 8 / 카드 14 / 모달 16 / 칩 full.
- 모션: fade-in 300 · slide-up 400 · scale-in 200, press = scale(.98).

## 도메인 규칙 (앱 코드 기준)

- **SRS 도트 3개** = 1·3·7일차 이력. 정답 `green-500` / 오답 `red-500` / 미학습 `gray-300`, 8px.
- **SRS 단계 배지**: 신규 노랑 · 1일차 파랑 · 3일차 초록 · 7일차 보라 · 완료 주황. 10px / weight 500.
- **테스트 버튼**은 의미 30개 초과 시 회색 비활성.

## 수정 → 적용 흐름

1. 카드에서 방향 확인 → `tokens.css` 값 수정
2. 앱은 이미 `@import`로 연결돼 있으므로 저장만 하면 반영
3. 하드코딩된 `bg-purple-600`은 화면 단위로 `bg-primary`로 점진 교체

```css
/* tokens.css — 이 두 줄이 전체를 좌우함 */
--primary: var(--purple-600);
--font-size-root: 16px;
```

## 남은 작업 후보

- 다크 모드 토큰 (코드에 `.dark` 스코프 존재 — 아직 시스템 미반영)
- 네비게이션(탭바/헤더) · 리스트/스켈레톤 · 검색 화면
