# SINTEX Sales Hunter — 프로젝트 메모

> 마지막 업데이트: 2026-08-31
> 다음 작업: **V1 설계부터 시작**

## 내일 할 일 (Next Step)

거창한 완전자동화가 아니라, 아래 한 가지 흐름부터 실제로 동작하게 만드는 것이 V1의 목표.

```
[USA + Bridesmaid + Brand] → START HUNTING
→ 실제 유효한 잠재 Buyer들이 분석·점수화되어 화면에 나타난다
```

---

## 1. 목적

AI가 해외 신규 거래처를 계속 찾아주고, 분석하고, 연락 준비까지 해주는 SINTEX 전용 로컬 해외영업 시스템.

SINTEX는 특정 보유 원단을 판매하는 회사가 아니라 다음 능력을 가진 회사:

- 원단 제조 가능
- 원단 개발 가능
- 아시아 생산 인프라 보유
- 필요한 원단 소싱 가능

따라서 접근 순서는 **원단 → buyer**가 아니라 **buyer → 무엇을 제안할지 결정**.

## 2. AI가 찾을 대상

- **분야**: Bridal / Bridesmaid / Evening / Occasion / MOB
- **업체 유형**: Brand / Buyer / Wholesaler / Importer / Distributor / Garment Manufacturer / Vendor
- **국가**: 미국부터 시작 → 이후 UK, Europe, UAE 등으로 확대

## 3. 버튼 한 번 누르면 할 일

입력 예: `USA / Bridesmaid + Evening / Brand + Manufacturer` → `[START HUNTING]`

자동 진행 파이프라인:

1. 업체 발굴
2. 홈페이지 조사
3. 제품/컬렉션 분석
4. 사용 원단 추정
5. SINTEX와의 적합도 평가 (A/B/C 또는 점수화)
6. 담당자 탐색
7. Email / LinkedIn / Instagram 탐색
8. 제안할 원단 추천
9. Cold Email / DM 작성

## 4. 결과 화면 예시

```
ABC BRIDAL — FIT 92/100
USA / Bridesmaid Brand

주요 제품: Bridesmaid / Occasion
관찰 소재: Satin / Chiffon / Crepe
가격 포지션: Mid-market

왜 좋은 타깃인가?
SINTEX가 생산·소싱할 수 있는 소재와 제품 구성이 잘 맞음.

무엇을 제안할까?
Soft Satin / Matte Chiffon / Crepe

Contact
Product Development 담당자 ✓ / Email ✓ / LinkedIn ✓ / Instagram ✓

[EMAIL] [DM] [CONTACT] [ADD FABRIC]
```

단순 회사 리스트가 아니라 **"왜 연락해야 하는지 + 무엇을 팔아야 하는지"**까지 AI가 판단.

## 5. 원단 사진은 나중에 필요할 때만

- 처음부터 기존 원단 수천 개를 등록하지 않는다.
- AI가 좋은 buyer를 발견하고 "이 업체엔 Soft Satin을 제안하는 게 좋음"이라 판단하면, 사무실에서 해당 원단을 찾거나 새로 개발/소싱.
- 필요할 때 휴대폰으로 사진 찍어 등록 → AI가 buyer와 실제 원단을 재매칭.

흐름: `Buyer 발견 → Opportunity 발견 → 적합한 원단 찾기/개발 → 사진 등록 → 제안`

## 6. 영업 파이프라인 관리

상태 흐름:

```
NEW → ANALYZED → CONTACT READY → CONTACTED → FOLLOW-UP → REPLIED → SAMPLE REQUEST → CUSTOMER
```

- 답장 없으면 Follow-up 자동 생성, 답장 오면 자동 Follow-up 중단.
- Cold Email: 최종적으로 자동 발송 가능하게 만들되, 초기엔 **승인 → 발송** 방식.
- LinkedIn/Instagram: 계정 리스크 때문에 **AI가 찾기+분석+DM 초안 작성 → 사람이 Send**.

## 7. 비용 최소화 원칙

기존 보유 자원 활용: NAS + 사무실 Desktop + 인터넷 + 원단/생산 인프라 + 휴대폰 카메라

기본 스택: `Docker + n8n + PostgreSQL + 자체 웹 화면 + (필요시) Ollama`

- 로컬 모델 우선 사용, 중요 분석만 GPT/Claude/Gemini API 사용.
- 검색·연락처 탐색도 무료 방법 우선, 가치 높은 업체인데 담당자 이메일을 못 찾은 경우에만 Apollo 등 유료 enrichment 사용.

구조: `무료로 1,000개 탐색 → AI가 후보 압축 → 좋은 업체만 상세 분석 → 정말 필요한 소수에만 돈 사용`

## 8. 개발 순서

| 단계 | 내용 |
|---|---|
| **V1** | 회사 자동 발굴 → AI 분석 → Fit Score → DB 저장 |
| V2 | 담당자 / Email / LinkedIn / Instagram 탐색 |
| V3 | 개인화 Cold Email / DM 생성 → 승인 → 발송 |
| V4 | Follow-up 자동화 / 답장 감지 / CRM 업데이트 |
| V5 | AI가 새로운 시장까지 스스로 탐색하고 기존 Lead 재평가 |

## 한 문장 요약

> SINTEX Sales Hunter = "미국 Bridesmaid 찾아"라고 하면 AI가 해외 업체를 발굴하고, 실제 제품과 사업을 조사해서 SINTEX에 맞는 거래처인지 평가하고, 무엇을 제안할지 결정하고, 담당자와 연락처를 찾아 개인화된 영업 메시지까지 준비해주는 로컬 AI 해외영업 시스템.
