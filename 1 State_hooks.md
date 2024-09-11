# Hooks ek React-dom ka package hn,

- ### ye sirf web applications ke liye banaye gaye hain jo browser ke DOM (Document Object Model) environment me run karte hain.

    <hr>

- ### Ye hooks mobile applications, jaise iOS, Android, ya Windows applications me supported nahi hote kyunki wo browser environment ke bahar hain.

    <hr>

- ### Browser ke ilawa dusre environments ke liye aapko alag libraries use karni padti hain, jaise React Native jo mobile apps ke liye hota hai.

    <hr><br>

### Hooks aapko React components me mukhtalif features use karne dete hain.

### Aap ya to built-in Hooks ka use kar sakte hain ya inko mila ke apne custom Hooks bana sakte hain.

# Types

- ## State Hooks

  - ### State Hooks component ko kisi information ko read aur update karny lye me madad karte hain

  - ### jaise user ka input. e.g, form component input value ko store karne ke liye state ka use kar sakta hai, aur ek image gallery selected image ko track karne ke liye, etc.

<br>

# 2 Types ky State Hooks hn

- ## 1 useState

- ## 2 useReducer

# useState

- ### Simple state ke liye best.

- ## Syntax

```
const [value, setValue] = useState(initialValue);
```

- ### value me data ki value assign ki jati hn

- ### setValue function hota hn to value ko update karta hn

# Example

```javascript
// ./components/1_state_Hook.js

import { useState } from "react";

export default function US_ST() {
  const initialState = { count: 0, step: 1 };
  const [value, setCount] = useState(initialState);

  return (
    <div>
      <p> -> Count: {value.count}</p>
      <p> -> Step: {value.step}</p>

      <button
        onClick={() =>
          setCount({ count: value.count + value.step, step: value.step })
        }
      >
        Increment
      </button>

      <button
        onClick={() =>
          setCount({ count: value.count - value.step, step: value.step })
        }
      >
        Decrement
      </button>

      <br />

      <label htmlFor="step">Step</label>

      <input
        type="text"
        id="step"
        onChange={(e) =>
          setCount({ count: value.count, step: parseInt(e.target.value) || 1 })
        }
      />
    </div>
  );
}
```

# Preview

<a href=https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/1_usestate.gif target="_blank">Click Here Preview</a>

Yeh code ek simple counter component banata hai jo:

- **useState** se `count` aur `step` ko handle karta hai.

- **Increment/Decrement** buttons se count ko step ke mutabiq increase/decrease karta hai.

- **Step Input** se user manually step ki value set kar sakta hai.

<hr>

# useReducer

- ## Complex aur Multiple Logics ky liye best hy

# Syntax

```javascript
const [value, action] = useReducer(reducer, initialState);
```

# Example

```javascript
import React, { useReducer } from "react";

function reducer(value, action) {
  if (action.type === "increment") {
    return { count: value.count + value.step, step: value.step };
  } else if (action.type === "decrement") {
    return { count: value.count - value.step, step: value.step };
  } else if (action.type === "changeStep") {
    return { count: value.count, step: action.payload };
  } else {
    return value;
  }
}

export default function USE_ST() {
  const initialState = { count: 0, step: 1 };
  const [value, action] = useReducer(reducer, initialState);

  return (
    <div>
      <p> -> Count: {value.count}</p>
      <p> -> Step: {value.step}</p>

      <button onClick={() => action({ type: "increment" })}>Increment</button>

      <button onClick={() => action({ type: "decrement" })}>Decrement</button>

      <br />

      <label htmlFor="step">Step</label>

      <input
        onChange={(e) =>
          action({
            type: "changeStep",
            payload: parseInt(e.target.value),
          })
        }
        value={value.step}
      />
    </div>
  );
}
```

# Preview

<a href=https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/2_use_reducer.gif target="_blank">Click Here Preview</a>

Yeh code ek counter component hai jo **useReducer** ka use karta hai state aur actions manage karne ke liye:

- `reducer` function state update karne ka logic handle karta hai.

  - `increment` aur `decrement` actions count ko increase ya decrease karte hain.

  - `changeStep` action step value ko update karta hai.

- **Buttons** `increment` aur `decrement` ke liye actions dispatch karte hain.

- **Input field** user se step value le kar usko update karne ke liye `changeStep` action dispatch karta hai.

<hr>

# Use Case

- ## **useState**: Simple state management ke liye, jab state transitions straightforward hoon (jaise single values update karna).
- ## **useReducer**: Jab complex state logic ho, multiple state values update karni hoon, ya actions based updates hoon (jaise form handling ya counters with multiple actions).
