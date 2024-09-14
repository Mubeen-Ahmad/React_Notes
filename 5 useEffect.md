# useEffect

- ### useEffect React ka ek hook hai jo side effects handle karta hai.

- ### Side effects means, jaise:

  - ### API se data fetch karna (e.g., users ki list server se lana)

  - ### DOM ko directly manipulate karna (e.g., scroll position set karna)

  - ### Browser ke title ko update karna

  - ### Timer set karna (e.g., setInterval ya setTimeout)

  - ### etc.

### Jab aap koi React component render karte hain, to React khud se component ko DOM mein draw karta hai.

### Lekin agar aapko iske baad kuch kaam karna ho, jaise API se data laana etc, to aapko side effects handle karne padte hain, aur yahan useEffect kaam aata hai.

---

# Syntax

```javascript
import React, { useEffect } from "react";

useEffect(() => {
  // here your code
}, []);
```

### Note!

### React mein JavaScript ka mode strict hota hai, matlab:

- ### Development stage mein jab bhi koi component render hota hai, to wo 2 dafa check hota hai. Is liye mein `index.js` mein se strict mode ko disable kar raha hoon taki rendering par 2 dafa call na ho. Iski wajah se samajhne mein mushkil ho sakhti hn.

```javascript
// index.js

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  // <React.StrictMode>
  <App />
  // </React.StrictMode>
);
```

---

# Now Lets Start

# Case 1

- ## Execute on Every Render

  ```javascript
  import React, { useEffect } from "react";

  function USE_ST() {
    useEffect(() => {
      alert("I am Calling on Every Rendering");
    });

    return <h1>Welcome</h1>;
  }

  export default USE_ST;
  ```

  ### Ye `useEffect` hamesha call ho ga jab bhi:

  - ### `Page first time load hony par`

  - ### `State change hony par`

    # Preview

    <a href="https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/1_useeffect.gif" target="_blank">Click Here Preview</a>

    <br>

  # case 1 Example 2

  ```javascript
  import React, { useEffect, useState } from "react";

  function USE_ST() {
    useEffect(() => {
      alert("I am Calling on Every Rendering");
    });

    const [value, setValue] = useState(0);

    return (
      <>
        <h1>Count : {value}</h1>
        <button onClick={() => setValue(value + 1)}>+</button>
      </>
    );
  }

  export default USE_ST;
  ```

  ### Yaha `useState` ka use kiya gaya hai aur button par click karne par value (state) change ho rahi hai.

  - ### So, yaha jab bhi value change ho gi, to `useEffect` call ho ga aur page reload hone par bhi call ho ga.

      <br>
      
      # Preview

    <a href="https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/2_useEffect.gif" target="_blank">Click Here Preview</a>

<br>

# Case 2

- ## Execute only on Specfic State

  ```javascript
  useEffect(() => {
    alert("Update Color");
  }, [color]);
  ```

  ```javascript
  import { useEffect, useState } from "react";

  function App() {
    const [color, setColor] = useState("");

    useEffect(() => {
      alert("I am calling on Every Render");
    });

    useEffect(() => {
      alert("Update Color");
    }, [color]);

    return (
      <div style={{ backgroundColor: color }}>
        <h1>Welcome</h1>
        <button onClick={() => setColor("green")}>Green</button>
        <button onClick={() => setColor("orange")}>Orange</button>
      </div>
    );
  }

  export default App;
  ```

  - ### Yaha pe pehla `useEffect` har rendering aur page refresh hone par run ho ga.

  - ### Aur doosra `useEffect` sirf `color` state change hone par aur page refresh hone par hi run ho ga.

  - ### Aur jab bhi `color` change ho ga, to `color` re-render ho ga. Re-render hone se pehle pehla `useEffect` call ho ga jo har render par call hota hai, phir iske baad `color` wala `useEffect` call ho jayega.

  # Preview

  <a href="https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/3_useEffect.gif" target="_blank">Click Here Preview</a>

    <br>

# Case 3

- ## Execute only on first Page render

  - ### `useEffect(()=>{alert("Call on Every Render")})`

  - ### Ye har trah ki rendering aur page load par call ho ga.

  <hr>

  - ### `useEffect(()=>{alert(" ")}, [color])`

  - ### Ye `useEffect` sirf tab call ho ga jab `color` change ho ga. Jaise hi `color` change ya page reload ho ga, to pehla `useEffect` (jo har render par call hota hai) pehle chalega, phir ye `color` wala `useEffect` chalega.

  <hr>

  - ### `useEffect(()=>{alert("call on load page")}, [])`

  - ### Jab aap `[]` pass karte hain, to ye `useEffect` sirf page reload hone par hi call ho ga. Jaise hi ye call hona shuru ho ga, ussi waqt Every render wala `useEffect` bhi pehle chalega, aur phir baad mein ye "call on load page" wala `useEffect` chalega.

  ```javascript
  import { useEffect, useState } from "react";

  function App() {
    const [color, setColor] = useState("");

    useEffect(() => {
      alert("I am calling on Every Render");
    });

    useEffect(() => {
      alert("Welcome to the page");
    }, []);

    useEffect(() => {
      alert("call on change color");
    }, [color]);

    return (
      <div style={{ backgroundColor: color }}>
        <h1>Welcome</h1>
        <button onClick={() => setColor("green")}>Green</button>
        <button onClick={() => setColor("orange")}>Orange</button>
      </div>
    );
  }

  export default App;
  ```

  - ### on page load

    - ### `useEffect(() => {alert("I am calling on Every Render") });`

    - ### `1st call` every render wala ho ga

    - ### `2nd call` welcome to the page

    - ### `3rd call` call on change color

  - ### on load first page

    - ### `useEffect(() => { alert("Welcome to the page");}, []);`

    - ### `1st call` every render wala ho ga

    - ### `2nd call` welcome to the page

  - ### on load first page

    - ### `useEffect(() => { alert("call on change color"); }, [color]);`

    - ### `1st call` every render wala ho ga

    - ### `2nd call` call on change color

    # Preview

    <a href="https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/4_useeffect.gif" target="_blank">Click Here Preview</a>

    <br>
