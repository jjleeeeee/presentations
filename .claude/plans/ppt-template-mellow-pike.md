# PPT Template — Content Slide (POC)

## Context

위버스 팀 범용 발표 자료용 PPT 템플릿이 필요. 빈 `09_presentation_docs/`에 새로 만든다. 첫 단계로 **Content 슬라이드 1장**만 만들어 `chord-design-system` 토큰을 HTML/Reveal.js 환경에서 어떻게 호명하고 적용하는지 워크플로우를 검증한다. 이 한 장이 검증되면 cover/section/comparison 등 나머지 레이아웃을 같은 패턴으로 확장한다.

**왜 한 장만 먼저?**
- token JSON → CSS var 매핑 방식, font family 처리(Pretendard/Circular), light/dark 토글, 16:9 비율 안정성 등 미지수가 많음
- 풀 템플릿 만들고 패턴 잘못 잡으면 전수 수정 비용 큼

**왜 Content 슬라이드?**
- 가장 자주 쓰이는 본문 레이아웃 = 위계(headline + body + list) 검증에 최적
- Chord DS의 핵심 원칙(Content-First, 여백·타이포 위계, primary 액센트 절제) 모두 적용 가능

## Source 자료

- `/Users/jj.iee/Desktop/workspace/chord-design-system/DESIGN.md` — 브랜드/시스템 SoT (frontmatter curated 18 color / 12 typography / 8 radius / 13 spacing / 6 shadow)
- `/Users/jj.iee/Desktop/workspace/chord-design-system/tokens/color.json` — 408 토큰 (필요 시 직접 참조)
- `/Users/jj.iee/Desktop/workspace/chord-design-system/tokens/typography.json` — 71 원자 토큰
- `/Users/jj.iee/Desktop/workspace/chord-design-system/tokens/size.json` — radius/spacing/shadow
- 컴포넌트 인스턴스 미사용 (단일 슬라이드라 raw HTML로 충분)

## 산출 파일

```
09_presentation_docs/
├── index.html                  # Reveal.js scaffold, content 슬라이드 1장
├── css/
│   ├── tokens.css              # curated 토큰 → CSS 변수
│   └── chord-theme.css         # Reveal.js theme override (typography, layout, colors)
└── README.md                   # 실행법 + 토큰 확장 가이드
```

라이브러리: Reveal.js v5.x **CDN** (jsdelivr) — 빌드 도구 없음, 정적 파일만.

## 구현 디테일

### 1. `css/tokens.css` — curated 토큰만 CSS var로

DESIGN.md frontmatter에 등재된 curated subset만 1차 호명. 누락 시 SoT JSON 직접 참조하는 룰은 README에 기재.

```css
:root {
  /* colors — curated 18 (light 모드 기본) */
  --color-roles-primary: #00CBD5;
  --color-text-default: #000000;
  --color-text-gray-600: #666666;
  --color-text-primary: #00B8C1;
  --color-surface-default: #FFFFFF;
  --color-outline-default-50a: rgba(0,0,0,0.04);
  /* ...전체 18개 */

  /* typography — curated 12 */
  --font-family-body: "Pretendard", -apple-system, "Noto Sans KR", sans-serif;
  --font-family-title: "Pretendard", -apple-system, "Noto Sans KR", sans-serif;
  --font-family-circular: "CircularXX TT", var(--font-family-title);

  --type-title-m-800-size: 28px;
  --type-title-m-800-lh: 36px;
  --type-headline-m-800-size: 20px;
  --type-headline-m-800-lh: 26px;
  --type-body-s-400-size: 14px;
  --type-body-s-400-lh: 18px;
  /* ...12개 */

  /* radius — curated 8 */
  --radius-box-75: 6px;
  --radius-box-100: 8px;
  --radius-box-200: 16px;
  /* ...8개 */

  /* spacing — curated 13 */
  --space-padding-box-100: 8px;
  --space-padding-box-200: 16px;
  --space-padding-box-350: 28px;
  --space-margin-screen-125: 10px;   /* display 화면 */
  --space-margin-screen-200: 16px;   /* end 화면 */
  /* ...13개 */

  /* shadow — curated 6 */
  --shadow-lg: 0 6px 28px rgba(0,0,0,0.10);
  /* ... */
}
```

### 2. `css/chord-theme.css` — Reveal.js theme

