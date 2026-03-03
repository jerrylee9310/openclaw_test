# 04. Targeted protocol (T2D + MI, recent 5 years, strict no-LD)

작성일: 2026-03-03

## 목표
- 최종 목적: **논문 초안 작성 전 단계의 근거 문헌 셋 구축**
- 질환 범위: **Type 2 Diabetes (T2D), Myocardial Infarction (MI)**
- 기간: **최근 5년 중심(2021~현재)**
- 변이 범위: **SV 중 DEL/DUP/INS 중심**
- 제외: **CNV-only 분석, SNP-LD proxy 기반 해석, LD/haplotype 의존 모델**

---

## 핵심 원칙: strict no-LD
아래를 모두 만족해야 본문 포함:
1. 분석 단위가 직접 관측된 SV(DEL/DUP/INS)
2. 통계 검정이 SV 자체를 독립 단위로 수행
3. LD block/tag SNP/haplotype 기반 유도 추론을 주 분석에 사용하지 않음

### 허용 가능한 결합 방식
- Fisher's method 등 **p-value 결합**은 허용
- 단, 결합 대상은 **SV 기반 독립 검정 결과**여야 함
- 결합 단계에서 LD 행렬/상관구조를 모델링하면 제외 또는 mixed로 강등

---

## 포함/제외 기준 (운영판)

### Include
- WGS/long-read/short-read 기반 SV calling 후 DEL/DUP/INS association
- case-control 회귀, burden, meta p-value 결합(Fisher 등)
- 질환/표현형이 T2D 또는 MI(또는 CAD-AMI 하위 정의에서 MI 명시)

### Exclude
- CNV만 다루는 연구
- SNP GWAS + LD proxy로만 SV를 암시하는 연구
- 리뷰/사설/방법론 소개만 있고 실제 질환 연관검정 부재
- 2020년 이전(단, 방법론적 landmark는 부록 후보)

### Borderline (보류)
- 주분석은 SV direct이나 보조분석에서 LD 조건부/fine-mapping 포함
- MI 대신 broad CVD만 다루고 MI 결과가 분리되지 않은 경우

---

## 검색 전략

## 1) 데이터베이스/엔진
- PubMed (우선)
- Google Scholar/저널 검색(보조)
- Brave web_search는 후보 수집용, 최종 검증은 PubMed/저널 원문 기준

## 2) 질환별 쿼리 뼈대
- T2D:
  - ("type 2 diabetes" OR T2D) AND ("structural variant" OR deletion OR duplication OR insertion) AND (association OR burden) AND (WGS OR "whole genome sequencing")
- MI:
  - ("myocardial infarction" OR AMI) AND ("structural variant" OR deletion OR duplication OR insertion) AND (association OR burden) AND (WGS OR sequencing)

## 3) 배제 키워드
- "copy number variation" OR CNV (초기 검색에서 제외 필터)
- "LD" "haplotype" "tag SNP" 중심 논문은 후순위

---

## 스크리닝 파이프라인
1. 제목/초록 1차: 질환/기간/SV 유형 확인
2. 본문 Methods 2차: strict no-LD 여부 확인
3. 통계 검정 추출: 모델, 공변량, 효과크기, 다중검정 방식
4. 증거등급 부여: sample size, replication, QC, sensitivity

---

## 품질 기준 (자동 점수)
총점 10점 (7점 이상 본문, 5~6점 부록)
- 표본수 충분성: 0~2
- 독립 재현 코호트: 0~2
- SV QC/validation 명시: 0~2
- 통계모형 투명성(공변량/보정): 0~2
- strict no-LD 충족도: 0~2

---

## Git 운영 규칙
- 원본 카탈로그는 유지
- 이번 라운드는 아래 신규 파일만 append/update:
  - `data/screening_template_t2d_mi_sv_no_ld.csv`
  - `notes/questions_for_next_search_round.md`
  - `reports/04_targeted_protocol_t2d_mi_sv_no_ld.md`
- `verification_status`는 반드시 단계형으로 기록:
  - `candidate`
  - `biblio_verified`
  - `method_verified`
  - `final_include`
