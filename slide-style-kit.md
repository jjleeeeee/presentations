# Slide Style Kit — Chord DS 기반
> DESIGN.md에서 슬라이드 적용 요소만 추출. 페르소나 PPT 디자인 기준으로 사용.
> **다크 테마 사용 중** (배경 #000, 텍스트 #FFF). Light 원본값은 괄호 표기.

---

## 색상

### 다크 테마 (현재 사용) — SoT color.json 확인값

| 역할 | 토큰 | Hex | 슬라이드 사용처 |
|------|------|-----|----------------|
| 배경 | `surface/default` dark | `#000000` | 슬라이드 기본 배경 |
| 카드 표면 | `surface/default-2` dark | `#161616` | 카드·섹션 박스 (elevation 1단계) |
| 코드블록·비강조 | `surface/default-3` dark | `#1F1F1F` | 코드블록 배경 (elevation 2단계) |
| 강조 영역 | `surface/default-4` dark | `#282828` | 표 헤더 배경 (elevation 3단계) |
| 본문 텍스트 | `text/default` dark | `#FFFFFF` | 헤드라인, 본문 |
| 보조 텍스트 | `text/gray-600` dark | `#999999` | 서브카피, 출처, 캡션 |
| 더 옅은 보조 | `text/gray-500` dark | `#777777` | 비활성 텍스트, 플레이스홀더 |
| 액센트 (민트) | `roles/primary` dark | `#01D5DF` | 강조 단어, 태그, 라벨 |
| 액센트 텍스트 | `text/primary` dark | `#01D5DF` | 강조 텍스트 (roles/primary와 동일) |
| 경고·Don't | `roles/negative` dark | `#FE5B58` | Don't 마커 (Light/Dark 동일) |
| 구분선 | `outline/default-50a` dark | `#FFFFFF0D` | 표 구분선 (5% 흰) |
| 테두리 | `outline/gray-100` dark | `#282828` | 카드 테두리 |

> 모든 값 SoT `color.json` 직접 확인. 추정값 없음.

**규칙:** 민트 슬라이드당 1~3곳 이하. 섹션 구분 = 여백 + 타이포 위계 (fill 금지). Dark elevation = 카드가 배경보다 밝아야 함 (Lighter is Higher).

---

## 타이포그래피

| 슬라이드 요소 | DS 토큰 | size / weight / lh |
|--------------|---------|-------------------|
| 슬라이드 메인 타이틀 | `title-m-800` | 28px / 800 / 36px |
| 섹션 헤더 | `headline-m-800` | 20px / 800 / 26px |
| 서브섹션 | `headline-s-800` | 18px / 800 / 23px |
| 본문 (강조) | `body-m-500` | 15px / 500 / 21px |
| 본문 (기본) | `body-s-400` | 14px / 400 / 18px |
| 표 헤더·라벨 | `body-s-700` | 14px / 700 / 18px |
| 캡션·출처 | `caption-m-400` | 12px / 400 / 16px |

**대표 페어링:**
- 슬라이드 헤드라인 + 본문: `title-m-800` → `body-s-400`
- 표/리스트 행: 헤더 `body-s-700` + 내용 `body-s-400`
- 강조 본문 내 굵게: `body-s-400` → `body-s-700` (색 변경 X, weight만)

### 커버 전용 타이포 (Figma 커버 node:337-6371 기준)

> CircularXX TT 사용 — DESIGN.md "영문 헤더·라벨" 전용 폰트. 한글에도 적용됨(Figma 커버 실사례 확인).

| 요소 | 폰트 | size | weight | lineHeight | letterSpacing |
|------|------|------|--------|------------|---------------|
| 커버 메인 타이틀 | CircularXX TT Bold | 80px | 700 | 1.2 (96px) | -1.6px |
| 커버 서브헤드 | CircularXX TT Bold | 36px | 700 | 1.32 (47.5px) | -0.72px |

**다크 버전 색상:**
- 메인 타이틀: `#FFFFFF`
- 서브헤드: `#999999`
- 배경: `#000000`

---

## 컨테이너·카드

| 용도 | Radius 토큰 | 실제값 | Shadow |
|------|------------|--------|--------|
| 슬라이드 카드·섹션 박스 | `box-200` | 16px | `shadow-lg` |
| 코드블록·인풋 박스 | `box-100` | 8px | 없음 |
| 태그·뱃지·라벨 | `box-50` | 4px | 없음 |
| 카드 안 작은 모듈 | `box-100` | 8px | 없음 |

**포함 위계:** 큰 카드(`box-200`) ⊃ 내부 모듈(`box-100`). 같은 radius 중첩 금지.

---

## 여백·간격

| 용도 | 토큰 | 실제값 |
|------|------|--------|
| 슬라이드 좌우 마진 | `margin-screen-200` | 16px |
| 섹션 간 간격 | `padding-box-350` | 28px |
| 카드 내부 패딩 | `padding-box-200` | 16px |
| 아이콘-텍스트 갭 | `padding-box-100` | 8px |
| 태그 내부 패딩 | `padding-box-75` | 6px |

---

## Do / Don't

**Do**
- 섹션 구분: 여백 + 타이포 위계로 (회색 fill 박스 금지)
- 텍스트 강조: weight 변경으로 (`body-s-400` → `body-s-700`)
- 민트 액센트: 슬라이드당 핵심 포인트 1~3곳만
- 카드 elevation: `shadow-lg` 단일 사용 (여러 단계 혼용 금지)

**Don't**
- 그라데이션 장식 금지 (Spectrum Gradient = 모먼트·멤버십 전용, 슬라이드 배경·장식 불가)
- `-100a` 계열 배경 금지 (`surface-default-100a` 같은 alpha 토큰 = 오버레이 전용)
- 텍스트에 민트·퍼플·그라데이션 강조 금지
- 슬라이드당 Primary 액센트 2개 이상 금지

---

## 빠른 참조 — 자주 쓰는 조합 (다크 테마)

```
헤드라인 슬라이드
  배경: #000000
  타이틀: 28px / 800 / #FFFFFF
  서브: 14px / 400 / #999999
  액센트 단어: #01D5DF

표 슬라이드
  헤더 행: 14px / 700 / #FFFFFF  배경: #282828
  일반 행: 14px / 400 / #FFFFFF  구분선: #FFFFFF0D
  강조 셀: 텍스트 color #01D5DF

카드/박스
  배경: #161616  radius: 16px  border: #282828  shadow: shadow-lg

코드블록/비강조
  배경: #1F1F1F  radius: 8px

태그/라벨
  배경: #01D5DF  텍스트: #000000  radius: 4px  패딩: 6px 12px
  Don't 마커: 배경 #FE5B58  텍스트: #FFFFFF
```
