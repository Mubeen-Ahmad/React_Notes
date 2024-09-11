# useState Examples

- ## Initializer State V/S Call State

- ## Initialize State

  - ### Jab Aap `useState` hook ko use karte ho aur usko koi value ya function pass karte ho, to React us value ko sirf pehli dafa component ke load hone par set karta hai.

  - ## Yeh kaam ek dafa hota hai jab component shuru hota hai, aur isi ko initialize state kehte hain.

  - ## Iska maksad hota hai ke jab aap ka component pehli dafa render ho to ek default value set ho jaye.

## Example

```javascript
import React, { useState } from "react";

export default function USE_ST() {
  function load_db() {
    // just assume this is old database record

    let db = [
      { id: 1, item: "red" },
      { id: 2, item: "green" },
      { id: 3, item: "purple" },
      { id: 4, item: "orange" },
    ];

    return db;
  }

  const [data, updateData] = useState(load_db);

  const [text, updateText] = useState("");

  return (
    <div>
      <input
        type="text"
        value={text}
        onChange={(e) => updateText(e.target.value)}
      />

      <button
        type="button"
        onClick={() => {
          updateData(data.concat([{ id: data.length, item: text }]));
          updateText("");
        }}
      >
        ADD
      </button>

      <ul>
        {data.map((i) => (
          <li id={i.id}> {i.item} </li>
        ))}
      </ul>
    </div>
  );
}
```

# Preview

<a href=https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/3_intiliaze_vs_call.gif target="_blank">Click Here Preview</a>

---

## **useState Examples**

### **Initializer State vs Call State**

### **Initialize State:**

- Jab aap `useState` hook ko use karte ho aur usay koi **function reference** pass karte ho (parentheses ke baghair), to React us function ko **sirf ek dafa** tab run karta hai jab component pehli dafa render hota hai.
- Isko **initialize state** kehte hain, aur iska maksad yeh hota hai ke jab component shuru ho to koi default value set ho jaye. Yeh performance ke liye bohot acha hota hai, kyun ke yeh unnecessary calculations ko roknay mein madad karta hai.

---

- ### `const [data, updateData] = useState(load_db);`

  - ### Yahan `load_db` function **initialize** kiya gaya hai, **call nahi kiya**.

  - ### Iska matlab yeh function sirf ek dafa run hoga jab component pehli dafa render hoga.

  - ### Yeh React ko signal deta hai ke sirf shuru mein data load karein.

- ### `const [text, updateText] = useState('');`:

  - ### Yeh simple state hai text input ke liye, jisme user jo bhi type karega, wo yahan store hoga.

  - ### Jab user text input karega, to `onChange` ke zariye new value state me store ho rahi hai, aur jab "Add" button pe click hoga to:

  - ### New item purane `data` array ke sath `concat` hoke list mein add ho jai gi.

  - ### Phir input field clear ho jai gi taake user new item add kar sake.

- ## Is example mein `load_db` function **sirf ek dafa** run hoga jab component pehli dafa load hoga, chahe state kitni baar bhi update ho, yeh function dobara run nahi hoga.
- ## Agar hum `load_db()` ko parentheses ke sath call karte, jaise `useState(load_db());`, to yeh **har render** pe run hota, jo ke har character type karne par function ko dubara run kar deta. Is se **performance slow** hoti kyun ke unnecessary calls ho rahi hoti.
