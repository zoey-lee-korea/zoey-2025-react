# 🌱 React 실전 커리큘럼 for 실무 입문자

## 👨‍🏫 목적
- 실무 프로젝트에 적응할 수 있도록 React의 상태 관리, 훅 사용, 컴포넌트 구조 등을 학습
- 프로젝트 내 사용 컴포넌트와 기능을 중심으로 실습 위주의 학습을 유도
- 실전에서 마주치는 복잡한 훅 흐름, 비동기 처리, 상태 공유 등에 익숙해지기

---

## 🧱 커리큘럼 구성

각 단계는 개념 설명 + 실습 예제를 포함하고 있으며, **선행 → 후행 순서**로 학습할 수 있도록 설계되었습니다.

---

## 📘 1단계: React 상태와 기본 훅 이해

- 주요 개념: `useState`, `useEffect`, `useRef`
- 컴포넌트 렌더링 흐름 및 상태 업데이트 방식 숙지

### ✅ 실습 예제
> 댓글 입력창 show/hide 토글 + 입력 시 focus 처리

```tsx
const [showInput, setShowInput] = useState(false);
const inputRef = useRef();

useEffect(() => {
  if (showInput) inputRef.current?.focus();
}, [showInput]);
