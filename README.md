# X Shadowban Checker

> **X(Twitter) 계정의 쉐도우밴 여부를 실시간으로 진단하는 웹 도구**

<img width="2582" height="1774" alt="image" src="https://i.imgur.com/Mslkg4o.png" />

이 프로젝트는 X(구 Twitter) 플랫폼에서 사용자 계정에 적용된 각종 제한(섀도우밴)을 확인하기 위해 개발되었습니다. X 플랫폼의 직선적이면서도 고대비 스타일의 다크 테마 UI를 중심으로 직관적인 진단 결과를 제공하며, Cloudflare Worker 기반 프록시 아키텍처를 통해 안정적인 API 통신을 보장합니다.

## 1. 프로젝트 개요 (Overview)

- **버전**: 1.1.0
- **데모**: [GitHub Pages 배포 URL](<https://jtech-co.github.io/Shadowban-Checker/index.html>)

본 프로젝트는 다음과 같은 문제를 해결합니다:
- X 플랫폼에서 사용자 모르게 적용되는 계정 제한(섀도우밴 등)의 존재 여부 확인
- Grok AI 기반 X 정책 위반 심층 분석 (Safety / Privacy / Authenticity)
- 한국어와 영어 지원

## 2. 주요 기능 (Key Features)

**UI/UX (Design)**
- **레이아웃**: 반응형 단일 페이지 구조, 모바일 및 데스크탑 최적화
- **테마**: SpaceX Market Intelligence 스타일 다크 모드, 고대비 모노크롬 디자인
- **다국어**: KR/EN 실시간 전환 지원 (Grok 검사 시 선택된 언어로 잠금)

**시스템 (Technical)**
- **밴 진단**: Search Suggestion Ban, Search Ban, Ghost Ban, Reply Deboosting 4종 동시 검사
- **X 정책 검토 (Grok)**: xAI Grok API를 활용한 계정 정책 위반 심층 분석
  - Safety (안전성) / Privacy (개인정보 보호) / Authenticity (진위성) 3개 카테고리 진단
  - 게시글, 댓글, 이미지, 아티클, 인용문 전체 검토
  - 선택한 UI 언어(EN/KR)에 맞춰 진단 결과 출력
- **보안 통신**: AES-256-CBC IP 암호화 및 SHA-256 Proof-of-Work 인증
- **CORS 우회**: Cloudflare Worker 프록시를 통한 외부 API 중계

## 3. 기술 스택 (Tech Stack)

| 구분 | 스택 | 비고 |
| --- | --- | --- |
| **Frontend** | HTML5, Vanilla JavaScript | 단일 파일 구성 |
| **Styling** | CSS3 Custom Properties | X 스타일 테마 |
| **Typography** | Inter, JetBrains Mono | Google Fonts CDN |
| **Proxy** | Cloudflare Worker | API 중계, CORS 처리, Grok API 프록시 |
| **AI 분석** | xAI Grok API (`grok-4-1-fast-reasoning`) | X 정책 위반 심층 진단 |
| **Hosting** | GitHub Pages | 정적 호스팅 |
| **외부 API** | xAI Shadowban API | 밴 상태 조회 |

## 4. 폴더 구조 (Directory Structure)

```text
/
├── index.html                # 메인 애플리케이션 (GitHub Pages 배포 대상)
├── cloudflare-worker.js      # Cloudflare Worker 프록시 — ES Modules 포맷
├── cloudflare-worker-sw.js   # Cloudflare Worker 프록시 — Service Worker 포맷
└── README.md                 # 프로젝트 문서
```

## 5. 밴 유형 설명 (Ban Type Description)

| 유형 | 한국어 | 설명 |
| --- | --- | --- |
| **Search Suggestion Ban** | 서치제안밴 | 검색 자동완성에서 계정이 제외됨 |
| **Search Ban** | 서치밴 | 검색 결과에서 포스트가 완전히 제외됨 |
| **Ghost Ban** | 고스트밴(쉐도우밴) | 답글이 대화 스레드에서 숨겨짐 |
| **Reply Deboosting** | 디부스팅 | 답글이 접히거나(스팸으로 필터링) 우선순위가 낮아짐 |

## 6. X 정책 검토 - Grok AI 분석 (X Policy Review)

"Grok 세부검사 진행" 체크박스를 활성화한 상태에서 검사를 실행하면, 밴 진단 결과와 함께 xAI Grok API를 통한 심층 정책 분석이 수행됩니다.

**진단 카테고리:**

| 카테고리 | 검토 내용 |
| --- | --- |
| **Safety (안전성)** | 폭력, 괴롭힘, 혐오 발언 등 안전 위험 요소 |
| **Privacy (개인정보 보호)** | 개인정보 공유, 도크싱, 개인정보 침해 여부 |
| **Authenticity (진위성)** | 사칭, 스팸, 조작된 미디어 여부 |

**출력 예시 (EN):**
```
[Diagnosis results]: @username No violations of X's 2026 regulations / Fully compliant with all reviewed items.

▷ Safety - No posts, replies, images, articles, or quotes promoting violence, harassment, hate speech, or other safety risks / Fully compliant with safety policies
▷ Privacy - No sharing of personal information, doxxing, or privacy violations in any reviewed content / Privacy Policy fully compliant
▷ Authenticity - All content appears genuine with no evidence of impersonation, spam, or manipulated media / Authenticity rules compliant
```

**출력 예시 (KR):**
```
[진단 결과]: @username X의 2026 규정 위반 사항 없음 / 검토된 모든 항목에 완전히 준수함.

▷ 안전성 - 폭력, 괴롭힘, 혐오 발언 또는 기타 안전 위험을 조장하는 게시물, 댓글, 이미지, 기사 또는 인용문 없음 / 안전 정책 완전히 준수
▷ 개인정보 보호 - 검토된 콘텐츠에서 개인정보 공유, 도크싱 또는 개인정보 침해 없음 / 개인정보 보호 정책 완전히 준수
▷ 진위성 - 모든 콘텐츠가 진정성 있게 보이며 사칭, 스팸 또는 조작된 미디어의 증거 없음 / 진위성 규칙 준수
```

**참고:** Grok 검사를 선택한 경우, 검사 시점에 선택된 언어(EN/KR)로 결과가 고정됩니다. 언어를 변경하려면 페이지를 새로고침한 후 새 세션에서 진행해야 합니다.

## 7. 라이선스 (License)

이 프로젝트는 MIT License에 따라 배포됩니다. 자세한 내용은 `LICENSE` 파일을 참고하세요.

---
