# Update Data in Form

- ### ... person
- ### ...person yahan spread operator ka use kia hn, jo existing object person ki saari properties ko copy karta hai.
- ### Iska matlab hai ke purana person object intact rahega, aur aap sirf name property ko update kar rahe ho.

```javascript
import React, { useState } from "react";

export default function USE_ST() {
  const [person, setPerson] = useState({
    name: "",
    title: "",
    city: "",
    image: "",
  });

  let update_name = (e) => {
    setPerson({ ...person, name: e.target.value });
  };
  let update_title = (e) => {
    setPerson({ ...person, title: e.target.value });
  };
  let update_city = (e) => {
    setPerson({ ...person, city: e.target.value });
  };
  let update_image = (e) => {
    setPerson({ ...person, image: e.target.value });
  };

  return (
    <>
      <div
        style={{
          padding: 10,
          maxWidth: 100,
          margin: 5,
          lineHeight: "1.5",
          color: "red",
        }}
      >
        Name : <input value={person.name} onChange={update_name} />
        <br />
        Title : <input value={person.title} onChange={update_title} />
        <br />
        city : <input value={person.city} onChange={update_city} />
        <br />
        Image : <input value={person.image} onChange={update_image} />
      </div>

      <div
        style={{
          border: "2px solid black",
          backgroundColor: "grey",
          maxWidth: 200,
          padding: 10,
          margin: 5,
          color: "blue",
        }}
      >
        <p>
          <i>{person.title}</i> {" by "} {person.name} <br />
          (located in {person.city})
        </p>
        <img src={person.image} alt={person.title} width="200" height="200" />
      </div>
    </>
  );
}
```

# Preview

<a href="https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/usetate_ex_1.gif" target="_blank">Click Here Preview</a>

---
