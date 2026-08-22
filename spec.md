<!-- 프로젝트 기능 명세서 (spec.md) -->
# 기능 명세서 (Specification)

## 1. Git 형상 관리 및 GitHub 연동
* **기능 설명**: 로컬 프로젝트 저장소에 Git 형상 관리를 적용하고, GitHub 원격 저장소(`ttlblood/VH-design-system`)를 생성하여 동기화
* **상세 내역**:
  - `git init -b main`: 기본 브랜치 `main`으로 로컬 저장소 초기화
  - `README.md` 및 `.gitignore` 생성
  - `gh repo create`: GitHub에 공개(Public) 저장소 생성 및 초기 커밋 푸시
* **추가 일시**: 2026-08-07

## 2. 로컬 디자인 확인용 서버 실행 가이드 추가
* **기능 설명**: 로컬 환경에서 디자인 시스템 HTML 파일 및 토큰을 브라우저로 바로 확인할 수 있도록 Python 내장 HTTP 서버 실행 가이드 추가
* **상세 내역**:
  - `python3 -m http.server 8899` 실행 명령어 및 `http://localhost:8899` 접속 가이드 추가
  - `README.md` 사용 방법 업데이트
* **추가 일시**: 2026-08-22 11:18
