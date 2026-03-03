# Draft Manuscript (v0.1)
## Structural Variant Association Without LD Modeling in Type 2 Diabetes and Myocardial Infarction (2021–2025): A Focused Evidence Synthesis

> 상태: **초안(v0.1)**  
> 작성일: 2026-03-03  
> 목적: 논문 초안 골격 + 현재까지의 근거를 엄격 기준으로 정리

---

## Abstract

### Background
구조변이(structural variant, SV)는 복합질환 유전학에서 잠재적 설명력을 가지지만, 다수 연구는 여전히 SNP/LD 기반 프록시 해석에 의존한다. 본 초안은 **LD 구조를 직접 모델링하지 않는(strict no-LD)** SV 연관연구만 대상으로, 최근 5년(2021–2025) 동안 **제2형 당뇨병(T2D)** 및 **심근경색(MI)** 영역의 근거를 재정리하였다.

### Methods
사전 정의된 기준으로 문헌을 선별하였다: (1) DEL/DUP/INS 직접 검출 및 직접 검정, (2) LD block/tag SNP/haplotype 기반 유도 추론 비사용, (3) CNV-only 연구 제외, (4) 2021년 이후. 검색은 PubMed/저널 색인/웹 검색을 병행하고, 최종 포함은 원문 Methods 검증을 우선한다.

### Results
MI/CAD 축에서는 대규모 WGS 기반 SV 연관분석의 최근 근거가 확인되었고, T2D에서는 본 기준을 동시에 만족하는 직접 SV 연관연구가 제한적이었다. 즉, **질환 간 근거 비대칭**이 관찰되며, 특히 T2D에서 strict no-LD + non-CNV + recent-window 조건을 만족하는 데이터가 희소하다.

### Conclusions
현 시점에서 strict no-LD SV 근거는 MI/CAD에서 상대적으로 형성되어 있으나, T2D는 공백이 크다. 따라서 본 주제의 본 논문은 “양성 결과 요약”보다 **근거 지형(evidence landscape) + 방법론적 공백 정의**를 중심으로 구성하는 전략이 타당하다.

---

## 1. Introduction

복합질환 유전학의 다수 성과는 SNP GWAS에 기반하지만, SV(DEL/DUP/INS)는 기능효과 크기와 기전적 직접성 측면에서 독립적 가치가 있다. 다만 실무적으로는 다음 문제가 지속된다.

1. SV 자체를 직접 검정하지 않고 LD 프록시로 우회하는 경향
2. CNV 중심 프레임에 편중되어 DEL/DUP/INS의 정밀 분해가 부족
3. 질환별로 데이터 성숙도가 다름 (심혈관 vs 대사질환)

본 연구는 위 문제를 줄이기 위해, **LD 비모델링(strict no-LD)** 기준으로 T2D와 MI 영역의 최근 근거를 제한적으로 통합한다.

---

## 2. Methods

### 2.1 Scope and eligibility

- 질환: T2D, MI (단, CAD 대규모 코호트에서 MI 관련 임상맥락이 명확한 경우 보조 포함)
- 기간: 2021–2025
- 변이: DEL/DUP/INS (CNV-only 제외)
- 분석: SV 직접 호출 + 직접 연관검정
- 제외:
  - LD block/tag SNP/haplotype 기반 주분석
  - 리뷰, 방법론 소개만 있는 비실증 논문

### 2.2 Definition of strict no-LD

아래 3개를 모두 만족할 때 strict no-LD로 판정:
- SV genotype/call이 1차 분석 단위
- 주효과 추정이 SV 변수 기반 회귀/검정으로 수행
- LD 행렬/하플로타입 구조를 모델에 사용하지 않음

**참고:** Fisher’s method 같은 p-value 결합은 허용 가능하나, 입력값이 SV 직접검정에서 산출된 값이어야 한다.

### 2.3 Quality scoring

총점 10점(본 프로젝트 운영기준):
- 표본수/검정력 (0–2)
- 독립 재현 (0–2)
- SV QC/validation (0–2)
- 통계모형 투명성 (0–2)
- strict no-LD 충족도 (0–2)

