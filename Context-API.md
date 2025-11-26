# React Context API – Simple Explanation with Example

## 🟦 What is the Context API?

The **React Context API** is a built-in way to share data across your component tree **without passing props manually** at every level.

You create:

* a **Context** (like a storage box) and
* wrap your components with a **Provider** that gives the value
* then any component inside can read that value using `useContext()`

It helps avoid **"prop drilling"**, especially when multiple components need the same data.

---

## ✅ When to Use Context API

Use Context when your application is **small or medium** and when you want to share simple global values such as:

* logged-in user info
* theme (light/dark)
* selected language

It's great when the shared state is:

* **simple**
* **not updated frequently**
* **used across many levels of the component tree**

---

## ❌ When *Not* to Use Context

Avoid Context API when:

* **many components consume the same state** → because every update causes **re-renders** across all consumers
* state becomes **big or complex**
* you need **performance optimization** or **scalable global state management** (e.g., use Redux/Zustand instead)

---

## 🛠 Example Use Cases

* Current logged-in user data
* Light / Dark theme
* Selected language (English/Hindi)

These values rarely change and must be available everywhere.

---

## 📘 Simple Example

Here’s the most basic example of using Context to share a theme value:

```jsx
import { createContext, useContext } from "react";

const ThemeContext = createContext();

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Home />
    </ThemeContext.Provider>
  );
}

function Home() {
  const theme = useContext(ThemeContext);
  return <p>Theme is: {theme}</p>;
}
```

### 🔍 What’s happening here?

1. `createContext()` → creates a storage box for the theme
2. `<Provider value="dark">` → gives the value to all children
3. `useContext(ThemeContext)` → reads the value inside `Home`

No props passed. No drilling. Simple.

