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
