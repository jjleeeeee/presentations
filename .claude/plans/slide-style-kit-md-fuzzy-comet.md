# Plan — AI 퍼소나 슬라이드를 design-cds-docs 레포에 호스팅

## Context

`09_presentation_docs/index.html` (17 슬라이드, 단일 파일)을 사내 동료에게 공유할 영구 링크로 제공.
기존 `design-cds-docs` 레포(weversecorp/design-cds-docs, public)를 활용해 GitHub Pages로 정적 호스팅.

레포 구조가 번호 폴더 기반(`00_tokens`, `01_chord-ds`, `97_knowledge-history`, `98_workflow`, `99_ref`)이라 신규 폴더 `03_presentations/` 추가가 자연스러움.

---

## 넣을 파일

`/Users/jj.iee/Desktop/workspace/design-cds-docs/03_presentations/ai-persona/`

| 파일 | 목적 |
|---|---|
| `index.html` | 09_presentation_docs/index.html 복사 |
| `src/thumbnail/yuki.png` | 슬라이드 08 썸네일 (2.1MB) |
| `src/thumbnail/satomi.png` | 슬라이드 09 썸네일 (2.1MB) |
| `src/background/bg-nsona.JPG` | 슬라이드 12 배경 (1.6MB) |


`index.html` 안의 상대경로 `src/thumbnail/...`, `src/background/...` 그대로 유지 → `src/` 폴더 통째로 복사.

선택:
- `03_presentations/README.md` — 폴더 인덱스. 향후 다른 덱 추가 시 확장.

---

## GitHub Pages 활성화

레포 Settings → Pages:
- Source: Deploy from a branch
- Branch: `main` / `/ (root)`
- Save

배포 URL:
- `https://weversecorp.github.io/design-cds-docs/03_presentations/ai-persona/`

---

## 작업 순서

1. `mkdir -p /Users/jj.iee/Desktop/workspace/design-cds-docs/03_presentations/ai-persona`
2. `cp /Users/jj.iee/Desktop/workspace/09_presentation_docs/index.html /Users/jj.iee/Desktop/workspace/design-cds-docs/03_presentations/ai-persona/index.html`
3. `cp -R /Users/jj.iee/Desktop/workspace/09_presentation_docs/src /Users/jj.iee/Desktop/workspace/design-cds-docs/03_presentations/ai-persona/src` — 이미지 자산 복사

이후는 사용자가 직접 처리 (git add/commit/push, Pages 활성화).

---

## 검증

- 로컬: `open /Users/jj.iee/Desktop/workspace/design-cds-docs/03_presentations/ai-persona/index.html` → 17 슬라이드 정상
- Pages 배포 후: URL 접속 → 첫 슬라이드 표시, 화살표 키 작동, 카운터 17까지
- Pretendard 폰트 로드 확인 (CDN 차단 시 fallback `system-ui` 적용됨)

---

## 주의

- public 레포라 슬라이드 내용도 외부 노출. 사내 전용 내용(아틀라시안 위키 링크 포함됨)이 있는지 확인 후 진행.
- 위키 링크는 사내 인증 필요 → 외부인 클릭 시 401, 슬라이드 자체는 표시됨.
- 이미지 3개 (썸네일 2 + 배경 1, 총 ~5.9MB) `src/` 폴더로 함께 push. SVG는 인라인.
- 이미지 파일명 대소문자 주의: `bg-nsona.JPG` (대문자 확장자). macOS 로컬은 case-insensitive지만 GitHub Pages는 case-sensitive — HTML 참조와 실제 파일명 일치 확인됨.

---

## 변경 외 영향

- 신규 폴더만 추가, 기존 토큰/컴포넌트 문서 무영향
- 레포 root에 다른 `index.html`이 없으면 Pages root 접속 시 README.md 자동 표시
