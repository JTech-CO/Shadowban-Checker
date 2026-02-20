# X Shadowban Checker

> **X(Twitter) 계정의 쉐도우밴 여부를 실시간으로 진단하는 웹 도구**

<img width="2580" height="1652" alt="image" src="https://i.imgur.com/ZNc7ue0.png" />

이 프로젝트는 X(구 Twitter) 플랫폼에서 사용자 계정에 적용된 각종 제한(쉐도우밴)을 확인하기 위해 개발되었습니다. X 플랫폼의 직선적이면서도 고대비 스타일의 다크 테마 UI를 중심으로 직관적인 진단 결과를 제공하며, Cloudflare Worker 기반 프록시 아키텍처를 통해 안정적인 API 통신을 보장합니다.

## 1. 프로젝트 개요 (Overview)

- **버전**: 1.0.0
- **링크**: [X 쉐도우밴 진단기](<https://jtech-co.github.io/Shadowban-Checker/index.html>)

본 프로젝트는 다음과 같은 문제를 해결합니다:
- X 플랫폼에서 사용자 모르게 적용되는 계정 제한(쉐도우밴 등)의 존재 여부 확인
- 한국어와 영어 지원

## 2. 주요 기능 (Key Features)

**UI/UX (Design)**
- **레이아웃**: 반응형 단일 페이지 구조, 모바일 및 데스크탑 최적화
- **테마**: X 플랫폼 공식 스타일 다크 모드(Pure Black), 고대비 모노크롬 디자인
- **다국어**: KR/EN 실시간 전환 지원

**시스템 (Technical)**
- **밴 진단**: Search Suggestion Ban, Search Ban, Ghost Ban, Reply Deboosting 4종 동시 검사
- **보안 통신**: AES-256-CBC IP 암호화 및 SHA-256 Proof-of-Work 인증
- **CORS 우회**: Cloudflare Worker 프록시를 통한 외부 API 중계

## 3. 기술 스택 (Tech Stack)

| 구분 | 스택 | 비고 |
| --- | --- | --- |
| **Frontend** | HTML5, Vanilla JavaScript | 단일 파일 구성 |
| **Styling** | CSS3 Custom Properties | X 스타일 변수 시스템 |
| **Typography** | Inter, JetBrains Mono | Google Fonts CDN |
| **Proxy** | Cloudflare Worker | API 중계 및 CORS 처리 |
| **Hosting** | GitHub Pages | 정적 호스팅 |
| **외부 API** | fia-s.com Shadowban API | 밴 상태 조회 |

## 4. 폴더 구조 (Directory Structure)

```text
/ Shadowban-Checker
├── index.html              # 메인 애플리케이션 (GitHub Pages 배포 대상)
├── cloudflare-worker.js    # Cloudflare Worker 프록시 (Cloudflare에 별도 배포)
├── README.md               # 프로젝트 문서
│
│  ── 로컬 테스트 전용 (깃허브에 포함되지 않음) ──
├── server.js               # Express 프록시 서버 (로컬 개발용)
├── package.json            # Node.js 의존성 (로컬 개발용)
└── public/
    └── index.html          # 로컬 서버용 사본
```

## 5. 밴 유형 설명 (Ban Type Description)

| 유형(영어) | 유형(한국어) | 설명 |
| --- | --- | ---|
| **Search Suggestion Ban** | 서치제안밴 | 검색 자동완성에서 계정이 제외됨 |
| **Search Ban** | 서치밴 | 검색 결과에서 포스트가 완전히 제외됨 |
| **Ghost Ban** | 고스트밴(쉐도우밴) | 답글이 대화 스레드에서 숨겨짐 |
| **Reply Deboosting** | 디부스팅 | 답글이 접히거나(스팸으로 필터링) 우선순위가 낮아짐 |

## 6. 라이선스 (License)

이 프로젝트는 MIT License에 따라 배포됩니다. 자세한 내용은 `LICENSE` 파일을 참고하세요.

---