---

## 3. Results (Preliminary)

### 3.1 Myocardial infarction / coronary artery disease axis

최근 근거 중, 대규모 WGS에서 common/rare SV를 직접 분석한 CAD 연구가 확인되었다. 해당 연구는 SV 직접 분석이라는 점에서 본 프레임과 정합성이 높으며, MI 단독보다 CAD-연관 임상 스펙트럼으로 결과가 제시되는 경향이 있다.

- 해석 포인트
  - SV 기반 직접 검정 가능성은 대규모 코호트에서 현실화됨
  - 다만 phenotype 정의가 CAD 광역으로 묶이는 경우가 많아, MI-순수 신호 분리에는 한계

### 3.2 Type 2 diabetes axis

본 라운드(2021–2025, strict no-LD, non-CNV, DEL/DUP/INS)에서는 T2D에 대해 즉시 포함 가능한 high-confidence 실증 논문이 제한적이었다. T2D 문헌은 여전히 SNP/LD 기반 신호 해석 또는 CNV 중심 보고가 다수이며, strict 기준을 동시에 만족하는 연구가 상대적으로 적었다.

- 해석 포인트
  - “근거 부재”가 아니라 “기준 충족 연구의 희소성”에 가깝다
  - 향후 long-read 및 biobank-scale SV association 성숙이 핵심 공백 해소 경로

### 3.3 Cross-disease synthesis

- MI/CAD: 직접 SV 분석 연구의 신호가 형성 중
- T2D: strict no-LD + non-CNV 조건에서 근거 축적이 느림
- 결론적으로 동일한 방법론 프레임을 두 질환에 같은 강도로 적용하기 어렵고, 논문 구조도 질환별 비대칭을 반영해야 함

---

## 4. Discussion

본 초안의 핵심 기여는 “무엇이 유의했는가”보다 “현재 어떤 연구가 strict no-LD 조건을 통과하는가”를 분명히 한 데 있다.

### 4.1 Why this matters

- SV의 생물학적 직접성은 높지만, 통계 설계의 표준화가 아직 진행 중
- LD 비모델링 전략은 해석 단순성과 직접성을 제공하나, 표본수와 QC 요구가 큼

### 4.2 Practical implications for manuscript development

최종 논문은 다음 구조가 유리하다.
1. 방법론적 엄격 기준(why strict no-LD)
2. 질환별 근거지도(MI/CAD vs T2D)
3. 공백 분석(왜 T2D는 비어 보이는가)
4. 후속 연구 제안(large WGS + harmonized DEL/DUP/INS pipeline)

### 4.3 Limitations

- 본 문서는 초기 라운드 기반 초안이며 체계적 메타분석 단계 전임
- 저널별 접근 제한으로 원문 full-text 재확인이 추가 필요
- CAD와 MI 경계(phenotype granularity)에서 포함/제외 민감도 존재

---

## 5. Conclusion

2021–2025 구간에서 strict no-LD, non-CNV, DEL/DUP/INS 조건을 적용하면, MI/CAD 영역 대비 T2D 영역의 즉시 활용 가능 근거가 희소하다. 따라서 본 주제의 논문 초안은 “질환 간 근거 비대칭”을 전면에 두고, 결과 자체보다 연구 설계/데이터 성숙도 격차를 분석하는 방향이 타당하다.

---

## References (seed set; to be expanded in v0.2)

1. Rounis M, et al. **Unveiling the Genetic Landscape of Coronary Artery Disease Through Common and Rare Structural Variants.** *J Am Heart Assoc.* 2025;14(4):e036499. doi:10.1161/JAHA.124.036499. (PubMed: 39950338)

2. (방법론/배경 보조) Collins RL, et al. **A structural variation reference for medical and population genetics.** *Nature.* 2020;581:444–451. doi:10.1038/s41586-020-2287-8.

> 주: 본 레퍼런스는 v0.1 seed이며, T2D 직접 포함 논문은 v0.2에서 strict 기준으로 추가 검증 예정.
