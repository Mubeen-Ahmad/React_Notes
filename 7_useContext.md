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

###  Preview Page

<img title="output" alt="Alt text" src="https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/1usecontext.png" width=150 height=200>
