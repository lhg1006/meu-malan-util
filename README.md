# 메유 (MEU) — 메이플랜드 올인원 유틸리티

> **월 50,000+ PV** · Lighthouse 100점 · Google AdSense 수익화
> 기획 · 디자인 · 개발 · 운영을 단독 수행하는 프로덕션 서비스

[![Next.js](https://img.shields.io/badge/Next.js_16-000000?style=flat-square&logo=next.js&logoColor=white)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React_19-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=flat-square&logo=supabase&logoColor=white)](https://supabase.com/)
[![Vitest](https://img.shields.io/badge/Vitest-6E9F18?style=flat-square&logo=vitest&logoColor=white)](https://vitest.dev/)
[![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat-square&logo=vercel&logoColor=white)](https://vercel.com/)

🌐 **서비스**: [malan-util.com](https://malan-util.com)

---

## 서비스 소개

**메유(MEU)**는 메이플랜드 플레이어를 위한 올인원 유틸리티 서비스입니다.

공격력 계산, 강화 시뮬레이션, 아이템/몬스터 도감, 코디 시뮬레이터, 거래 수수료 계산 등 게임에 필요한 모든 도구를 한 곳에서 제공합니다.

<img src="./images/main-light.png" width="800" alt="메인 페이지" />

---

## 핵심 성과

| 지표 | 수치 |
| --- | --- |
| **월간 페이지뷰** | 50,000+ PV |
| **Lighthouse Performance** | 100점 |
| **LCP** | 0.3초 |
| **유닛 테스트** | 42개 |
| **코드 리팩토링** | 3,794줄 → 1,449줄 (61.8% 감소) |
| **커스텀 훅** | 24개 |
| **수익화** | Google AdSense |

---

## 기술 스택

| 영역 | 기술 |
| --- | --- |
| **Framework** | Next.js 16, React 19 |
| **Language** | TypeScript |
| **Styling** | Tailwind CSS |
| **Auth / DB** | Supabase (SSR + Discord OAuth) |
| **Testing** | Vitest, React Testing Library |
| **Deploy** | Vercel |
| **Security** | Nonce CSP, HSTS, Permissions-Policy |

---

## 주요 기능

### 🗡️ 계산기

<img src="./images/calc-attack.png" width="800" alt="공격력 계산기" />

**공격력 계산기**
직업별 스탯 기반 데미지 계산. 버프, 크리티컬, 방어 관통, 도핑 멀티플라이어 등 모든 변수 반영. 프리셋 5슬롯 저장 + Supabase 클라우드 동기화.

**n방컷 계산기**
몬스터 HP 기반 필요 데미지 역산. 방어력 감산, 레벨 페널티, 크리티컬, 멀티히트 스킬 반영.

**환산 스공 비교기**
현재/변경/결과 3열 비교 그리드.

<img src="./images/calc-exp.png" width="800" alt="경험치 계산기" />

**경험치 계산기**
레벨 1~200 경험치 테이블 기반. 현재 경험치 퍼센트 반영. 시간당 경험치 입력 시 레벨업 소요 시간·일수 예측.

<img src="./images/calc-exchange.png" width="800" alt="교환거래 수수료" />

**교환거래 / 택배거래 수수료**
6단계 구간별 차등 수수료 자동 계산. 최적 분할 전략 제안. 일반 vs 배달 (+1%) 비교.

<img src="./images/calc-worldcoin.png" width="800" alt="월드코인 계산기" />

**월드코인 계산기**
그리디 알고리즘 기반 최적 패키지 조합. 현금↔월드코인 양방향 변환.

---

### 🎲 시뮬레이션

<img src="./images/sim-scroll.png" width="800" alt="강화 시뮬레이터" />

**강화 시뮬레이터**
장비 강화 확률 시뮬레이션. 아이템 검색 (띄어쓰기 무시, 카테고리 유지). 확률 통계 테이블 (범위별 색상, 소수점, 오름차순). 모바일 하단 고정 바.

<img src="./images/sim-coordi.png" width="800" alt="코디 시뮬레이터" />

**코디 시뮬레이터**
장비 아이템 조합 미리보기. 직업/레벨/카테고리 필터링. 슬롯별 장착 관리.

---

### 📚 도감

<img src="./images/db-monster.png" width="800" alt="몬스터 도감" />

**몬스터 도감**
몬스터 상세 정보 + 드롭 테이블 + 보스 스폰맵. 실시간 검색 (띄어쓰기 무시).

<img src="./images/db-item.png" width="800" alt="아이템 도감" />

**아이템 도감**
아이템 상세 정보 + 드롭 몬스터 역추적. 즐겨찾기.

**맵 도감**
맵 목록 + 출현 몬스터 정보.

---

### 🔧 유틸리티

**메랜소식** — maple.land 콘텐츠 파싱 + 롤링 티커

<img src="./images/util-timetable.png" width="800" alt="배 시간표" />

**배 시간표** — 게임 내 배 출발 시간 정보

<img src="./images/util-tracker.png" width="800" alt="알리미" />

**알리미** — 시간 기반 이벤트 추적. 일/시간/분 단위 커스텀 주기 등록

---

### 🌙 반응형 + 다크 모드

모바일, 태블릿, 데스크톱 모든 화면에 최적화. 다크/라이트 모드 지원.

<div align="center">
  <img src="./images/main-dark.png" width="600" alt="다크 모드" />
  <img src="./images/mobile.png" width="180" alt="모바일" />
</div>

---

## 기술적 특징

### 성능 최적화

- **Lighthouse 100점** 유지
- **렌더링 전략 분리**: 홈 SSG (`force-static`), 계산기 CSR, 도감 ISR
- **Dynamic Import** + `ssr: false`: StatCalculator (1,773줄) 등 무거운 컴포넌트 분리
- **이미지 최적화**: 파비콘 1.2MB → 154KB
- **폰트 최적화**: 로컬 폰트 (GeistVF, NexonLv1Gothic) + CDN Pretendard (preconnect + preload, `display: swap`)

### 보안

- **Nonce 기반 CSP**: 매 요청마다 `crypto.randomUUID()` → base64 nonce 생성
- **HSTS**: `max-age=31536000; includeSubDomains`
- **Permissions-Policy**: `camera=(), microphone=(), geolocation=()`
- Google AdSense + Discord OAuth 도메인 호환 허용 목록

### 3단계 캐싱 전략

```
1. Memory (Map)        → SPA 내 즉시 접근
2. sessionStorage      → 새로고침 유지 (TTL 5분)
3. Supabase            → 영구 저장 (source of truth)
```

- CUD 3초 쿨다운 (rate limiting)
- 인증 변경 시 자동 무효화

### 인증

- **Supabase Auth** + **Discord OAuth**
- 서버/클라이언트 Supabase 클라이언트 분리
- 미들웨어 레벨 세션 리프레시

### AdSense 통합

- 스마트 재시도: 최대 3회, 5초 간격
- 광고 로드 실패 감지 → DOM 재생성
- CSP nonce 호환

---

## 테스트

**42개 유닛 테스트**로 핵심 비즈니스 로직의 정확성을 보장합니다.

<img src="./images/vitest-ui.png" width="800" alt="Vitest UI" />

**수수료 계산 (21개)** — 6구간 경계값, 일반 vs 배달, 절삭 정확도, 데이터 무결성

**월드코인 변환 (21개)** — 패키지 효율성, 그리디 알고리즘, 양방향 일관성, 엣지 케이스

---

## 아키텍처

```
src/
├── app/                        # Next.js App Router (15+ 페이지)
│   ├── page.tsx                # 홈 (SSG)
│   ├── damage/                 # 공격력 계산기 (CSR)
│   ├── scroll/                 # 강화 시뮬레이터
│   ├── item/                   # 아이템 도감
│   ├── monster/                # 몬스터 도감
│   ├── coordi/                 # 코디 시뮬레이터
│   ├── exp/                    # 경험치 계산기
│   ├── trade/                  # 수수료 계산기
│   └── ...                     # 배 시간표, 소식, 알리미 등
│
├── components/                 # 24개 커스텀 훅
│   ├── calc/                   # 공격력 계산 (6 hooks)
│   ├── scroll/                 # 강화 시뮬 (4 hooks)
│   ├── item/                   # 아이템 (5 hooks)
│   ├── monster/                # 몬스터 (4 hooks)
│   ├── coordi/                 # 코디 (3 hooks)
│   └── exp/                    # 경험치 (2 hooks)
│
├── contexts/                   # AuthContext, SoundContext
├── lib/supabase/               # 서버/클라이언트 Supabase
├── utils/                      # 계산 로직 + 42개 테스트
└── proxy.ts                    # Nonce CSP + 보안 헤더
```

---

## Author

**이효규 (Lee Hyo-gyu)**

- 🌐 [malan-util.com](https://malan-util.com)
- 📂 [@lhg1006](https://github.com/lhg1006)
- 📧 lhg961006@gmail.com
- 📝 [Blog](https://hamzz1.tistory.com/)

---

**※ 비공식 팬 메이드 프로젝트로, 메이플랜드 공식 서비스와 무관합니다.**
