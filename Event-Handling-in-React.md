# 📘 Event Handling in React

Event handling in React refers to how React captures and processes user interactions such as clicks, typing, scrolling, form submissions, and more.

React uses its own Synthetic Event System, which provides a consistent, cross-browser way to handle events efficiently.

## ⚡ React’s Synthetic Event System

React does not use native DOM events directly. Instead, it wraps events inside a SyntheticEvent object that provides:

✔ Cross-browser consistency
✔ Performance optimizations
✔ Unified event API

## 🚀 How React Handles Events Internally

## React does not attach event listeners to each element. Instead:

✔ 1. A single event listener is attached at the root (React 17+)
✔ 2. All events bubble up to the root listener
✔ 3. React identifies the target component and invokes its handler

This approach:

Reduces memory usage

Improves event delegation

Makes React faster and more scalable

### 🎯 Passing Data to Event Handlers in React

In real applications, you often need to pass custom data (like id, index, name, or objects) to event handlers.

However, this does not work:
```
<button onClick={handleClick(id)}>Click</button>  
// ❌ This executes handleClick immediately
```

React needs a function reference, not a function call.

## ✅ Correct Ways to Pass Data to Event Handlers
## 1️⃣ Using Inline Arrow Function (Most Common)
```
<button onClick={() => handleClick(id)}>Click</button>
```
Why is this correct?

() => handleClick(id) is a new function

It runs only when clicked

It allows passing arguments easily

It is the most commonly used pattern

Example:
```
function App() {
  const handleClick = (id) => {
    console.log("Clicked item:", id);
  };

  return (
    <button onClick={() => handleClick(42)}>Click Me</button>
  );
}
```
## 2️⃣ Passing Both Event & Custom Data

Sometimes you need the event object and your custom argument:
```
<button onClick={(event) => handleClick(event, id)}>Click</button>
```
```
Example:

function handleClick(event, id) {
  console.log(event.type); // "click"
  console.log(id);         // 10
}

<button onClick={(e) => handleClick(e, 10)}>Click</button>

```

✔ React always passes the event first
✔ You can add custom arguments afterward

📌 Summary

React event handling is built for:

Performance (single root listener)

Consistency (SyntheticEvent)

Flexibility (easy to pass data)
