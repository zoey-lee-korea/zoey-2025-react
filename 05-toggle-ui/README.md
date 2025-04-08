# 📘 05. UI 토글 & 조건부 렌더링

## 🧠 목표

- `useState`를 통해 상태에 따라 컴포넌트를 조건부로 렌더링할 수 있다.
- 모달, 스위치, 버튼 등 토글 가능한 UI를 구현할 수 있다.

---

## 📌 주요 개념

### 1. 조건부 렌더링

- 특정 상태에 따라 JSX를 보여줄지 말지를 결정

```tsx
{
  isOpen && <Modal />;
}
```

### 2. toggle 함수 만들기

- 상태를 반전시키는 패턴

```tsx
const toggle = () => setOpen((prev) => !prev);
```

---

## 🧪 실습 예제: 댓글 삭제 확인 모달

### 🎯 목표

- "삭제" 버튼 클릭 시 모달이 열리고, 확인을 누르면 삭제 로직 수행

### 💻 예제 코드

```tsx
import { useState } from "react";

export default function DeleteConfirm() {
  const [showConfirm, setShowConfirm] = useState(false);

  const handleDelete = () => {
    alert("삭제되었습니다!");
    setShowConfirm(false);
  };

  return (
    <div>
      <button onClick={() => setShowConfirm(true)}>삭제</button>

      {showConfirm && (
        <div className="modal">
          <p>정말 삭제하시겠습니까?</p>
          <button onClick={handleDelete}>확인</button>
          <button onClick={() => setShowConfirm(false)}>취소</button>
        </div>
      )}
    </div>
  );
}
```

---

## 📝 연습 과제

- 모달을 컴포넌트로 분리해보세요 (props로 메시지와 이벤트 전달)
- 버튼 문구를 `삭제 요청` ↔ `취소`로 토글되도록 구현해보세요

---

## 🔚 다음 단계

[06-fetch-data](../06-fetch-data/README.md)
