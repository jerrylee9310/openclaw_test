# Limitations & Verification TODO

## 현재 한계

1. 이 세션에서 `web_search` 도구가 Brave API 키 미설정으로 비활성화됨.
2. 따라서 논문 메타데이터(연도/DOI/저널) 자동확정이 불완전.
3. 현재 `paper_catalog.csv`는 **초기 후보 정리본**이며 수동 검증 필요.

## 검증 TODO (v1.0 만들기)

- [ ] 각 항목 DOI 확인 (PubMed / Crossref / 저널 페이지)
- [ ] 제목 정식명 일치 여부 확인
- [ ] 분석 설계가 truly LD-free인지 Method 섹션으로 재확인
- [ ] 재현 코호트 유무, 표본수, 통계모형 세부 기록
- [ ] 최종적으로 `verification_status=verified`만 남긴 확정표 생성

## 추천 업그레이드 순서

1) 카탈로그 10편 → 25편으로 확장
2) 질환군(ASD/SCZ/CVD/희귀질환)별 소표 작성
3) 결과 해석 충돌 논문(positive vs null) 분리 비교
4) 최종 발표용 PDF/슬라이드 생성
