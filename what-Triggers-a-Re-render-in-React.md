# ⭐ What Triggers a Re-render in React?

React re-renders a component when its state changes, its props change, its parent re-renders, or when context/store values change.
Refs and regular variables do NOT trigger re-renders because they are not reactive.

### ✅ 1. State Change (useState / useReducer)
### ✅ 2. Props Change
### ✅ 3. Parent Component Re-renders
### ✅ 4. Context Value Change (useContext)

### 🟡 Optional Triggers (Less Common)
### ✔ 5. Redux/Zustand/MobX Store Update

Subscribed components re-render when the store value they depend on changes.

### ✔ 6. forceUpdate (Class Components)

Rare and discouraged, but still a trigger.
