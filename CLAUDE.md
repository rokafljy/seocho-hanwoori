# 서초한우리오케스트라 제4회 정기연주회 홍보 사이트 — 작업 맥락

> 이 파일은 다른 컴퓨터(노트북 등)에서 작업을 이어갈 때 Claude가 현재 상태를 빠르게 파악하기 위한 핸드오프 문서입니다.

## 무엇을 만들고 있나
- **공연**: 시네마 & 오페라 : 시간을 초월한 선율 / 2026.7.2(목) 19:30 / 예술의전당 콘서트홀 / 국립오페라단 협연
- **형태**: 단일 페이지 홍보 사이트 (`index.html` 하나 + `images/`). 외부 의존성은 Google Fonts, Tabler Icons(CDN)뿐.
- **디자인**: 밝은 아이보리 갤러리 톤 + 네이비·골드 강조. Hero·인용 밴드·관람안내·푸터는 어두운 극장 톤. 제목 세리프(Cormorant/Noto Serif), 본문 산세리프(Noto Sans).

## 현재 라이브 / 배포
- **라이브(GitHub Pages)**: https://rokafljy.github.io/seocho-hanwoori/ — `main`에 push하면 1~2분 뒤 자동 갱신.
- **저장소**: https://github.com/rokafljy/seocho-hanwoori (현재 **public** — 무료 Pages 사용 위해 전환함)
- **Netlify**(`seocho-hanwoori.netlify.app`, siteId `9fe38334-8614-40ea-82c5-f54b98f53b99`): 계정 **사용량 초과로 배포 차단**됨(`Skipped due to account credit usage exceeded`). 한도 리셋/업그레이드 전엔 사용 불가.

## 로컬 미리보기
```
node server.js      # 의존성 없는 정적 서버
```
→ http://localhost:4321 (Claude Code의 Launch preview 패널로도 가능)

## 섹션 구성 (index.html, 위→아래)
NAV → Hero(연주 영상 배경+소리버튼) → 소개(Listen) → 인용 밴드 → 프로그램(Experience, 1·2부 탭+해설 아코디언) → 출연진(Meet, 4인 실제 프로필) → 단원(Together, 18인 명단) → 연혁(Remember, 표창 사진+타임라인) → 관람안내(Connect, 다크) → 오시는 길(Visit, 지도카드+편의시설 픽토그램) → Footer + 플로팅 '관람 신청하기' 버튼.

## 핵심 자산 / 연동
- 사진: 전부 한우리 실제 사진(`images/` — orchestra/brass/stage/gallery/award/concert.jpg, 출연진 jeon·kim·lee·hwang.png, 단원 members1~4.png, poster.png). 원본은 hwo.or.kr 갤러리/홈에서 받아 1800px·~0.4MB로 최적화함.
- Hero 영상: `images/hero.mp4`(16초, 1.88MB). 유튜브 iFKA39C2EJw(경기아트센터 2025.8.31 실황)의 ~240초 와이드 합주 구간을 잘라 워터마크 크롭 후 인코딩. 음소거 자동재생 + "소리 켜기" 토글. reduce-motion이면 "영상 재생" 버튼 노출.
- 관람 신청: 구글폼 https://forms.gle/z7paaiJS4aXJCuAy6 (모든 CTA가 새 탭으로 연결).
- 후원계좌 우리은행 1005-801-632724(서초구립한우리정보문화센터), 문의 070-7209-2932·2931.

## 작업 방식 (사용자 선호)
- **일괄 수정 → 한 번에 반영 → 로컬 미리보기로 확인 → 승인 시 배포(push)**. 한 건씩 즉시 배포하지 않음.
- 그냥 시키는 대로만 하지 말고 **더 나은 방법을 먼저 제안**하고 의견을 주고받으며 진행.
- 코드 변경은 사용자 승인 시 commit + push (push하면 Pages 자동 배포).

## 영상 재편집이 필요할 때 (도구는 데스크톱 _imgtool에만 있음)
- 데스크톱 `C:\Users\NT751\_imgtool\bin`에 yt-dlp.exe, ffmpeg가 설치돼 있음(저장소엔 미포함).
- 다른 구간으로 바꾸려면: `_imgtool/work/src.mp4`(원본 720p)에서 ffmpeg로 다시 트림 → `images/hero.mp4` 교체 → push.

## 남은 일 / 결정 대기
- 공개 배포처: GitHub Pages(현재, public) 유지할지 / Cloudflare Pages(private 유지 가능)로 옮길지 / Netlify 복구할지.
- 영상: 현재 16초 와이드 합주 구간. 다른 장면·길이 원하면 재편집 가능.
- (선택) 영상 자막/음성해설, 단원 인터뷰 한 줄, 축사 인용 매거진 섹션 등은 자료 확보 시 추가.
