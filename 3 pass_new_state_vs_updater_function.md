# Passing the next state directly

- ### Yaha Aap directly new value pass kary gn

- ### Agar aap directly ek new state value pass karte ho, to har update isolated hoga. Yeh purane state ke upar depend nahi karega.

- ### `setCount(count + 1);`

- ### `Issue :`

  - ### Agar multiple state updates ek sath perform kiye jaye , To React batching ki wajah se sirf ek update ko consider karega, kyunki har update ko isolated maana jata hai, purani state pe nahi.

  - ### is sy state 1 dafa hi update ho gi

# Passing an updater function

- ### Yaha Aap ek function pass karte ho jo previous state ko le kar new state calculate karta hai.

- ### React sure karta hai ki har update correct previous state ke basis par ho.

- ### `setCount(i => i + 1);`

- ### `Benefit :`

  - ### Har state update previous state ke upar based hota hai, to agar multiple updates hoti hain, sab sequentially previous state ke basis par perform hoti hain

  - ### is sy state multiple times update ho gi

```javascript
import React, { useState } from "react";

export default function USE_ST() {
  const [count, setCount] = useState(0);

  function direct_state() {
    setCount(count + 1);
  }

  function updater_function() {
    setCount((i) => i + 1);
  }

  return (
    <>
      <h3>Counter : {count}</h3>

      <button
        onClick={() => {
          direct_state();
          direct_state();
          direct_state();
        }}
      >
        3 Calls with <br />
        direct_state
      </button>

      <button
        onClick={() => {
          updater_function();
          updater_function();
          updater_function();
        }}
      >
        3 Calls with <br />
        updater_function
      </button>
    </>
  );
}
```

# Preview

<a href="https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/4_pass_state_vs_updater_function.gif" target="_blank">Click Here Preview</a>

---
