# MarketView - 투자 블로그 설정 가이드

투자 시장 뉴스와 이슈를 다루는 독립 블로그를 GitHub Pages + Hugo로 구축했습니다.

## 📋 프로젝트 구조

```
investment-blog/
├── content/
│   ├── posts/          # 한국어 포스팅
│   └── posts-en/       # 영어 포스팅
├── layouts/
│   ├── _default/
│   │   ├── baseof.html    # AdSense 스크립트 포함
│   │   └── single.html    # 포스트 레이아웃 (광고 삽입)
│   └── partials/
│       ├── adsense-head.html    # <head> 광고 스크립트
│       └── adsense-ad-unit.html # 포스트 내 광고 단위
├── static/             # 로고, favicon 등 정적 파일
├── themes/
│   └── PaperMod/       # Hugo 테마
├── hugo.toml           # 사이트 설정 (AdSense, 다국어)
└── .github/
    └── workflows/
        └── hugo.yml    # GitHub Actions 배포 파이프라인
```

---

## ⚙️ 초기 설정

### 1. Google AdSense 설정

**AdSense Publisher ID를 hugo.toml에 입력하세요:**

```toml
[params.adsense]
  publisher_id = "ca-pub-XXXXXXXXXXXXXXXX"  # 여기에 입력
```

Publisher ID는 AdSense 계정 → 설정 → 계정 정보에서 확인 가능합니다.

**AdSense 심사 통과:**
- 새 사이트라면 최소 3-5개의 포스팅이 필요합니다.
- Google Search Console 등록 및 사이트맵 제출 권장

### 2. 커스텀 도메인 설정

**선택 1: GitHub Pages 기본 도메인 (무료)**
```
https://yourusername.github.io/investment-blog/
```

**선택 2: 커스텀 도메인 구입**
- GoDaddy, Namecheap, 등록.kr 등에서 도메인 구입 (연 ₩10,000~15,000)
- GitHub Pages에서 커스텀 도메인 설정

**hugo.toml에서 baseURL 수정:**
```toml
baseURL = 'https://yourdomain.com/'  # 또는 'https://yourusername.github.io/investment-blog/'
```

### 3. GitHub 저장소 생성

1. GitHub에서 새 저장소 `investment-blog` 생성
2. 로컬 폴더를 GitHub에 푸시:

```bash
cd investment-blog
git remote add origin https://github.com/yourusername/investment-blog.git
git branch -M main
git push -u origin main
```

### 4. GitHub Pages 배포 활성화

1. GitHub 저장소 → Settings → Pages
2. Build and deployment
   - **Source**: GitHub Actions (선택)
   - **Branch**: main 자동 선택

→ 자동으로 `.github/workflows/hugo.yml` 실행되어 배포됩니다.

---

## 📝 포스팅 작성

### 한국어 포스팅 추가

```bash
hugo new posts/my-post.md
```

`content/posts/my-post.md` 파일을 편집:

```markdown
---
title: "2026년 4월 13일 미국증시 오늘의 시황"
date: 2026-04-13T08:30:00Z
draft: false
author: "MarketView"
description: "간단한 설명"
categories:
  - "US Market"   # 또는 "KR Market"
tags:
  - "미국주식"
  - "나스닥"
---

## 포스팅 제목

포스팅 내용을 마크다운으로 작성하세요.

### 소제목

더 자세한 내용...
```

### 영어 포스팅 추가

```bash
hugo new posts-en/my-post.md
```

### 포스팅 상태 관리

- `draft: false` — 공개
- `draft: true` — 비공개 (로컬 테스트 시 `hugo -D` 사용)

---

## 🧪 로컬 테스트

### 1. Hugo 서버 실행

```bash
hugo server -D
```

- 자동 핫리로드 지원
- http://localhost:1313 접속

### 2. 빌드 확인

```bash
hugo -D
```

- `public/` 디렉토리에 정적 파일 생성
- AdSense 코드 확인

---

## 📊 검색 최적화 (SEO)

