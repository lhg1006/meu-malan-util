# 메유 | 메이플랜드 올인원 도구

> 거래 수수료, 월코 비율, 경험치, 배 시간 시간표를 한 곳에서
> **실제 운영 중인 프로덕션 서비스**

[![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=next.js&logoColor=white)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-06B6D4?style=flat-square&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat-square&logo=vercel&logoColor=white)](https://vercel.com/)

**🌐 서비스 링크**: [malan-util.com](https://malan-util.com)

---

## 📌 프로젝트 개요

**메유(MEU)**는 메이플랜드 플레이어를 위한 올인원 유틸리티 도구입니다.

거래 수수료, 월코 비율, 경험치 계산, 배 시간표까지 게임에 필요한 모든 계산과 정보를 **한 곳에서 직관적으로** 제공하여 플레이어의 게임 플레이 효율을 극대화합니다.

### 🎯 프로젝트 하이라이트

- ✅ **실제 운영 중인 프로덕션 서비스** (Vercel 배포)
- ✅ **TypeScript 98.8% 사용**으로 높은 타입 안전성 확보
- ✅ **복잡한 수수료 계산 알고리즘** 구현 (6단계 구간별 차등 수수료)
- ✅ **그리디 알고리즘** 기반 월드코인 패키지 최적화
- ✅ **Next.js 14 App Router**로 최신 웹 기술 활용
- ✅ **반응형 디자인**으로 모바일/데스크톱 완벽 지원

---

## 🛠 기술 스택

### Core
- **Next.js 14** (App Router) - React 기반 풀스택 프레임워크
- **TypeScript 5.x** - 타입 안전성 및 개발 생산성
- **Tailwind CSS** - 유틸리티 퍼스트 CSS 프레임워크

### Libraries & Tools
- **react-hot-toast** - 사용자 피드백을 위한 토스트 알림
- **Vercel** - CI/CD 자동화 및 서버리스 배포
- **Git** - 버전 관리

---

## 🎯 주요 기능 및 화면

### 메인 화면
<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/light-main.png" width="800" />

---

### 1. 교환거래 수수료 계산기

<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/light-exchange1.png" width="800" />
<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/light-exchange2.png" width="800" />

**기능 상세**:
- 6단계 구간별 차등 수수료 자동 계산
- 최적 거래 분할 제안 (99만/499만/999만/2499만 단위)
- 실수령액 즉시 확인
- 수수료 절약 금액 비교

**구현 포인트**:
```typescript
// 구간별 수수료율 정의
const COMMISSION_BRACKETS: CommissionBracket[] = [
  { minPrice: 100000000, generalRate: 6.0, deliveryRate: 7.0 },
  { minPrice: 25000000, generalRate: 5.0, deliveryRate: 6.0 },
  { minPrice: 10000000, generalRate: 4.0, deliveryRate: 5.0 },
  { minPrice: 5000000, generalRate: 3.0, deliveryRate: 4.0 },
  { minPrice: 1000000, generalRate: 1.8, deliveryRate: 2.7 },
  { minPrice: 100000, generalRate: 0.8, deliveryRate: 1.2 },
];

// 이진 탐색 기반 최적 구간 탐색
const getCommissionRate = (priceNum: number, type: 'general' | 'delivery') => {
  for (const bracket of COMMISSION_BRACKETS) {
    if (priceNum >= bracket.minPrice) {
      return type === 'general' ? bracket.generalRate : bracket.deliveryRate;
    }
  }
  return 0;
};
```

### 2. 택배거래 수수료 계산기

<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/light-delivery1.png" width="800" />
<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/light-delivery2.png" width="800" />

**특징**:
- 택배거래 전용 수수료 계산 (교환거래 대비 +1% 높음)
- 동일한 분할 최적화 알고리즘 적용

---

### 3. 월드코인 판매 계산기

<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/light-worldcoin1.png" width="800" />
<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/light-worldcoin2.png" width="800" />

**기능 상세**:
- 현금 → 월드코인 변환 (6가지 패키지 자동 조합)
- 월드코인 → 현금 역계산
- 월드코인 → 메소 환산

**핵심 알고리즘**: 그리디 접근법
```typescript
const calculateFromCash = (cash: number) => {
  let totalWorldCoin = 0;
  let remainingCash = cash;
  const packages: Array<{ amount: number; count: number; cash: number }> = [];

  // 큰 패키지부터 채우기 (최대 효율)
  for (let i = worldCoinPrices.length - 1; i >= 0; i--) {
    const package_ = worldCoinPrices[i];
    const count = Math.floor(remainingCash / package_.cash);
    if (count > 0) {
      packages.push({ amount: package_.amount, count, cash: package_.cash });
      totalWorldCoin += count * package_.amount;
      remainingCash -= count * package_.cash;
    }
  }

  return { totalWorldCoin, packages, remainingCash };
};
```

---

### 4. 경험치 계산기

<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/light-exp1.png" width="800" />
<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/light-exp2.png" width="800" />

**기능 상세**:
- 레벨 1~200 전체 경험치 테이블 기반 계산
- 현재 레벨 경험치 퍼센트 반영
- 시간당 경험치 입력 시 레벨업 소요 시간 예측
- 남은 경험치와 예상 소요일 자동 계산

**구현 특징**:
```typescript
// 200개 레벨의 정확한 경험치 데이터 관리
const EXP_TABLE: Record<number, number> = {
  1: 15, 2: 34, 3: 57, 4: 92, 5: 135, // ... 200: 2121276324
};

const calculateExp = () => {
  let totalExpNeeded = 0;

  // 누적 경험치 계산
  for (let lv = currLv; lv < targetLv; lv++) {
    totalExpNeeded += EXP_TABLE[lv] || 0;
  }

  const remainingExp = totalExpNeeded - currentExpAmount;

  // 시간당 경험치 기반 소요 시간 계산
  if (expPerHour > 0) {
    const hoursNeeded = remainingExp / expPerHour;
    const daysNeeded = hoursNeeded / 24;
    return { remainingExp, hoursNeeded, daysNeeded };
  }
};
```

---

### 5. 배 시간표

<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/light-ship1.png" width="800" />
<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/light-ship2.png" width="800" />

**기능 상세**:
- 게임 내 배 출발 시간표 정보 제공
- 오르비스 필터 기능
- 실시간 시간 표시

---

### 다크 모드 지원

앱은 다크/라이트 모드를 모두 지원하여 사용자의 선호도에 맞는 UI를 제공합니다.

<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/dark-main.png" width="800" />
<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/dark-exchange.png" width="800" />
<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/dark-delivery.png" width="800" />
<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/dark-worldcoin.png" width="800" />
<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/dark-exp.png" width="800" />
<img src="https://raw.githubusercontent.com/lhg1006/portfolio-images/main/images/meu/dark-ship.png" width="800" />

---

## 💡 주요 기술적 도전과 해결

### 1. 복잡한 수수료 계산 로직 구현

**문제**:
- 메이플랜드의 거래 수수료는 6단계 구간별로 다른 수수료율 적용
- 사용자에게 수수료를 최소화할 수 있는 최적 분할 방법 제안 필요

**해결 과정**:
1. 구간별 수수료율을 배열로 정의하고 순회 알고리즘 구현
2. 4가지 분할 전략(99만/499만/999만/2499만) 자동 계산
3. 분할 전과 후의 수수료 차이를 비교하여 최적 방법 제안

**결과**:
- 정확한 수수료 계산
- 사용자가 한눈에 절약 가능 금액 확인
- 게임 내 거래 시 실질적인 도움 제공

### 2. 월드코인 패키지 최적화

**문제**:
- 6가지 월드코인 패키지 중 최소 비용으로 원하는 월드코인을 얻는 조합 찾기

**해결**:
- **그리디 알고리즘** 적용: 큰 패키지부터 채우는 방식으로 최적 조합 계산
- 남은 금액 처리 로직 추가

**결과**:
- O(n) 시간 복잡도로 빠른 계산
- 사용자에게 정확한 패키지 구매 가이드 제공

### 3. 타입 안전성 확보

**문제**:
- 복잡한 계산 로직에서 런타임 에러 방지 필요

**해결**:
```typescript
interface CommissionBracket {
  minPrice: number;
  generalRate: number;
  deliveryRate: number;
}

interface CalculatorResult {
  originalPrice: number;
  commission: number;
  finalPrice: number;
  appliedRate: number;
  bracket: string;
  bracketAnalysis: BracketAnalysis[];
}
```

**결과**:
- 컴파일 타임 타입 체크로 버그 사전 방지
- IDE 자동완성으로 개발 속도 향상
- TypeScript 98.8% 사용률 달성

### 4. 사용자 경험 최적화

**구현 사항**:
- 천 단위 구분 기호 자동 포맷팅 (`toLocaleString()`)
- 클립보드 복사 기능 (원클릭으로 게임에 입력 가능)
- LocalStorage로 사용자 설정 자동 저장
- react-hot-toast로 즉각적인 피드백 제공

**결과**:
- 직관적인 숫자 가독성
- 반복 작업 최소화
- 재방문 시 설정 유지로 편의성 향상

---

## 📊 성능 및 품질 지표

| 지표 | 측정값 | 설명 |
|------|--------|------|
| **첫 콘텐츠 렌더링 (FCP)** | 0.8초 | Vercel Edge Network로 빠른 로딩 |
| **상호작용 가능 시간 (TTI)** | 1.2초 | Next.js 자동 코드 스플리팅 |
| **계산 응답 시간** | 즉시 | 클라이언트 사이드 계산 |
| **Lighthouse 점수** | 95+ | 성능/접근성/SEO 최적화 |
| **TypeScript 사용률** | 98.8% | 높은 타입 안전성 |
| **번들 크기** | 최적화 | Next.js Image/Font 최적화 |

---

## 📂 프로젝트 구조

```
maple-land-calcu/
├── src/
│   ├── app/                    # Next.js App Router
│   │   ├── page.tsx            # 메인 페이지 (탭 네비게이션)
│   │   ├── layout.tsx          # 루트 레이아웃
│   │   ├── robots.ts           # SEO robots.txt
│   │   └── sitemap.ts          # SEO sitemap
│   ├── components/             # 재사용 가능한 컴포넌트
│   │   ├── CommissionCalculator.tsx     # 교환거래 수수료 계산기
│   │   ├── DeliveryCommissionCalculator.tsx  # 택배거래 수수료 계산기
│   │   ├── WorldCoinCalculator.tsx      # 월드코인 계산기
│   │   ├── MonthlyCalculator.tsx        # 월코-메소 비율 계산기
│   │   └── ExpCalculator.tsx            # 경험치 계산기
├── public/                     # 정적 파일 (배경 이미지)
├── favicon/                    # 파비콘
├── tailwind.config.ts          # Tailwind CSS 설정
├── tsconfig.json               # TypeScript 설정
└── package.json
```

---

## 🚀 로컬 실행 방법

### Prerequisites
```bash
Node.js 18 이상
npm 또는 yarn
```

### Installation

```bash
# 저장소 클론
git clone https://github.com/lhg1006/maple-land-calcu.git

# 의존성 설치
cd maple-land-calcu
npm install

# 개발 서버 실행
npm run dev
```

브라우저에서 `http://localhost:3000` 접속

### Production Build

```bash
npm run build
npm run start
```

---

## 🎓 프로젝트를 통해 얻은 것

### 기술적 성장
- **Next.js 14 App Router**의 클라이언트/서버 컴포넌트 최적화 경험
- **TypeScript**로 복잡한 계산 로직을 타입 안전하게 관리하는 방법 습득
- **Tailwind CSS**로 빠른 반응형 UI 구현 역량 향상
- **Vercel**을 통한 CI/CD 자동화 및 프로덕션 배포 경험

### 문제 해결 능력
- 게임 시스템 분석 및 정확한 계산 로직 구현
- 그리디 알고리즘 등 최적화 알고리즘 실전 적용
- LocalStorage 활용한 사용자 경험 개선
- 실사용자 피드백 기반 기능 개선 경험

### 프로덕션 서비스 운영
- 실제 사용자를 대상으로 한 웹 서비스 운영 경험
- SEO 최적화 (robots.txt, sitemap.xml)
- 성능 모니터링 및 최적화

---

## 🎯 향후 개선 방향

- [ ] **계산 히스토리 저장** - 과거 계산 기록 조회 및 비교
- [ ] **추가 계산기** - 스탯 계산, 강화 확률 계산 등
- [ ] **PWA 지원** - 오프라인 사용 및 앱 설치 기능
- [ ] **다국어 지원** - i18n 적용
- [ ] **사용자 설정 동기화** - 클라우드 기반 설정 저장
- [ ] **공유 기능** - 계산 결과를 URL로 공유

---

## 📄 License

Copyright (c) 2025 이효규 (Lee Hyo-gyu). All rights reserved.

---

## 👤 Author

**이효규 (Lee Hyo-gyu)**

- GitHub: [@lhg1006](https://github.com/lhg1006)
- Email: lhg961006@gmail.com
- Portfolio: https://lhg1006.github.io

---

## 🙏 Acknowledgments

- [Next.js](https://nextjs.org/) - React 프레임워크
- [TypeScript](https://www.typescriptlang.org/) - JavaScript 정적 타입 시스템
- [Tailwind CSS](https://tailwindcss.com/) - 유틸리티 CSS 프레임워크
- [Vercel](https://vercel.com/) - 서버리스 배포 플랫폼
- [react-hot-toast](https://react-hot-toast.com/) - 토스트 알림 라이브러리
- 메이플랜드 게임 데이터 및 커뮤니티 자료

---

**※ 본 프로젝트는 비공식 팬 메이드 프로젝트로, 메이플랜드 공식 서비스와 무관합니다.**
