# 📘 03. 커스텀 훅 만들기 & 활용

## 🧠 목표

- 재사용 가능한 커스텀 훅(Custom Hook)을 설계하고 사용한다.
- 로직 분리와 관심사의 분리를 통해 코드 유지보수성을 높인다.

---

## 📌 주요 개념

### 1. 커스텀 훅이란?

- 여러 컴포넌트에서 중복되는 **로직을 추상화한 함수**
- `use`로 시작해야 하며 내부에서 **React 훅을 사용할 수 있음**

```tsx
function useCustomHook() {
  const [state, setState] = useState();
  useEffect(() => { ... }, []);
  return { state, setState };
}
```

---

## 🧪 실습 예제: 사용자 정보 가져오는 훅 만들기

### 🎯 목표

- API를 통해 사용자 정보를 가져오고 컴포넌트에서 재사용하기

### 💻 예제 코드

```tsx
// hooks/useFetchUserProfile.ts
import { useEffect, useState } from "react";
import { fetchUser } from "@/lib/api/user";
import { IUser } from "@/lib/model/user";

export function useFetchUserProfile() {
  const [user, setUser] = useState<IUser | null>(null);

  useEffect(() => {
    fetchUser().then(setUser);
  }, []);

  return { user };
}
```

```tsx
// 사용 예시
import { useFetchUserProfile } from "@/hooks/useFetchUserProfile";

export default function ProfileBox() {
  const { user } = useFetchUserProfile();

  return <div>{user ? `안녕하세요, ${user.name}님` : "로딩 중..."}</div>;
}
```

---

## 📝 연습 과제

- 사용자 정보 외에 **다른 공통 API 호출 훅**을 만들어 보세요. (ex: useFetchPosts)
- `isLoading` 상태를 포함하도록 커스텀 훅을 개선해 보세요.

---

## 🔚 다음 단계

[04-useRef-pagination](../04-useRef-pagination/README.md)
