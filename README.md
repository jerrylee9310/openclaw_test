# Structure Variant (SV) without LD-structure modeling

요청 주제: **"LD 구조를 직접 모델링하지 않고 structural variant를 테스트한 논문 정리"**

## 폴더 구조

- `reports/`
  - `01_scope_and_framework.md` : 과제 정의/스코프/분류 프레임워크
  - `02_synthesis_report.md` : 분석 보고서(방법론 비교 + 해석 포인트)
- `data/`
  - `paper_catalog.csv` : 논문 카탈로그(초기 버전)
  - `analysis_matrix.csv` : 방법론 매트릭스(연구설계별 비교)
- `notes/`
  - `limitations.md` : 현재 수집 한계 및 검증 TODO
  - `questions_for_next_search_round.md` : 다음 검색 라운드 전 확정 질문
- `reports/`
  - `04_targeted_protocol_t2d_mi_sv_no_ld.md` : T2D/MI 한정 strict no-LD 조사 프로토콜
- `data/`
  - `screening_template_t2d_mi_sv_no_ld.csv` : 1차 스크리닝 입력 템플릿

## 정리 기준(핵심)

LD(연관불평형) 구조를 이용한 태깅/하플로타입 기반 추론 대신, 아래 중 하나를 직접 수행한 연구를 우선 포함:

1. SV 자체를 직접 genotyping/calling 후 단일변이 검정
2. 희귀 SV burden test (gene/region 단위 집계)
3. trio/family 기반 de novo SV 분석
4. case-control 빈도 차이 기반 통계
5. 기능효과(발현/조절영역 교란) 중심 검정

## 주의

- 본 카탈로그는 **초기 정리본(v0.1)**이며, 일부 항목은 DOI/저널/연도 수동 검증이 필요합니다.
- 정확한 메타분석/인용에 쓰기 전, `notes/limitations.md`의 검증 절차를 먼저 수행하세요.