### Google Search Console 등록

1. [Google Search Console](https://search.google.com/search-console) 접속
2. URL 접두사에 도메인 입력
3. DNS/HTML 파일/메타태그로 소유권 확인

### 사이트맵 제출

- 자동 생성: `sitemap.xml`
- Search Console → Sitemaps → 제출

### 로봇 규칙

- `robots.txt` 자동 생성 (크롤링 허용)

---

## 💰 광고 수익화 전략

### AdSense 수익 최적화

1. **광고 배치**:
   - 포스트 상단 1개
   - 포스트 하단 1개
   - (필요시) 사이드바 추가

2. **최소 요구사항**:
   - 월 1,000 PV (Page View) 이상
   - 월 $100 이상 수익 시 지급 (다음 달)

3. **수익 증대 팁**:
   - **콘텐츠 품질**: 롱폼 포스팅 (2,000+ 단어)
   - **SEO 최적화**: 키워드 타겟팅
   - **정기 포스팅**: 주 3-5회 업데이트
   - **내부 링크**: 관련 포스팅 연결

### 월별 목표

| 기간 | 목표 | 전략 |
|------|------|------|
| 1-2개월 | 포스팅 10개 | 정기적 콘텐츠 축적 |
| 3개월 | PV 500-1,000 | SEO + SNS 공유 |
| 4-6개월 | PV 1,000+ | AdSense 수익 $50+ |
| 6개월+ | 지속적 성장 | 뉴스레터, SNS 연동 |

---

## 🎨 커스터마이징

### 로고 추가

1. 로고 이미지 준비 (PNG, 500x500px 추천)
2. `static/logo.png`에 저장
3. `hugo.toml` 수정:
```toml
[params.profileMode]
  imageUrl = "/logo.png"
```

### Favicon 추가

1. `static/favicon.ico` 저장

### 색상 테마

`hugo.toml` 수정:
```toml
[params]
  defaultTheme = "dark"  # "light", "dark", "auto"
```

---

## 🚀 배포 및 모니터링

### GitHub Actions 자동 배포

1. 파일 변경 후 `git push main`
2. GitHub Actions 자동 실행
3. 약 1-2분 후 사이트 갱신

### 배포 확인

- GitHub 저장소 → Actions 탭에서 빌드 상태 확인

### 트래픽 모니터링

**Google Analytics 추가** (선택사항):
```toml
# hugo.toml
googleAnalytics = 'G-XXXXXXXXXXXX'
```

---

## 🆘 자주 묻는 질문 (FAQ)

### Q1: AdSense가 승인되지 않았습니다.
- 최소 5-10개의 원본 포스팅 필요
- Google Search Console에 등록 및 사이트맵 제출
- 1-2주 소요

### Q2: 포스팅이 검색에 안 나옵니다.
- Search Console에 URL 수동 제출
- 사이트맵 재제출
- 검색 결과 반영까지 1-4주 소요

### Q3: 한/영 다중 언어를 더 추가하고 싶습니다.
`hugo.toml` 수정:
```toml
[languages.ja]
  languageName = '日本語'
  weight = 3
  contentDir = 'content/posts-ja'
```

### Q4: 포스팅 댓글 기능을 추가하고 싶습니다.
Disqus 또는 Giscus 연동:
```toml
[params]
  comments = true
```

---

## 📞 다음 단계

1. **AdSense Publisher ID 입력**
2. **GitHub 저장소 생성 및 배포**
3. **Google Search Console 등록**
4. **첫 포스팅 작성 및 게시**
5. **SNS 채널 연동** (선택사항)

---

## 📖 참고 자료

- [Hugo 공식 문서](https://gohugo.io/documentation/)
- [PaperMod 테마 가이드](https://github.com/adityatelange/hugo-PaperMod)
- [GitHub Pages 배포](https://docs.github.com/en/pages)
- [Google AdSense 정책](https://support.google.com/adsense)

---

*이 가이드는 정기적으로 업데이트됩니다.*
