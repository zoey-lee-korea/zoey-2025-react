# 📘 06. 데이터 Fetch 및 비동기 흐름 처리

## 🧠 목표

- API 요청 시의 비동기 흐름과 상태 변경 로직을 이해한다.
- `fetch`, `async/await`, `Promise`, `try/catch` 흐름을 실습한다.

---

## 📌 주요 개념

### 1. fetch와 async/await 기본 구조

```tsx
const fetchData = async () => {
  try {
    const res = await fetch("/api/example");
    const data = await res.json();
    setData(data);
  } catch (error) {
    console.error(error);
  }
};
```

### 2. 상태 기반 로딩 처리

```tsx
const [isLoading, setIsLoading] = useState(false);

useEffect(() => {
  setIsLoading(true);
  fetchData().finally(() => setIsLoading(false));
}, []);
```

---

## 🧪 실습 예제: 댓글 목록 불러오기

### 🎯 목표

- API 호출 → 응답 확인 → 상태 업데이트 → 에러 처리까지 전체 흐름 체험

### 💻 예제 코드

```tsx
import { useEffect, useState } from "react";

export default function CommentList() {
  const [comments, setComments] = useState([]);
  const [isLoading, setIsLoading] = useState(false);

  const fetchComments = async () => {
    try {
      setIsLoading(true);
      const res = await fetch("/api/comments");
      const data = await res.json();
      setComments(data);
    } catch (err) {
      console.error("에러 발생:", err);
    } finally {
      setIsLoading(false);
    }
  };

  useEffect(() => {
    fetchComments();
  }, []);

  return (
    <div>
      {isLoading ? (
        <p>로딩 중...</p>
      ) : (
        comments.map((c) => <p key={c.id}>{c.text}</p>)
      )}
    </div>
  );
}
```

---

## 📝 연습 과제

- 실패 시 사용자에게 alert로 오류 메시지를 보여주는 로직을 추가해보세요.
- 데이터가 없는 경우 "댓글이 없습니다" 메시지를 조건부로 표시해보세요.

---

## 🔚 다음 단계

[07-autoresizing-textarea](../07-autoresizing-textarea/README.md)
