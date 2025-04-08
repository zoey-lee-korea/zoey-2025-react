# 📘 02. useEffect 패턴 익히기

## 🧠 목표

- 다양한 상황에서의 `useEffect` 사용법을 익힌다.
- 의존성 배열에 따라 동작이 어떻게 달라지는지 체험한다.

---

## 📌 주요 개념

### 1. 의존성 배열에 따른 실행 시점

```tsx
useEffect(() => {
  // 항상 실행됨
});

useEffect(() => {
  // 최초 한 번 실행됨 (마운트 시)
}, []);

useEffect(() => {
  // 특정 상태가 변경될 때만 실행됨
}, [value]);
```

### 2. 조건부 렌더링 및 버튼 상태 제어

- 여러 상태를 조합하여 특정 조건이 만족될 때만 실행

---

## 🧪 실습 예제 1: 버튼 활성화 조건

### 🎯 목표

- 입력값에 따라 버튼을 활성화/비활성화

### 💻 코드 예시

```tsx
import { useEffect, useState } from "react";

export default function SubmitForm() {
  const [title, setTitle] = useState("");
  const [desc, setDesc] = useState("");
  const [isAbleSubmit, setIsAbleSubmit] = useState(false);
  const [isEnable, setIsEnable] = useState(false);

  useEffect(() => {
    if (title && desc && isAbleSubmit) {
      setIsEnable(true);
    } else {
      setIsEnable(false);
    }
  }, [title, desc, isAbleSubmit]);

  return (
    <div>
      <input
        placeholder="제목"
        value={title}
        onChange={(e) => setTitle(e.target.value)}
      />
      <input
        placeholder="내용"
        value={desc}
        onChange={(e) => setDesc(e.target.value)}
      />

      <label>
        <input
          type="checkbox"
          onChange={(e) => setIsAbleSubmit(e.target.checked)}
        />
        제출 가능 여부
      </label>

      <button disabled={!isEnable}>제출</button>
    </div>
  );
}
```

---

## 🧪 실습 예제 2: 스크롤 로딩 트리거

### 🎯 목표

- 특정 요소가 화면에 보일 때 API 호출하도록 트리거 구현

### 💻 코드 예시

```tsx
useEffect(() => {
  const observer = new IntersectionObserver((entries) => {
    if (entries[0].isIntersecting) {
      console.log("로딩 영역 감지됨!");
      // fetchData 호출 등
    }
  });

  const target = document.querySelector("#load-target");
  if (target) observer.observe(target);

  return () => observer.disconnect();
}, []);
```

```tsx
<div style={{ height: '150vh' }} />
<div id="load-target">⬇️ 여기에 닿으면 API 호출</div>
```

---

## 📝 연습 과제

- 입력값이 일정 글자 수 이상일 때만 버튼이 활성화되도록 조건을 바꿔보세요.
- 스크롤 대신 버튼을 눌렀을 때 `IntersectionObserver`와 동일한 로직을 수동 호출하도록 바꿔보세요.

---

## 🔚 다음 단계

[03-custom-hooks](../03-custom-hooks/README.md)
