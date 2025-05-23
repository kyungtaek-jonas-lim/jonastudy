# 📌 React란?  

## 1️⃣ React란 무엇인가?  
- **React는 JavaScript 라이브러리**로, 사용자 인터페이스(UI)를 효율적으로 구축하는 데 사용됩니다.  
- **컴포넌트 기반(Component-based)**: UI를 재사용 가능한 작은 단위(컴포넌트)로 나누어 개발할 수 있습니다.  
- **선언형(Declarative) 프로그래밍**을 사용하여, 개발자가 UI의 최종 상태를 정의하면 React가 자동으로 업데이트해 줍니다.  
- **가상 DOM(Virtual DOM)**을 활용해 최소한의 DOM 조작으로 성능을 최적화합니다.  

---

## 2️⃣ 왜 React를 사용할까?  

### 🎯 **React의 장점**  
✅ **가볍고 빠름** – 가상 DOM을 사용하여 최적화된 렌더링 제공.  
✅ **배우기 쉬움** – JSX 문법을 사용해 직관적인 개발 가능.  
✅ **강력한 커뮤니티와 생태계** – 풍부한 라이브러리, 플러그인, 오픈소스 지원.  
✅ **유연성과 확장성** – 다양한 라이브러리, 프레임워크, 백엔드 기술과 쉽게 결합 가능.  
✅ **SEO 친화적** – Next.js와 같은 프레임워크를 활용하면 검색 엔진 최적화(SEO)가 가능.  

### 🔄 **다른 프레임워크와 비교**  
|  | **React** | **Vue.js** | **Angular** |  
|----|----|----|----|  
| **유형** | 라이브러리 | 프레임워크에 가까운 라이브러리 | 풀스택 프레임워크 |  
| **학습 난이도** | 중간 (JSX 및 상태 관리 학습 필요) | 쉬움 (문법이 직관적) | 어려움 (TypeScript, 구조적 패턴 학습 필요) |  
| **생태계** | 매우 큼 (Facebook 지원) | 큼 (Evan You 및 커뮤니티 중심) | 큼 (Google 지원) |  
| **유연성** | 높음 (필요한 도구만 선택) | 높음 | 낮음 (일관된 구조 강제) |  
| **성능** | 빠름 (가상 DOM 사용) | 빠름 | 무거움 (초기 로딩 속도 느림) |  

---

## 3️⃣ React 배우기 🚀  

### 📌 **프로젝트 시작하기**  
- **패키지 매니저**  
  - **npm** – 기본 패키지 관리자.  
  - **yarn** – 속도와 안정성이 강화된 npm 대안.  
  - **bun** – 가장 빠른 패키지 관리자(실험적).  
- **React 프로젝트 생성**  
  - **Vite** – 빠르고 효율적인 최신 빌드 도구 (🔥 가장 많이 사용됨).  
  - **Create React App (CRA)** – 공식 제공 도구지만, Vite에 비해 느림.  
  - **Next.js** – 서버 사이드 렌더링(SSR), 정적 사이트 생성(SSG) 지원.  

---

## 4️⃣ 핵심 개념 🎯  

### 🛠 **상태 관리 (State Management)**  
✔ **State (상태)** – 컴포넌트 내부에서 관리하는 데이터.  
✔ **Props (프롭스)** – 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달하는 방법.  
✔ **Hooks (훅)** – 함수형 컴포넌트에서 상태 및 생명주기 관리.  
  - `useState` – 상태 관리.  
  - `useEffect` – 부수 효과 처리 (예: API 요청, 타이머 설정).  
  - `useContext` – 전역 상태 공유(Prop Drilling 방지).  
  
✔ **전역 상태 관리 라이브러리**  
  - **Context API** – 간단한 글로벌 상태 관리.  
  - **Redux** – 복잡한 상태 관리를 위한 중앙 집중식 도구.  
  - **Zustand** – Redux보다 가벼운 상태 관리 라이브러리.  

---

### 🔄 **React 라이프사이클**  
- **Mount (마운트)** – 컴포넌트가 생성될 때 실행.  
- **Update (업데이트)** – 상태 또는 props가 변경될 때 실행.  
- **Unmount (언마운트)** – 컴포넌트가 제거될 때 실행.  

---

### 🔗 **비동기 처리 (Async) & 데이터 페칭**  
- JavaScript의 **이벤트 루프(Event Loop) 및 비동기 처리(Promise, async/await)** 개념을 기반으로 동작.  
- React에서 API 요청 시 `useEffect`를 활용하여 실행.  
- **React Query / SWR**을 사용하면 캐싱과 데이터 동기화가 더욱 쉬워짐.  

---

## 5️⃣ 컴포넌트 설계 패턴 🎨  

### 🧩 **Atomic Design Pattern (원자적 디자인 패턴)**  
✔ **Atoms (원자)** – 가장 작은 UI 요소 (버튼, 입력 필드).  
✔ **Molecules (분자)** – 여러 원자로 구성된 작은 UI 조각 (입력 필드 + 버튼 조합).  
✔ **Organisms (유기체)** – 여러 분자로 구성된 복잡한 UI 블록 (네비게이션 바, 카드 리스트).  

---

## 6️⃣ React에서 라우팅 처리 🚦  

### 🛣 **클라이언트 사이드 라우팅**  
✔ **React Router** – SPA(Single Page Application)에서 페이지 이동을 처리하는 표준 라이브러리.  
✔ **Next.js 라우팅** – 파일 기반 라우팅 시스템으로, SEO 및 성능 최적화 가능.  

---

## 7️⃣ 추가적으로 알아두면 좋은 개념 🎯  
🔹 **서버 컴포넌트(Server Components)와 클라이언트 컴포넌트(Client Components)**  
🔹 **SSR(서버 사이드 렌더링) vs CSR(클라이언트 사이드 렌더링) vs SSG(정적 사이트 생성)**  
🔹 **React에서 성능 최적화 기법 (Memoization, Code Splitting, Lazy Loading)**  
🔹 **React Native – 모바일 앱 개발에 React 활용**  

---

## 🚀 마무리  
이제 React의 기본 개념과 학습 방향을 알게 되었습니다!  
다음 단계로는 직접 **프로젝트를 만들어보고** 경험을 쌓는 것이 중요합니다.  
🔹 **작은 프로젝트부터 시작하여 점차 복잡한 개념을 적용해 보세요!**  

---

### 🔥 **React 학습 추천 자료**  
📌 공식 문서: [https://react.dev](https://react.dev)  
📌 Vite 프로젝트 시작하기: [https://vitejs.dev](https://vitejs.dev)  
📌 Next.js 공식 문서: [https://nextjs.org](https://nextjs.org)