# 팀 노트 · 빌드 기록 (BRIEF / FINGERPRINT)

scroll-craft + taste-skill 두 스킬을 적용해 `index.html`을 스크롤 구동형 편집물로
다시 만들었습니다. 이 문서는 스킬이 요구하는 BRIEF / 지문(fingerprint) 기록이며,
이번 환경에서 **실행하지 못한 자동 검증**도 함께 밝힙니다.

## tell-someone 한 줄
> "스크롤을 내리면 팀 조직도가 스스로 한 선씩 그려지고, 그 위로 각자의 이름과
> 역할이 차례로 올라오는 팀 소개 페이지."

## 선택한 grammar — Chaptered editorial (챕터형 편집물)
팀 소개 + 업무 매뉴얼은 "읽는 글"에 가깝습니다. 그래서 여덟 grammar 중 편집물
grammar를 골랐고, filmic one-shot 기본형을 의도적으로 피했습니다.
- 여백 folio(장 번호 + 제목)가 스크롤에 따라 갱신됩니다.
- hero는 미디어 없는 **표지(title page)**: 종이 바탕 위 타이포만.
- 닫음은 **판권(colophon)**: 가장 작은 타이포, CTA는 버튼이 아니라 본문 속 링크.
- 이 grammar가 금지하는 scrub·spotlight·magnet·연속 drift를 전부 사용하지 않았습니다
  (영상·실데이터가 없어 애초에 쓸 수 없는 장치들과도 일치).

## feeling curve (장치보다 먼저 설계)
```
00 표지    Stillness    종이 위 큰 제목, folio 등장
01 전제    Recognition  "팀은 누가 무엇을 맡는가에 관한 약속" 명제
02 구조    Curiosity    [PEAK] 조직도가 --sc-p 따라 스스로 그려짐
03 담당자  Acquaintance 여섯 명을 편집물 항목으로, flow+stagger
04 방식    Weight       네 가지 매뉴얼을 방법 카드(번호 매김 절차)로
05 맺음    Intent       판권, 본문 속 조용한 CTA
```
인접한 두 장이 같은 감정을 내지 않도록 배치했습니다.

## PEAK & 시그니처 무브
- **시그니처 무브:** SVG 조직도의 `stroke-dashoffset`을 pin 액트의 `--sc-p`로 구동해
  **선이 스스로 그려지고**, 이어 각 노드(이름·역할)가 순서대로 떠오름.
  엔진은 손대지 않고(`ScrollCraft.mount`만 호출), 페이지 자체 JS로만 구현.
  kit의 기존 장치(스포트라이트 재색·tilt 각도 변경 등)와 구분되는 고유 상호작용.
- PEAK가 페이지에서 가장 큰 scroll room(`data-sc-span="3.4"`)을 가집니다. 앞 장(전제)은
  조용한 산문이라 PEAK 앞의 "침묵"이 확보됩니다.

## 장치 다양성 (≥4 families, 연속 중복 없음)
`reveal(title page 경계) → 커스텀 SVG-draw(pin, --sc-p) → flow+in(담당자) →
flow+in(방식) → flow+in(판권)`. pin은 PEAK 한 번만. 같은 장치가 연달아 오지 않습니다.

## taste 하우스 룰 준수
- 폰트 2종만: **Fraunces(디스플레이, 편집물이라 serif 정당화) + Geist(본문)**. Inter 미사용.
- 색 6역할·단일 accent(ink-blue). cream-and-brass·AI-퍼플 트랩 회피.
- 대비 측정(렌더 기준): 본문 15.1:1, 보조 5.1:1, accent 10.0:1 — 전부 4.5:1 이상 통과.
- 금지 목록 확인: em dash 0, gradient-text 0, emoji 0, glass 0, box-shadow 0,
  스크롤 유도 문구 0, `01/06` 카운터 0, 아이콘+제목 카드 그리드 구조 아님.
- 사진이 없어 인물 plate는 코드(SVG 레터)로 그림. 지어낸 통계가 없어 counter 미사용.

## 지문(fingerprint) — 이 빌드 1행
| 차원 | 값 |
|---|---|
| Grammar | Chaptered editorial |
| Nav | 여백 folio (장 번호 + 제목, 스크롤로 갱신) |
| Hero | 미디어 없는 표지, 종이 위 타이포 |
| Act shape | reveal → pin(draw) → flow×3, PEAK 1개, 약 7~8vh |
| Close | 판권, 본문 속 링크 CTA, 최소 타이포 |
| Signature | 스크롤로 스스로 그려지는 SVG 조직도 |

(레지스트리는 사용자별이며 처음엔 비어 있는 것이 정상 — 첫 빌드라 충돌 없음.)

## 이번 환경에서 실행하지 못한 검증 (정직하게 밝힘)
- **브라우저 자동 검증 미실행:** 이 런타임은 브라우저 자동화가 꺼져 있고 Chrome이
  없어, scroll-craft의 `shoot.mjs`(스크롤 위치별 contact sheet, dead-scroll·cue opacity·
  합성 대비 측정)와 taste의 inspect 패스를 **돌리지 못했습니다.**
- **에셋·영상 생성 미실행:** ffmpeg 정식 빌드와 `KIE_AI_API_KEY`가 없어 scrub 영상·
  생성 이미지를 만들 수 없습니다. 그래서 영상 장치 대신 코드로 그린 시각물과
  타이포 중심의 편집물 grammar를 택했습니다(스킬의 "에셋 없음" 대체 경로).
- **대신 수행한 것:** HTML 태그 균형 검사(통과), 인라인 JS·엔진 구문 검사(통과),
  색 대비 수치 계산(통과), 금지 패턴 정적 스캔(통과), 엔진이 `--sc-p`를 액트에
  publish하는지 소스 확인(통과). 움직임의 체감 검증은 실제 브라우저에서만 가능합니다.
