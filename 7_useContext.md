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

![image](https://scontent.flhe41-1.fna.fbcdn.net/v/t39.30808-1/424600352_2586639321495598_4721183349517087182_n.jpg?stp=cp0_dst-jpg_s60x60&_nc_cat=106&ccb=1-7&_nc_sid=50d2ac&_nc_eui2=AeEE4J12YROWnHkD8_ARtJJqsthCfGkUgmey2EJ8aRSCZ-suf2Lz_Wvq3B80N_y6izKOVQ_5Q3KlBAeMXKJ1qv0-&_nc_ohc=KRkmHu1WS5kQ7kNvgE2ZqNE&_nc_ht=scontent.flhe41-1.fna&_nc_gid=AQ0MT1L7abTZ9iCYk6cU0h2&oh=00_AYDMiF-EaBOlNLCs1yF74v6TixFDFRjMc5zcyYf5TiZAdg&oe=66ECD737 "a title")