- `.reveal .slides` 사이즈: **1920×1080 (16:9)** — `Reveal.initialize({ width: 1920, height: 1080 })`로 설정
- 슬라이드 surface: `--color-surface-default` (Light 모드, 흰 무대)
- 페이지 마진: `--space-margin-screen-200` (16px) — 발표는 *end 화면* 분류 (액션 중심: 청자가 읽고 이해)
- 타이포 — DESIGN.md "대표 페어링" 따름:
  - 슬라이드 타이틀 → `headline-m-800` (20px) — 슬라이드는 "섹션 헤더" 위계가 적절. `title-m-800` (28px)은 cover 슬라이드용으로 예약.
  - 본문 → `body-s-400` (14px) … *발표용으로는 작음. 18~24px 스케일로 키울지 README에 메모 + 추후 결정*
- 위계는 사이즈·굵기·여백으로만 표현 (mint·gradient 본문 강조 금지)

### 3. `index.html` — Content 슬라이드 1장

구조:
```
<section> (Reveal.js 슬라이드)
  ├── <h2> 슬라이드 타이틀          ← headline-m-800
  ├── <p> 리드 문장 (선택)            ← body-m-500
  ├── <ul> 본문 리스트 3~4 항목       ← body-s-400
  └── <footer> 발표명 / 페이지 번호    ← caption-m-400, text-gray-600
```

샘플 콘텐츠: "Chord Design System — Content-First 원칙" + 3개 불릿(여백·타이포·primary 절제).

레이아웃 룰:
- 콘텐츠 영역 max-width 제한 (1920에서 좌우 100~120px gutter — `margin-screen` 룰은 모바일 기준이라 데스크톱 슬라이드는 별도 큰 마진 적용. README에 결정 사유 기재)
- footer는 슬라이드 하단 고정 (`shadow`/`border` 없이 spacing만으로 분리)

### 4. `README.md`

- 실행: `python3 -m http.server 8000` 후 `http://localhost:8000`
- 토큰 확장 룰: curated에 없으면 SoT JSON 열어 raw value 추가, 추정 금지 (DESIGN.md `sot-is-json` 룰)
- 위반 패턴 체크리스트 (alpha suffix solid 사용 금지, fixed_color 일반 UI 금지 등 — DESIGN.md `ai-implementation-rules` 요약)

## 의식적으로 *제외*하는 것

- **빌드 스크립트** (JSON → CSS 자동 변환): 한 장 POC엔 과함. 패턴 확정 후 도입.
- **Dark 모드**: light 모드만 1차. dark는 surface 4단계·shadow 대신 surface 톤 등 별도 룰 필요 — 다음 단계.
- **Spectrum Gradient**: 기능 식별자(모먼트·멤버십)에서만 사용. 범용 content 슬라이드와 무관.
- **아이콘**: `chord-design-system/assets/` 빈 상태(.gitkeep만). 한 장 POC에 아이콘 미사용.
- **Reveal.js fragment/transition**: 정적 1장 — motion은 다음 단계.

## Verification

1. `cd /Users/jj.iee/Desktop/workspace/09_presentation_docs && python3 -m http.server 8000` 실행
2. 브라우저에서 `http://localhost:8000` 접속
3. 시각 검증:
   - [ ] 16:9 비율 유지 (브라우저 리사이즈에도 슬라이드 비율 깨지지 않음)
   - [ ] 흰 surface + 검정 텍스트 위계 (mint·gradient 본문 침투 없음)
   - [ ] 타이틀 = 20px / 800 weight, 본문 = 14px(또는 결정된 발표용 스케일) / 400
   - [ ] Pretendard 폰트 로드 확인 (DevTools Network)
   - [ ] footer 회색 톤 = `text-gray-600` (`#666666`)
4. 토큰 호명 검증: DevTools에서 임의 요소 inspect → 모든 색·여백·radius 값이 `var(--...)` 형태인지 확인 (raw hex/px 하드코딩 0개)
5. DESIGN.md `ai-implementation-rules` 6개 룰 위반 0개 확인

## 다음 단계 (이번 작업에 *미포함*)

- Cover / Section divider / Comparison / Quote / Closing 레이아웃 확장
- Dark 모드 토큰 추가 (color.json dark 모드 값)
- 토큰 빌드 스크립트 (전체 408 색·71 타이포 자동 추출)
- Speaker notes, fragment 애니메이션, PDF 익스포트
