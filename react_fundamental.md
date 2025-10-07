# React Fundamentals

## 🧠 Overview
React is a **JavaScript library** for building dynamic user interfaces.  
It uses a **declarative** and **component-based** approach to create reusable UI blocks that update efficiently.

---

## ⚙️ Core Concepts

### JSX
JSX lets you write HTML-like syntax inside JavaScript.
```jsx
const name = "Chon";
export default function Hello() {
  return <h1>Hello, {name}!</h1>;
}
```
✅ Must return **one root element**.  
✅ You can use fragments: `<>...</>` to avoid extra wrappers.

---

### Components
Two main types:
1. **Function Components** (modern standard)
2. **Class Components** (legacy / still used in some codebases)

```jsx
function Button({ label }) {
  return <button>{label}</button>;
}
```
Props are **read-only**:
```jsx
function Avatar({ src, alt = "User Avatar" }) {
  return <img src={src} alt={alt} />;
}
```

---

### State & Events
Use `useState` to store local state.
```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(c => c + 1)}>{count}</button>;
}
```
⚡ State updates are asynchronous and batched.  
Use **functional updates** if the next state depends on the previous one.

---

### Lists & Keys
```jsx
const todos = [{ id: 1, text: "Learn React" }];

<ul>
  {todos.map(todo => <li key={todo.id}>{todo.text}</li>)}
</ul>
```
🧩 **Keys** must be unique and stable.

---

### Conditional Rendering
```jsx
{isLoading ? <Spinner /> : <Data />}
{error && <p role="alert">{error.message}</p>}
```

---

## 🔄 React Hooks (Core)

### `useState`
Keeps track of local state.

### `useEffect`
Performs **side effects** such as data fetching or DOM updates.
```jsx
useEffect(() => {
  document.title = `Count: ${count}`;
  return () => console.log("Cleanup");
}, [count]);
```

### `useRef`
Stores mutable values that don’t trigger re-renders.
```jsx
const inputRef = useRef(null);
<input ref={inputRef} />;
```

### `useMemo` & `useCallback`
Optimize performance by memoizing computations or functions.
```jsx
const total = useMemo(() => heavyCalc(items), [items]);
const handleClick = useCallback(() => doThing(id), [id]);
```

### `useContext`
Share data globally without prop drilling.
```jsx
const ThemeContext = createContext("light");
function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Child />
    </ThemeContext.Provider>
  );
}
```

### Custom Hook Example
```jsx
function useToggle(initial = false) {
  const [on, setOn] = useState(initial);
  const toggle = useCallback(() => setOn(o => !o), []);
  return { on, toggle };
}
```

---

## ✍️ Forms (Controlled Components)
```jsx
const [form, setForm] = useState({ email: "" });

<input
  value={form.email}
  onChange={e => setForm({ ...form, email: e.target.value })}
/>
```
React controls the input via state — known as **controlled inputs**.

---

## 🌐 Data Fetching
```jsx
function Users() {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    (async () => {
      const res = await fetch("/api/users");
      const json = await res.json();
      setData(json);
      setLoading(false);
    })();
  }, []);

  if (loading) return <p>Loading...</p>;
  return <ul>{data.map(u => <li key={u.id}>{u.name}</li>)}</ul>;
}
```

---

## 🧩 Composition Over Inheritance
Use **composition** (children props) to build flexible UIs.
```jsx
function Card({ title, children }) {
  return (
    <div className="card">
      <h3>{title}</h3>
      {children}
    </div>
  );
}
```

---

## 🧭 Routing (React Router)
```bash
npm i react-router-dom
```
```jsx
import { createBrowserRouter, RouterProvider } from "react-router-dom";

const router = createBrowserRouter([
  { path: "/", element: <Home /> },
  { path: "/about", element: <About /> },
]);

export default function App() {
  return <RouterProvider router={router} />;
}
```

---

## 🧱 Error Boundaries
Error boundaries catch runtime errors in child components.
```jsx
class Boundary extends React.Component {
  state = { hasError: false };
  static getDerivedStateFromError() {
    return { hasError: true };
  }
  render() {
    return this.state.hasError ? <p>Something went wrong.</p> : this.props.children;
  }
}
```

---

## ⚡ Performance Tips
- Split bundles with `React.lazy` + `<Suspense>`.
- Memoize components using `React.memo`.
- Keep state **local** to where it’s needed.
- Stabilize props/functions with `useMemo` and `useCallback`.

---

## 🧰 Setup with Vite
```bash
npm create vite@latest my-app -- --template react
cd my-app
npm install
npm run dev
```
Node.js LTS is recommended.

📂 Folder structure:
```
src/
  App.jsx
  main.jsx
  components/
  hooks/
  pages/
  styles/
```

---

## 🧪 Testing (with Vitest + RTL)
```bash
npm i -D vitest @testing-library/react @testing-library/user-event jsdom
```
```jsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import Button from "./Button";

test("increments", async () => {
  render(<Button />);
  await userEvent.click(screen.getByRole("button"));
  expect(screen.getByRole("button")).toHaveTextContent("1");
});
```

---

## ⚠️ Common Mistakes
- ❌ Mutating state directly.
- ❌ Using array index as key.
- ❌ Forgetting cleanup in `useEffect`.
- ❌ Global context overuse.

---

## ✅ Practice Checklist
- [ ] Build a counter using `useState`.
- [ ] Create a form with validation.
- [ ] Fetch data from an API.
- [ ] Add routing between two pages.
- [ ] Implement a custom hook.

---

## 📚 References
- [React Official Docs – react.dev](https://react.dev/learn)
- [React Router – reactrouter.com](https://reactrouter.com/en/main)
- [Vite – vitejs.dev](https://vitejs.dev/guide/)
- [React Testing Library – testing-library.com](https://testing-library.com/docs/react-testing-library/intro/)
- [MDN – JSX Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/JSX)
- [Kent C. Dodds – Advanced React Patterns](https://kentcdodds.com/blog)

---
