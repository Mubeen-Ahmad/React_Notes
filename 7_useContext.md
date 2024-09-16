# useContext

- ### useContext React ka ek hook hai jo tumhe kisi context se value ko directly access karne ki sahulat deta hai.

- ### Iska matlab hai ke tum apne components mein bina prop drilling (yani props ko har component ke through pass karna) ke context ko use kar sakte ho.

<br>

# Understand Example Problem

- ### Humare paas `App.js` (starting point) mein value hai.

- ### Hume ye value `App.js` se `Page1` ko pass karni hai.

- ### Phir `Page1` se ye value `Page2` ko pass karni hai.

- ### Hum props ka use karke ye value `App.js` se `Page1`, aur phir `Page1` se `Page2` tak le ja sakte hain.

```javascript
import { useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Home</h1>
      <Page1 count={count} />
    </div>
  );
}

function Page1({ count }) {
  return (
    <div>
      <h3>Page1</h3>
      <Page2 count={count} />
    </div>
  );
}

function Page2({ count }) {
  return (
    <div>
      <h4>Page2</h4>
      count : {count}
    </div>
  );
}

export default App;
```

### Preview Page

<img title="output" alt="Alt text" src="https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/1usecontext.png" width=150 height=250>

<br>

## Ye problem ko solve karne ke liye hum `useContext` aur `createContext` function ka use karenge

- ### `createContext` React ka ek function hai jo hume globally shared data ko handle karne ka tareeqa deta hai bina props drilling ke.

- ### Iska matlab hai ke tum kisi bhi component tree ke andar kisi bhi level par data ko share kar sakte ho, aur wo data direct child components ko props ke zariye pass karne ki zarurat nahi hoti.

- ### `createContext` value ko lekar aayega aur `useContext` us value ko use karega.

- ### Note: `createContext` hook nahi hai, ye React ka function hai, jabke `useContext` hook hai.

# Understand Syntax

```javascript
import { useState, createContext, useContext } from "react";

// create and export a context
export const context = createContext();

function App() {
  const [count, setCount] = useState(0);

  return (
    <context.Provider value={count}>
      <Page2 />
    </context.Provider>
  );
}

function Page2() {
  const count = useContext(context);

  return (
    <div>
      <h4>Page2</h4>
      count : {count}
    </div>
  );
}

export default App;
```

## 1 Context Create Karna:

- ### Pehle createContext() ka use karke ek context (context) banaya gaya hai jisko hum globally data share karne ke liye use karenge.

## 2 Context Provide Karna:

- ## App component ke andar context.Provider ka use karke count ki value ko provide kiya gaya hai. count ko useState hook ke zariye manage kiya gaya hai.

## 3 Context Value Access Karna:

- ## Page2 component ke andar useContext() hook ka use karke context se count ko access kiya gaya hai.

# Example

```javascript
import { useState, createContext, useContext } from "react";

export const context = createContext();

function App() {
  const [count, setCount] = useState(8);

  return (
    <context.Provider value={count}>
      <div>
        <h1>Home</h1>
        <Page1 />
      </div>
    </context.Provider>
  );
}

function Page1() {
  return (
    <div>
      <h3>Page1</h3>
      <Page2 />
    </div>
  );
}

function Page2() {
  const count = useContext(context);

  return (
    <div>
      <h4>Page2</h4>
      count : {count}
    </div>
  );
}

export default App;
```

### Preview Page

<img title="output" alt="Alt text" src="https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/2usecontext.png" width=150 height=250>

<br>

# Example 2 (componnents)

- ### App.js

```javascript
import Home from "./components/Home";
import Page1 from "./components/Page1";
import Result from "./components/Result";

import { createContext, useState } from "react";

export const context = createContext();

function App() {
  const [value, setValue] = useState({ x: 2, y: 6 });

  return (
    <context.Provider value={value}>
      <Home />
      <Page1 />
      <Result />
    </context.Provider>
  );
}

export default App;
```

# Explaination

- ## Context:

  - ### `createContext()` ka use karke ek global context (context) banaya gaya hai jisko hum data share karne ke liye use karenge.

- ## Manage State:

  - ### App component ke andar useState hook se ek object {x: 2, y: 6} ko manage kiya gaya hai. Ye object value me store hai.

- ## Context Provide:

  - ### `context.Provider` ke through value ko Home, Page1, aur Result components ke liye available karaya gaya hai. Ab yeh components useContext hook ka use karke value ko access kar sakte hain.

<br>

- ## Home.js

```javascript
import { useContext } from "react";
import { context } from "../App";

export default function Home() {
  const value = useContext(context);

  return (
    <div style={{ border: "1px solid red", margin: 3, maxWidth: 200 }}>
      <h4>This is Home Page</h4>
      <p>Value of x is {value.x}</p>
    </div>
  );
}
```

# Explaination

- ## Access Context Access:

  - ### Home component me `useContext()` hook ka use karke context se value ko access kiya gaya hai, jo App.js me provide ki gayi thi.

- ## Use Value:

  - ### Access ki gayi value me se x ko extract karke Home component ke andar display kiya gaya hai.

- ## Display Value:

  - ### Ek simple div me styling ke saath x ki value ko display kiya gaya, jahan This is Home Page heading aur x ki value ko paragraph me dikhaya gaya hai.

<br>

- ## Page1.js

```javascript
import { useContext } from "react";
import { context } from "../App";

export default function Page1() {
  const value = useContext(context);

  return (
    <div style={{ border: "1px solid red", margin: 3, maxWidth: 200 }}>
      <h4>This is Page1</h4>
      <p>Value of y is {value.y}</p>
    </div>
  );
}
```

# Explaination

- ## Access Context:

  - ### Page1 component me `useContext()` hook ka use karke context se value ko access kiya gaya hai, jo App.js me context.Provider ke zariye provide kiya gaya tha.

- ## Use Value:

  - ### value se y ko extract karke Page1 component ke andar display kiya gaya hai.

- ## Display Value:

  - ### Ek simple div banaya gaya hai jisme border, margin, aur maxWidth styling ke sath y ki value ko display kiya gaya hai. Heading me This is Page1 aur y ki value ko paragraph me dikhaya gaya hai.

<br>

- ## Result.js

```javascript
import { useContext } from "react";
import { context } from "../App";

export default function Result() {
  const value = useContext(context);

  return (
    <div>
      <h4>
        Sum of ({value.x},{value.y}) is {value.x + value.y}
      </h4>
    </div>
  );
}
```

# Explaination

- ### Result component me `useContext` se x aur y ko access karke unka sum calculate kiya gaya, aur usko UI me dikhaya gaya hai.

### Preview Page

<img title="output" alt="Alt text" src="https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/6useEffect.png" width=150 height=250>

<br>
