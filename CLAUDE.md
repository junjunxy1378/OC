## 프로젝트 개요
Overlap Cloner plasmid assembly 반응을 계산하는 모바일 친화적 웹앱.

## 자료
- `/Users/jun/claude-project/OC/OC.xlsx`: 계산 기준 Excel 파일 (Frag#2~5 시트)
- `/Users/jun/claude-project/OC/_codex/`: Codex가 작성한 레퍼런스 구현체 및 스펙 문서
- `/Users/jun/claude-project/OC/index.html`: 현재 구현된 단일 파일 웹앱

## 배포
- GitHub: https://github.com/junjunxy1378/OC.git
- GitHub Pages: https://junjunxy1378.github.io/OC/
- 업데이트: `git add index.html && git commit -m "설명" && git push`

## 핵심 계산 공식 (Excel 수식 기반)
```
pmol        = mass(ng) × 1,000,000 / (660 × bp)          // B4 = B3/660*1000000/B2
insert_mass = vectorPmol × 660 × insert_bp / 1,000,000   // B7 = B8*660*B6/1000000
transfer_vol = mass / concentration(ng/μL)                 // E3 = B3/D3
DW          = totalVol - enzyme - buffer - Σ(DNA vols)    // H5 = H2-H3-H4-E3-E7...
```

## Buffer preset (반응 부피별)
| 반응 총량 | Enzyme | Buffer |
|-----------|--------|--------|
| 10 μL     | 1 μL   | 1 μL   |
| 15 μL     | 1 μL   | 1.5 μL |
| 20 μL     | 1 μL   | 2 μL   |
| 30 μL     | 1 μL   | 3 μL   |

## 경고 조건
- 총 DNA(ng) ≥ 300 → 빨간색 경고
- DW < 0 → 빨간색 경고 (농도 높이거나 반응 부피 늘릴 것)
- 모든 fragment 입력 완료 전까지 DW, 총 DNA는 "—" 표시

## 구현 현황 (index.html)
- Fragment 수: 2~5개 선택
- Vector(#1): 길이/양/농도 입력 → pmol, 사용 부피 자동 계산
- Insert(#2~N): 길이/농도 입력 → 1:1 pmol 기준 필요량, 부피 자동 계산
- 반응 부피: 10/15/20/30 μL 선택
- 반응 조성표: 소수점 2자리 표시
- Tailwind CSS CDN 사용 (외부 의존성 최소화)

## Excel 원본 주의사항
- DNA amount 단위: Excel 레이블은 "ug"지만 실제 값은 ng처럼 동작 (미확인)
- Frag#5 E3/E7 수식이 Excel에서 반전되어 있음 (버그) → 앱에서는 amount/concentration으로 정규화
- Frag#4 20μL 컬럼 불완전 → 앱에서는 일반 공식으로 처리

## Frag#2 검증 기준값
입력: Vector(4445bp, 200ng, 84ng/μL) / Insert#2(976bp, 12ng/μL)
- Insert#2 필요량: 43.9145 ng
- Vector 사용 부피: 2.3810 μL
- Insert#2 사용 부피: 3.6595 μL
- 총 DNA: 243.91 ng
- DW (10μL): 1.9595 μL
