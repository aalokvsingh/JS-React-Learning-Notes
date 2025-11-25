# ⭐ How React Fiber Changes Rendering and Scheduling

React Fiber is a complete rewrite of React’s reconciliation engine (introduced in React 16) that fundamentally changes how React handles rendering.

## Its goal is to make rendering:

Interruptible

Priority-based

Chunked into smaller units

Recoverable

More responsive to user interactions

### Before Fiber (React <16):
➡ Rendering was synchronous, blocking, and non-interruptible.

### After Fiber:
➡ Rendering is asynchronous, interruptible, and priority-driven.

🧵 1. Fiber breaks rendering into small “units of work”

### Before Fiber:
React rendered the entire component tree in one go.

If rendering took 200ms, the UI would freeze for 200ms. ❌

### With Fiber:
React breaks the rendering work into tiny chunks called fibers.

Each component = one fiber node.

```App
 ├── Header
 ├── Dashboard
 │     ├── Chart
 │     ├── Table
 └── Footer
```

### React processes each node one by one, like stepping through a linked list.

✔ Rendering is now incremental
✔ React can pause after each step

🛑 2. Rendering is now interruptible

Thanks to Fiber, React can stop rendering in the middle.

Example:

React is rendering a large list.

User types in an input.

React immediately pauses the long render, processes the input, then resumes.

This makes the UI much smoother.

### 🌟 This feature is called Cooperative Scheduling.

⏳ 3. Scheduling with Priorities

Fiber assigns a priority level to each update:

Priority	Example
```
🟥 High:	Typing, click, input changes
🟧 Medium:	Updating visible components
🟩 Low:	Background data fetching, invisible components
```

React will always process high-priority work first.

If a low-priority render is happening, React can:

✔ pause it
✔ run the urgent update
✔ resume later

## 🔁 4. New Rendering Flow: Render Phase and Commit Phase

Fiber splits the render cycle into two phases:

### 🧠 Render Phase (Reconciliation)

Compute changes

Compare Virtual DOM trees

Build the effects list

Can be:

⏸ paused

🧨 aborted

🔁 restarted

❌ No DOM updates happen here.

### 🛠 Commit Phase

Apply changes to real DOM

Run layout effects

Paint the UI

This phase:
✔ Is very fast
✔ Cannot be interrupted

🧩 5. Fiber enables Concurrent Rendering



### 📄 6. Fiber Data Structure (Key Innovation)

Fiber nodes store:

state

props

pending updates

priority

return pointer (parent)

sibling pointer

child pointer

effect list

This structure allows React to:

✔ Walk the tree efficiently
✔ Pause and resume work
✔ Reuse work from previous renders


## 🧠 Summary in One Sentence (Interview Gold)
```
React Fiber makes rendering interruptible, incremental, and priority-based by breaking the component tree into small units of work called fibers, enabling smoother UI, concurrent features, and responsive scheduling.
```
