# 📘 07. AutoResizingTextarea 컴포넌트 실습

## 🧠 목표

- 사용자 입력에 따라 크기가 자동으로 조절되는 textarea 컴포넌트를 사용한다.
- props로 입력 상태와 이벤트 핸들러를 전달하여 제어한다.

---

## 📌 주요 개념

### 1. AutoResizingTextarea의 역할

- 입력 길이에 따라 textarea 높이를 자동 조절
- 외부 상태(inputValue)와 입력 이벤트(handleInputChange)를 props로 받음

---

## 🧪 실습 예제: 댓글 입력 컴포넌트 구현

### 🎯 목표

- 입력값 상태를 부모에서 관리하고, textarea 컴포넌트는 재사용 가능하게 분리

### 💻 예제 코드

```tsx
// components/AutoResizingTextarea.tsx
import React from "react";

type Props = {
  placeholder: string;
  handleInputChange: (e: React.ChangeEvent<HTMLTextAreaElement>) => void;
  inputValue: string;
};

export default function AutoResizingTextarea({
  placeholder,
  handleInputChange,
  inputValue,
}: Props) {
  return (
    <textarea
      className="resize-none overflow-hidden"
      placeholder={placeholder}
      value={inputValue}
      onChange={handleInputChange}
      rows={1}
      style={{ width: "100%", minHeight: "38px" }}
    />
  );
}
```

```tsx
// 사용 예시
import { useState } from "react";
import AutoResizingTextarea from "@/components/AutoResizingTextarea";

export default function CommentInput() {
  const [inputValue, setInputValue] = useState("");

  const handleInputChange = (e: React.ChangeEvent<HTMLTextAreaElement>) => {
    setInputValue(e.target.value);
  };

  return (
    <div className="border p-4 rounded">
      <AutoResizingTextarea
        placeholder="댓글을 입력하세요"
        inputValue={inputValue}
        handleInputChange={handleInputChange}
      />
    </div>
  );
}
```

---

## 📝 연습 과제

- 입력값이 있을 때만 "등록" 버튼이 활성화되도록 구현해보세요.
- 글자 수 제한을 걸고, 제한 초과 시 경고 메시지를 띄워보세요.

---

## 🔚 다음 단계

[08-zustand-store](../08-zustand-store/README.md)
