# 📘 08. Zustand를 이용한 전역 상태 관리

## 🧠 목표

- React 프로젝트에서 상태를 전역으로 공유하기 위해 Zustand를 사용할 수 있다.
- 전역 상태의 정의, 사용, 갱신 흐름을 이해한다.

---

## 📌 주요 개념

### 1. Zustand란?

- Redux보다 가볍고 단순한 상태 관리 라이브러리
- 글로벌 상태 선언 → 훅으로 접근 가능

```bash
npm install zustand
```

### 2. store 정의 예시

```tsx
import { create } from "zustand";

interface UserStore {
  user: { name: string } | null;
  setUser: (user: { name: string }) => void;
}

export const useUserStore = create<UserStore>((set) => ({
  user: null,
  setUser: (user) => set({ user }),
}));
```

---

## 🧪 실습 예제: 사용자 상태 공유하기

### 🎯 목표

- 로그인 후 받아온 사용자 정보를 모든 컴포넌트에서 공유하도록 구현

### 💻 예제 코드

```tsx
// 로그인 후 user 저장
const { setUser } = useUserStore();
setUser({ name: "홍길동" });

// 다른 곳에서 user 가져오기
const { user } = useUserStore();

return <p>안녕하세요, {user?.name}님</p>;
```

---

## 📝 연습 과제

- 로그아웃 기능을 구현하여 user 값을 null로 리셋해보세요.
- Zustand로 다크모드 상태도 추가해보세요 (`isDarkMode`)

---

## 🔚 마무리

이로써 모든 실습이 완료되었습니다.  
이후엔 실무 프로젝트 구조를 다시 탐색하며, 배운 개념이 어떻게 사용되고 있는지를 직접 찾아보세요 👀
