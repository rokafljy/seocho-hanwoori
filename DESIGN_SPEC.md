# 서초한우리오케스트라 제4회 정기연주회 홍보 사이트 — 설계 스펙

> Claude Code 작업 지시서 · 단일 HTML 기준 (index.html 동봉)
> 공연: 시네마 & 오페라 : 시간을 초월한 선율 / 2026.7.2(목) 19:30 / 예술의전당 콘서트홀

---

## 1. 디자인 컨셉

포스터의 Deep Navy + Gold를 계승하고, 두 레퍼런스(SM 오디션 · 이트리움 갤러리)의 강점을 흡수.

| 출처 | 차용 요소 |
|------|-----------|
| 포스터 | Deep Navy 배경 · Gold 그라데이션 · 별빛 |
| SM 오디션 | 풀스크린 Hero · 거대 타이포 · 수상 뱃지 고정 · 미니멀 |
| 이트리움 | 영문 시적 슬로건 · 섹션별 영문 동사 라벨 · 여백의 호흡 |

핵심 원칙: **여백으로 고급감, 정보는 인터랙션으로 단계 노출, 색은 2계열(Navy·Gold)만.**

---

## 2. 디자인 토큰

```css
--navy-900:#070d24;  --navy-800:#0a1230;  --navy-700:#0f1a44;  --navy-600:#16225a;
--gold:#cbb073;  --gold-bright:#e9c873;  --gold-light:#f4e8c4;  --gold-pale:#fff6db;
--text-1:#eef1f9;  --text-2:#aab6d6;  --text-3:#8fa0c8;
--line:rgba(203,176,115,0.28);  --line-soft:rgba(255,255,255,0.08);
```

폰트 (Google Fonts):
- 영문 디스플레이 · 숫자 → `Cormorant Garamond` (italic 적극 활용)
- 한글 제목 → `Noto Serif KR`
- 한글 본문 · UI → `Noto Sans KR` (기본 weight 300)

---

## 3. 페이지 구조 (원페이지 스크롤, 8블록)

```
NAV (sticky, 스크롤 시 blur 배경)
①  HERO        풀스크린 · 별빛캔버스 · 영문슬로건3행 · 수상뱃지 · 카운트다운 · CTA
②  INTRO       Listen.   2단 그리드 · 시적리드 + 스탯3 + 본문
③  PROGRAM     Experience.  1부/2부 탭 · 곡 클릭 시 해설 아코디언
④  ARTISTS     Meet.   4인 카드(지휘·소프라노·테너·사회) hover lift
⑤  HISTORY     Remember.  스탯4 + 타임라인(수상 강조)
⑥  INFO        Connect.  관람안내 + 후원안내 2단
⑦  FOOTER      Be the Harmony. · 주최/후원 · 섭외문의
+ 상단 스크롤 프로그레스 바
```

섹션별 영문 동사 라벨은 이트리움 운율 차용 — Listen / Experience / Meet / Remember / Connect.

---

## 4. 인터랙션 명세

| 요소 | 동작 | 구현 |
|------|------|------|
| 별빛 배경 | 마우스 따라 깊이감 패럴랙스 | Canvas, depth별 offset |
| 타이틀 | 황금빛 흐름 | `@keyframes shimmer` background-position |
| 슬로건 3행 | 0.2/0.5/0.8s 순차 등장 | `fadeUp` animation-delay |
| 카운트다운 | 공연일까지 실시간 | `setInterval` 1초 |
| 프로그램 탭 | 1부↔2부 전환 | JS 데이터 렌더 |
| 곡 항목 | 클릭 시 해설 슬라이드다운 | `max-height` transition |
| 아티스트 카드 | hover 시 -6px lift | transform |
| 섹션 진입 | 페이드+슬라이드 등장 | IntersectionObserver `.reveal` |
| 네비 | 스크롤 60px↓ blur 배경 | scroll 이벤트 |
| 모바일 | 햄버거 → 풀스크린 메뉴 | toggle class |

접근성: `prefers-reduced-motion` 시 모든 애니메이션 차단, reveal 즉시 표시.

---

## 5. 콘텐츠 데이터

### 프로그램 (PROGRAM 객체)
- 1부 4곡: Centuria Overture / Les Misérables / The Sound of Music / Pirates of the Caribbean
- 2부 5곡: Intermezzo / Mein Herr Marquis(김효주) / Nessun Dorma(이충만) / Libiamo(김효주·이충만) / Carmen Fantasy
- 각 곡: 번호 · 곡명 · 작곡가 · 연주자 · 해설(프로그램 노트 요약)

### 아티스트 4인
- 지휘 전소영 (음악감독·펜실베니아 주립대 박사)
- 소프라노 김효주 (국립오페라단·밀라노 베르디)
- 테너 이충만 (국립오페라단·파르마 국립음악원)
- 사회 황수경 (전 KBS 아나운서)

### 타임라인 (수상/주요공연 7건, 2026 표창 강조)

### 후원
- 우리은행 1005-801-632724 / 서초구립한우리정보문화센터
- 예매·섭외 070-7209-2932 / 2931

---

## 6. Claude Code 작업 가이드

### 즉시 배포 (현재 상태)
index.html 단일 파일 → Netlify drag&drop 즉시 배포 가능. 외부 의존성은 Google Fonts + Tabler Icons(CDN)뿐.

### 이미지 교체 (권장 후속 작업)
현재 아티스트는 이니셜 원형 플레이스홀더. 실제 사진 확보 시:
1. `/images/artists/` 폴더 생성 (jeon.jpg, kim.jpg, lee.jpg, hwang.jpg)
2. `.artist-portrait` 의 텍스트를 `<img>`로 교체, `object-fit:cover` 적용
3. Hero 배경에 연주 영상 넣을 경우: `#star-canvas` 위에 `<video autoplay muted loop playsinline>` 레이어 추가, 별빛은 보조 레이어로 유지

### React + Vite 전환 시 (확장 고려)
- 섹션별 컴포넌트 분리: `Hero / Intro / Program / Artists / History / Info / Footer`
- PROGRAM·TL 데이터 → `data/` 분리
- 별빛 Canvas → `useEffect` + cleanup
- 카운트다운 → 커스텀 훅 `useCountdown(target)`
- 단, 홍보용 단일 페이지는 현재 HTML로 충분 — 예매 연동 등 확장 필요 시에만 전환 권장

### 수정 시 주의
- 색은 반드시 CSS 변수 사용 (하드코딩 금지)
- 새 섹션 추가 시 `.block` 클래스 + `.reveal` 패턴 유지
- 공연 일시 변경 시: countdown target, hero-meta, info-card 3곳 동시 수정

---

## 7. 체크리스트

- [x] 반응형 (모바일 880px / 560px 브레이크포인트)
- [x] 키보드 포커스 · reduced-motion 대응
- [x] SEO 메타 · OG 태그
- [x] 전화 예매 링크 (tel:)
- [ ] 실제 아티스트/연주 사진 (이미지 확보 후)
- [ ] 예매 링크 (별도 예매처 확정 시)
- [ ] 카카오맵 임베드 (오시는 길 강화 시)
