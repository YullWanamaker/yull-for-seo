# yull-for-seo

서창훈 상무님(비바리퍼블리카 / 토스증권) 추천서 요청 전용 랜딩 페이지.

**목표 URL:** https://for-seo.joy-ull.info

## 구조

```
yull-for-seo/
├── index.html           # 단일 페이지 (Tailwind CDN)
├── docs/
│   ├── yull-resume.pdf  # 경력기술서 (toss 버전 준비되면 교체)
│   └── yull-bullets.pdf # 핵심 요약 불릿포인트 (회장님 전달 대기)
└── README.md
```

## 페이지 구성

1. **헤더** — 화폐 3.0 동맹 메시지 + 추천 요청
2. **30초 핵심** — End-to-end BD · 전통금융 협력 · NEW-EIP 3개 카드
3. **3개 자료 카드:**
   - ① 포트폴리오 (toss.joy-ull.info 임베드 + 방문 링크)
   - ② 경력기술서 (PDF 임베드 + PDF 다운 / Google Docs / 텍스트 복사)
   - ③ 핵심 요약 (PDF 임베드 + PDF 다운 / Google Docs / 텍스트 복사)
4. **CONTACT** — 이메일·전화·X 링크

## 회장님이 채워야 할 곳 (index.html 안)

### 1) Google Docs 링크 — line 367–368
```js
const GDOCS_RESUME = "";   // ← Google Docs URL 넣기
const GDOCS_BULLETS = "";
```

### 2) 복사 텍스트 — line 408–426
```js
const RESUME_TEXT = `[조율 · Yull · 경력기술서 텍스트]
(전체 텍스트 붙여넣기)`;

const BULLETS_TEXT = `[조율 · Yull · 핵심 요약]
• 9년차 크립토 BD
• ... (블렛 목록)`;
```

### 3) 불릿포인트 PDF — `docs/yull-bullets.pdf`
파일 만들어서 위 경로에 저장. 그러면 자동으로 임베드 카드 활성화됨.
- 추후 임베드 placeholder 자리(`#bullets-embed-empty` div)를 `<div class="pdf-embed"><iframe src="./docs/yull-bullets.pdf#toolbar=0&navpanes=0"></iframe></div>` 로 교체

### 4) (선택) 경력기술서 토스 버전
현재는 `yull-resume.pdf` = 카카오용 PDF 그대로 복사. 토스용 PDF 준비되면 같은 이름으로 덮어쓰기.

## Cloudflare Pages 배포

```bash
# 1) GitHub repo 만들고 push
cd D:\클로드\취업준비\포트폴리오\yull-for-seo
git add -A
git commit -m "feat: initial yull-for-seo recommendation page"
git remote add origin https://github.com/YullWanamaker/yull-for-seo.git
git push -u origin main

# 2) Cloudflare Pages 대시보드
#    - Create application → Pages → Connect to Git
#    - yull-for-seo repo 선택
#    - Build settings: Framework preset = None
#    - Build command: (비움)
#    - Build output directory: /  (혹은 비움)
#    - Deploy

# 3) Custom domain
#    - Custom domains → Set up custom domain → for-seo.joy-ull.info
#    - DNS (Cloudflare): CNAME for-seo → yull-for-seo.pages.dev
```

## 디자인 톤

- **컬러**: 토스 블루 #0064FF + 흰색
- **폰트**: Noto Sans KR (Gmarket Sans 없는 환경 대비)
- **메시지**: 화폐 3.0 / 다음 시대 / 동맹 — 서창훈 상무 BCMC 발표 키워드 차용
- **로봇**: noindex, nofollow (검색 노출 차단)
