# 03. Update after Brave API enabled

업데이트 시각: 2026-03-03

## 무엇이 달라졌나

Brave `web_search`가 정상 동작하여, 이전 v0.1의 초안 상태에서
**검증 링크 기반 shortlist(v1)**를 다시 구성했습니다.

- 신규 파일: `data/verified_shortlist_v1.csv`
- 목적: "LD 구조를 직접 쓰지 않는 SV 분석"에 초점 맞춘 빠른 레퍼런스 세트

## 이번 라운드 핵심 결론

1. **정신질환(SCZ)** 쪽은 CNV burden 대규모 연구(예: PGC 계열)가 매우 강한 축
2. **신경발달/희귀질환** 쪽은 trio + de novo SV 분석이 LD-free 전략의 중심
3. **기술 트렌드**는 short-read 보완을 위한 long-read/pangenome 확장

## 방법론별 추천 사용처

- burden(CNV/SV): 케이스-컨트롤 대규모 코호트
- trio/de novo: ASD, DD, 조기발병 질환
- long-read direct SV: unresolved case, complex rearrangement

## 다음 권장 작업 (바로 가능)

- `verified_shortlist_v1.csv`를 기반으로
  1) **진짜 SV 중심 논문만 남기는 strict 필터**
  2) 각 논문에서 통계식(OR, burden model, covariates) 추출
  3) 발표용 표(질환별/설계별/LD의존성별) 제작

필요하면 내가 다음 턴에서 바로 **strict 필터 + 발표표 1장짜리**까지 만들어줄게.
