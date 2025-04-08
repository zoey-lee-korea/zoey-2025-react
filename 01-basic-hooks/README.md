# 📘 01. 기본 훅 학습 (useState, useEffect, useRef)

## 🧠 목표

- React의 기본 훅인 `useState`, `useEffect`, `useRef`를 이해하고 사용할 수 있다.
- 컴포넌트 렌더링 흐름과 상태 변화에 따른 UI 변경을 체험한다.

---

## 📌 주요 개념

### 1. useState

- 컴포넌트의 **상태를 저장하고 갱신**하기 위한 훅
- 상태 변경 시 컴포넌트가 **자동으로 리렌더링**됨

```tsx
const [count, setCount] = useState(0);
```

### 2. useEffect

- 컴포넌트의 **사이드 이펙트(부수효과)**를 처리하는 훅
- 예: 데이터 가져오기, 이벤트 등록, 타이머 등

```tsx
useEffect(() => {
  console.log("컴포넌트가 마운트됨");
}, []); // 의존성 배열이 빈 경우 한 번만 실행
```

### 3. useRef

- 컴포넌트 내부에서 **값을 기억**하거나 **DOM에 접근**할 때 사용
- 변경해도 렌더링이 발생하지 않음

```tsx
const inputRef = useRef<HTMLInputElement>(null);

useEffect(() => {
  inputRef.current?.focus();
}, []);
```

---

## 🧪 실습 예제

### 🎯 목표: 댓글 입력창 show/hide + 자동 포커스

### 💻 예제 코드

```tsx
import { useState, useRef, useEffect } from "react";

export default function CommentToggle() {
  const [showInput, setShowInput] = useState(false);
  const inputRef = useRef<HTMLInputElement>(null);

  useEffect(() => {
    if (showInput) inputRef.current?.focus();
  }, [showInput]);

  return (
    <div>
      <button onClick={() => setShowInput(!showInput)}>
        {showInput ? "숨기기" : "댓글 달기"}
      </button>

      {showInput && (
        <input
          ref={inputRef}
          type="text"
          placeholder="댓글을 입력하세요"
          style={{ marginTop: "10px" }}
        />
      )}
    </div>
  );
}
```

### ✅ 실습 포인트

- `useState`로 댓글 입력창의 열림 여부 관리
- `useRef`로 입력창 DOM에 접근
- `useEffect`로 상태 변화 시 자동 포커스 처리

---

## 📝 연습 과제

- 입력창에 텍스트가 입력될 때마다 실시간으로 하단에 보여주도록 해보세요.
- 버튼 문구를 `댓글 입력 취소` ↔ `댓글 입력하기`로 바꿔보세요.

---

## 🔚 다음 단계

[02-useEffect-patterns](../02-useEffect-patterns/README.md)
