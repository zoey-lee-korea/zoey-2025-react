# 📘 04. useRef를 활용한 페이징 처리

## 🧠 목표

- `useRef`를 통해 페이지 상태를 저장하고, 무한스크롤과 같은 상황에서 활용할 수 있다.
- 렌더링과 관계없는 변수 관리 방식 이해

---

## 📌 주요 개념

### 1. useRef는 어떤 값이든 저장 가능

- 렌더링과 무관하게 변경되는 값을 추적할 때 유용함
- 렌더링을 유발하지 않음

```tsx
const pageRef = useRef(1); // 페이지 번호 저장용
```

### 2. IntersectionObserver와 함께 사용

- 특정 요소가 보일 때 **자동으로 다음 페이지를 호출**하는 구조 구현 가능

---

## 🧪 실습 예제: 댓글 무한 스크롤

### 🎯 목표

- 하단 요소가 보일 때마다 다음 페이지의 댓글 목록을 불러오기

### 💻 예제 코드

```tsx
const pageRef = useRef(1);
const loaderRef = useRef(null);
const [comments, setComments] = useState([]);

useEffect(() => {
  const observer = new IntersectionObserver((entries) => {
    if (entries[0].isIntersecting) {
      pageRef.current += 1;
      fetchData(pageRef.current);
    }
  });

  if (loaderRef.current) observer.observe(loaderRef.current);
  return () => observer.disconnect();
}, []);

const fetchData = async (page: number) => {
  const res = await fetch(`/api/comments?page=${page}`);
  const data = await res.json();
  setComments((prev) => [...prev, ...data]);
};
```

```tsx
{
  /* 렌더링 파트 */
}
{
  comments.map((c) => <div key={c.id}>{c.text}</div>);
}
<div ref={loaderRef}>⬇️ 더 보기</div>;
```

---

## 📝 연습 과제

- 댓글 수가 적을 땐 observer가 작동하지 않게 조건을 추가해 보세요.
- `useState`와 `useRef`를 비교하는 주석을 추가해보세요.

---

## 🔚 다음 단계

[05-toggle-ui](../05-toggle-ui/README.md)
