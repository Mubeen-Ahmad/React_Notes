# useEffect Cleanup

- ## useEffect me cleanup function ka matlab hota hai koi aisa kaam jo aapko component ke unmount hone ya effect ke dobara run hone par karna hota hai, jaise resources ko release karna, event listeners ko remove karna, ya database se disconnect karna.

- ## useEffect ka cleanup function return ke through diya jata hai, aur ye tab call hota hai jab:

  - ### Component unmount ho raha ho.

  - ### useEffect dobara run hone wala ho, uska koi dependency change hone par.

# Syntax

```javascript
useEffect(() => {
  // Effect logic (like setting up a database connection)

  return () => {
    // Cleanup logic (like disconnecting the database)
  };
}, [dependencies]);

// dependencies ke change hone ya component ke unmount hone par cleanup run hota hai
```

# Example

```javascript
import { useState, useEffect } from "react";

function App() {
  const [isConnected, setisConnected] = useState(false);

  useEffect(() => {
    if (isConnected) {
      alert("Database connected");

      return () => {
        alert("Database disconnected");
      };
    }
  }, [isConnected]);

  return (
    <div>
      {isConnected ? (
        <button onClick={() => setisConnected(false)}>Disconnected</button>
      ) : (
        <button onClick={() => setisConnected(true)}>Connected</button>
      )}
    </div>
  );
}

export default App;
```

- ## Yaha agar state true hogi to "Database connected" show ho ga.

  - ### Agar state false ho gayi to return block me "Database disconnected" show ho jayega.

  - ### Aur yaha button me shorthand if-else (ternary operator) use kiya gaya hai. Jaise:

    - ### Agar isConnected true hai to user ko "Disconnect Database" button dikhai dega.

    - ### Otherwise (agar isConnected false hai) to user ko "Connect Database" button dikhai dega.

<br>

# Preview

<a href="https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/5_useEffect.gif" target="_blank">Click Here Preview</a>

<br>
