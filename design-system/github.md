repo: ttlblood/VH-design-system
branch: main

## Last sync

date: 2026-08-07T10:16:38Z
commit: (미확인 — tree 2ddaf49b715a 시점 기준)

### Updated in this project
- 저장소 연결. 현재 원격에는 README / spec / .gitignore 만 존재 (디자인 시스템 파일 없음)
- 이 프로젝트의 `design-system/` 폴더가 업로드 대상

## Screen map

| 프로젝트 화면 | 저장소 파일 |
|---|---|
| 00 · 디자인 시스템 개요 | (미업로드) design-system/00 · 디자인 시스템 개요.dc.html |
| 01 · Color | (미업로드) design-system/01 · Color.dc.html |
| 02 · Typography | (미업로드) design-system/02 · Typography.dc.html |
| 03 · Spacing, Radius, Elevation | (미업로드) design-system/03 · Spacing, Radius, Elevation.dc.html |
| 04 · Button | (미업로드) design-system/04 · Button.dc.html |
| 05 · Forms | (미업로드) design-system/05 · Forms.dc.html |
| 06 · Badge, Tag, Chip | (미업로드) design-system/06 · Badge, Tag, Chip.dc.html |
| 07 · Card | (미업로드) design-system/07 · Card.dc.html |
| 08 · Domain - Word & Quiz | (미업로드) design-system/08 · Domain - Word & Quiz.dc.html |
| 09 · Domain - Quiz | (미업로드) design-system/09 · Domain - Quiz.dc.html |
| 토큰 (단일 소스) | (미업로드) design-system/tokens.css |

## 운영 방식

- **읽기**: 저장소 변경사항을 여기로 가져올 수 있음 (Sync)
- **쓰기**: 저장소로의 커밋/푸시는 사용자가 직접 수행 (아래 절차)

```bash
# design-system.zip 다운로드 → 압축 해제 후
cd VH-design-system
cp -R ~/Downloads/design-system/* .
git add -A
git commit -m "design system update"
git push
```
