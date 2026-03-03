# 01. Scope & Framework

## 1) 질문 재정의

원문 요청: **"structure variant에서 LD 구조 없이 테스트한 논문들"**

실무적으로는 아래 질문으로 분해됨:

- Q1. SV를 LD 기반 태깅 없이 직접 테스트한 연구 설계는 무엇인가?
- Q2. 각 설계의 강점/약점(검정력, 해석력, 재현성)은?
- Q3. 어떤 상황에서 어떤 설계를 우선 선택해야 하는가?

## 2) 포함/제외 기준

### 포함
- SV(CNV, DEL, DUP, INV, INS, MEI 등) 직접 호출/유형화
- LD 블록/태그 SNP 의존 없이 직접 통계 검정
- burden, 단일변이, family-based, de novo, 기능영향 기반 분석

### 제외
- 순수 SNP GWAS 결과에서 LD 프록시로만 SV를 간접 해석한 연구
- SV가 핵심이 아닌 부록 수준 보고

## 3) 방법론 분류(본 프로젝트의 핵심 틀)

### A. Single-SV association (직접 단일변이 검정)
- 형태: 각 SV에 대해 case-control 또는 quantitative trait 회귀
- 장점: 해석 직관적
- 단점: 희귀 SV는 검정력 약함

### B. Rare-SV burden test
- 형태: gene/region/pathway 단위로 희귀 SV를 집계하여 검정
- 장점: 희귀 신호를 모아 검정력 향상
- 단점: 집계 규칙(길이/기능가중치)에 민감

### C. Trio/family de novo framework
- 형태: 부모-자녀 전달패턴/신규돌연변이로 위험도 평가
- 장점: 인구집단 층화(confounding) 완화
- 단점: 대규모 trio 필요, 비용 큼

### D. Functional-impact first test
- 형태: 발현, 조절영역, 3D genome 교란을 기반으로 효과 검정
- 장점: 생물학적 해석력 높음
- 단점: annotation 품질 의존

## 4) 읽는 법 (카탈로그 해석)

`ld_dependence` 컬럼 기준:
- `none-direct` : LD 구조를 통계 모델에 쓰지 않음(직접 SV)
- `minimal` : QC/보조 단계에서만 간접 참고
- `mixed` : 일부 분석에서 LD/하플로타입 개념 병행

본 과제는 우선 `none-direct` 중심으로 요약.
