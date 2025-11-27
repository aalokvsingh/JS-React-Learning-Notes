# 📦 Code-Splitting & Lazy Loading in React

Modern React applications can grow large, and loading the entire bundle at once slows down performance. **Code-splitting** and **lazy loading** solve this by loading only what is needed, when it is needed.

This README explains:

* What code-splitting is
* What lazy loading is
* Why they matter
* How React implements them
* Examples and best practices

---

# 🚀 What is Code-Splitting?

**Code-splitting** is the process of breaking your JavaScript bundle into smaller chunks that can be loaded on demand.

React apps built with Webpack, Vite, or CRA generate **one large bundle** by default. Code-splitting helps avoid loading unused code upfront.

### 🔥 Why Code-Splitting?

* Reduces initial load time
* Loads only what is needed for the current page
* Improves performance in large apps
* Better user experience

### 🧠 How React Enables Code-Splitting

React uses **dynamic imports** to split code:

```js
import('./MyComponent')
```

Each dynamic import creates a **separate bundle chunk**.

---

# 💤 What is Lazy Loading?

**Lazy loading** means loading a component or module only when it is required.

React supports lazy loading using:

* `React.lazy()`
* `Suspense`

### 🔍 Example

Instead of importing normally:

```js
import About from './About';
```

Use lazy loading:

```js
const About = React.lazy(() => import('./About'));
```

React loads the `About` component **only when rendered**.

---

# 🧷 React.lazy(): Lazy Loading Components

### ✔ Basic Usage

```jsx
import React, { Suspense } from 'react';

const Dashboard = React.lazy(() => import('./Dashboard'));

function App() {
  return (
    <Suspense fallback={<h2>Loading...</h2>}>
      <Dashboard />
    </Suspense>
  );
}

export default App;
```

### Key Points

* `React.lazy()` must return a **Promise** that resolves to a module with a `default` export.
* Components must be wrapped inside `<Suspense>`.
* `fallback` renders during loading.

🔍 What happens behind the scenes?

React sees React.lazy(() => import('./Dashboard'))

It creates a separate JS chunk for Dashboard

The chunk loads only when Dashboard is rendered

Until then, Suspense shows the fallback UI
---

# 🧩 Route-Based Code Splitting

Perfect for large applications.

### Using `react-router`

```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import React, { Suspense } from 'react';

const Home = React.lazy(() => import('./pages/Home'));
const Profile = React.lazy(() => import('./pages/Profile'));

export default function App() {
  return (
    <BrowserRouter>
      <Suspense fallback={<div>Loading page...</div>}>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/profile" element={<Profile />} />
        </Routes>
      </Suspense>
    </BrowserRouter>
  );
}
```
This is the most common real-world use case.
This loads each route **only when the user navigates to it**.

---

# 🛠 Advanced: Splitting by Interaction

Sometimes you want to lazy load based on user interaction.

```jsx
const Settings = React.lazy(() => import('./Settings'));

function App() {
  const [open, setOpen] = useState(false);

  return (
    <div>
      <button onClick={() => setOpen(true)}>Open Settings</button>

      {open && (
        <Suspense fallback={<p>Loading settings...</p>}>
          <Settings />
        </Suspense>
      )}
    </div>
  );
}
```

This avoids loading Settings until the user wants it.

---

# ⚡ Best Practices for Code-Splitting & Lazy Loading

### ✔ Split at Route Level

Most effective and common.

### ✔ Split Large Components

Tables, charts, dashboards, editors…

### ✔ Provide Meaningful Fallbacks

Loaders, skeletons, shimmer UI.

### ✔ Avoid Over-Splitting

Too many small chunks → too many network requests.

### ✔ Combine with Performance Tools

* React.memo
* useMemo
* useCallback
* React.Suspense + SuspenseList

---

# 🧠 Summary

| Concept            | Meaning                                      |
| ------------------ | -------------------------------------------- |
| **Code-splitting** | Breaking your JS bundle into chunks          |
| **Lazy loading**   | Loading chunks only when needed              |
| **React.lazy()**   | Built-in way to lazy load components         |
| **Suspense**       | Shows fallback UI while lazy component loads |

---

# 📚 Final Example (Complete)

```jsx
import React, { Suspense } from 'react';

const Reports = React.lazy(() => import('./Reports'));

function App() {
  return (
    <Suspense fallback={<div>Loading Reports...</div>}>
      <Reports />
    </Suspense>
  );
}

export default App;
```

This is the simplest full setup of **code-splitting + lazy loading**.

---

