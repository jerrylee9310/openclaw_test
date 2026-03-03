# 02. Synthesis Report (v0.1)

## TL;DR

LD 구조를 직접 쓰지 않는 SV 분석은 대체로 아래 3축으로 수렴합니다.

1. **직접 SV 단일 검정**: 해석이 쉬우나 희귀변이에서 약함
2. **희귀 SV burden 검정**: 검정력 증가, 하지만 집계 규칙 설계가 핵심
3. **trio/de novo 기반 분석**: 인구집단 교란에 강하지만 샘플 확보 비용 큼

---

## 1) 왜 LD-free 접근이 필요한가

SV는 SNP처럼 촘촘한 태깅이 잘 안 되고, 특히 아래에서 LD 프록시가 약함:
- 반복서열 인접/복잡재배열 구간
- 다대립(multi-allelic) SV
- 긴 삽입/역위 등 short-read에서 부정확한 클래스

즉, **"LD로 간접추론"보다 "직접 관측 + 직접 검정"이 타당**한 경우가 많습니다.

## 2) 설계별 비교

### A. Single-SV
- 추천 상황: 공통 SV, 표본 수 큼, 효과크기 중간 이상
- 실패 패턴: 희귀 SV 다중검정에서 power 부족

### B. Rare-SV burden
- 추천 상황: 희귀질환/정신질환/발달질환
- 핵심: gene set/기능 annotation을 사전에 명확히 고정

### C. Trio/de novo
- 추천 상황: ASD, DD, 선천성질환
- 장점: population structure confounding 최소화

### D. Functional-first
- 추천 상황: 조절영역 교란 메커니즘 탐색
- 주의: annotation database 업데이트 따라 결과 변동 가능

## 3) 실무 적용 체크리스트

- SV caller 2개 이상 교차확인(precision/recall trade-off)
- 길이/클래스별 QC 임계값 분리
- burden 단위(gene/region/pathway) 사전등록
- negative control phenotype로 inflation 확인
- 재현 코호트(out-of-sample)에서 방향성 재검증

## 4) 이번 정리의 해석

이번 폴더는 **문헌 정리 + 방법론 프레임**을 먼저 고정한 상태입니다.
다음 라운드에서는 DOI/저널 메타데이터를 자동 검증해 `paper_catalog.csv`를 확정판(v1.0)으로 업그레이드하면 바로 발표/공유 가능한 수준이 됩니다.
