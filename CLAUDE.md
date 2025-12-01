# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

개인 포트폴리오 웹사이트로, React와 React Bootstrap을 사용하여 구축된 SPA(Single Page Application)입니다.

## 개발 명령어

### 기본 명령어
- `npm start` - 개발 서버 시작 (포트 3000)
- `npm run build` - 프로덕션 빌드 생성
- `npm test` - 테스트 실행

### Docker
- 빌드: `docker build -t portfolio .`
- 실행: `docker run -p 80:80 portfolio`

## 아키텍처

### 라우팅 구조
- HashRouter 기반 라우팅 사용
- 메인 페이지: Home (`/`)
- 소개: About (`/about`)
- 프로젝트: Projects (`/project`)
- 경력: Career (`/career`)
- 이력서: Resume (`/resume`)
- 포트폴리오: Portfolio (`/portfolio`) - URL 파라미터 `?portfolio=true`로 활성화

### 주요 기술적 특징

1. **PortfolioContext**: 전역 상태 관리를 위한 Context API 사용
   - `showPortfolio`: 포트폴리오 메뉴 표시 여부
   - `portfolioParam`: URL 파라미터 유지
   - App.js:55-59에서 정의됨

2. **URL 파라미터 관리**
   - `UrlParamManager` 컴포넌트가 URL 파라미터를 자동으로 유지 (App.js:62-111)
   - `?portfolio=true` 파라미터가 있으면 포트폴리오 메뉴가 네비게이션 바에 표시됨

3. **스타일링**
   - LINE Seed KR 커스텀 폰트 사용
   - 동적 스타일 주입 (App.js:26-52)
   - Bootstrap 컴포넌트에 커스텀 폰트 자동 적용
   - home-bg.svg를 배경으로 사용하는 content-wrapper

4. **컴포넌트 구조**
   - `components/Navbar.js`: 네비게이션 바, Context를 활용한 조건부 메뉴 렌더링
   - `components/Home/`: 홈 페이지 관련 컴포넌트
   - `components/About/`: 소개 페이지 (기술 스택, 툴 스택 포함)
   - `components/Projects/`: 프로젝트 카드 컴포넌트
   - `components/Career/`: 경력 페이지
   - `components/Resume/`: 이력서 페이지
   - `components/Portfolio/`: 포트폴리오 페이지

5. **Assets 구조**
   - `src/Assets/Projects/`: 프로젝트 이미지
   - `src/Assets/LINE_SeedKR_2023.09.06/`: 커스텀 폰트 파일
   - `src/Assets/*.svg`: 다양한 아이콘 및 배경 이미지

## 중요 사항

- 새로운 페이지를 추가할 때는 App.js의 Routes에 경로를 추가하고, Navbar.js에 메뉴 아이템을 추가해야 함
- 포트폴리오 메뉴처럼 조건부 표시가 필요한 경우 PortfolioContext 사용 패턴 참고
- 모든 페이지 컴포넌트는 `page-section` 클래스를 가진 section 태그로 래핑되어야 함
- 배경 투명도 유지를 위해 `style={{ background: 'transparent' }}` 사용
