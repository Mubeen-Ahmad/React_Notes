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

# Todo Example

- ### Math.max ka kaam hai maximum value dena

- ### ...xyz object ko spread karta hai aur naya object create karta hai

```javascript
else if (action === "delete") {
  setTodos((prevTodos) => prevTodos.filter((t) => t.id !== payload.id))
};
```

- ### Yahan filter function data ko payload se compare kar raha hai

```javascript
else if (action === "checked") {

      setTodos((prevTodos) =>
        prevTodos.map((t) =>
          t.id === payload.id ? { ...t, done: !t.done } : t
        )
      );
}
```

- ### Yahan map function ka use kiya gaya hai aur ? ternary operator hai, jo shorthand if-else ki tarah kaam karta hai

- ### ...t ka matlab hai purana data, aur done: !t.done ka matlab hai agar done true hai to false ho jayega, warna true ho jayega

# Full Code

```javascript
import { useState } from "react";

export default function USE_ST() {
  const [todos, setTodos] = useState([
    { id: 1, title: "Buy Milk", done: false },
    { id: 2, title: "Buy Eggs", done: true },
  ]);

  const [id, setID] = useState(Math.max(...todos.map((i) => i.id)) + 1);

  const [todoValue, setTodoValue] = useState("");

  const divStyle = {
    margin: 10,
    padding: 10,
    border: "1px solid black",
    maxWidth: "30%",
    maxHeight: "10%",
    backgroundColor: "skyblue",
  };

  const btnStyle = {
    width: "30%",
    marginLeft: 25,
    backgroundColor: "orange",
    borderRadius: 50,
  };

  const handler = (action, payload) => {
    if (action === "add") {
      setTodos((prevTodos) => [
        ...prevTodos,
        {
          id: id,
          title: todoValue,
          done: false,
        },
      ]);
      setID(id + 1);
      setTodoValue("");
    } else if (action === "delete") {
      setTodos((prevTodos) => prevTodos.filter((t) => t.id !== payload.id));
    } else if (action === "checked") {
      setTodos((prevTodos) =>
        prevTodos.map((t) =>
          t.id === payload.id ? { ...t, done: !t.done } : t
        )
      );
    } else if (action === "edit") {
      const newValue = prompt("Edit Item", payload.new_value);
      if (newValue !== null) {
        setTodos((prevTodos) =>
          prevTodos.map((t) =>
            t.id === payload.id ? { ...t, title: newValue } : t
          )
        );
      }
    }
  };

  return (
    <>
      <div style={divStyle}>
        <input
          type="text"
          placeholder="Todo Data"
          name="todo"
          id="todo"
          onChange={(e) => setTodoValue(e.target.value)}
          value={todoValue}
        />

        <button style={btnStyle} onClick={() => handler("add")}>
          ADD
        </button>
      </div>

      <div style={divStyle}>
        <ul>
          {todos.map((i) => (
            <li key={i.id}>
              <input
                style={{ width: 20 }}
                type="checkbox"
                checked={i.done}
                onChange={() => handler("checked", { id: i.id })}
              />
              {i.title}
              <button
                style={{ marginLeft: 20, marginTop: 10 }}
                onClick={() =>
                  handler("edit", { id: i.id, new_value: i.title })
                }
              >
                Edit
              </button>
              <button
                style={{ marginLeft: 20, marginTop: 10 }}
                onClick={() => handler("delete", { id: i.id })}
              >
                Delete
              </button>
            </li>
          ))}
        </ul>
      </div>
    </>
  );
}
```

# Preview

<a href="https://github.com/Mubeen-Ahmad/React_Notes/blob/main/images/usestate_todo.gif" target="_blank">Click Here Preview</a>

<br>

# Todo Same Example With `useReducer`

```javascript
import React, { useReducer } from "react";

const initialState = {
  todos: [
    { id: 1, title: "Buy Milk", done: false },
    { id: 2, title: "Buy Eggs", done: true },
  ],
  nextId: 3,
  todoValue: "",
};

const reducer = (state, action) => {
  if (action.type === "ADD") {
    return {
      ...state,
      todos: [
        ...state.todos,
        { id: state.nextId, title: state.todoValue, done: false },
      ],
      nextId: state.nextId + 1,
      todoValue: "",
    };
  } else if (action.type === "DELETE") {
    return {
      ...state,
      todos: state.todos.filter((todo) => todo.id !== action.payload.id),
    };
  } else if (action.type === "CHECKED") {
    return {
      ...state,
      todos: state.todos.map((todo) =>
        todo.id === action.payload.id ? { ...todo, done: !todo.done } : todo
      ),
    };
  } else if (action.type === "EDIT") {
    return {
      ...state,
      todos: state.todos.map((todo) =>
        todo.id === action.payload.id
          ? { ...todo, title: action.payload.new_value }
          : todo
      ),
    };
  } else if (action.type === "UPDATE_TODO_VALUE") {
    return {
      ...state,
      todoValue: action.payload.value,
    };
  } else {
    return state;
  }
};

export default function USE_ST() {
  const [state, dispatch] = useReducer(reducer, initialState);

  const divStyle = {
    margin: 10,
    padding: 10,
    border: "1px solid black",
    maxWidth: "30%",
    maxHeight: "10%",
    backgroundColor: "skyblue",
  };

  const btnStyle = {
    width: "30%",
    marginLeft: 25,
    backgroundColor: "orange",
    borderRadius: 50,
  };

  return (
    <>
      <div style={divStyle}>
        <input
          type="text"
          placeholder="Todo Data"
          name="todo"
          id="todo"
          onChange={(e) =>
            dispatch({
              type: "UPDATE_TODO_VALUE",
              payload: { value: e.target.value },
            })
          }
          value={state.todoValue}
        />

        <button style={btnStyle} onClick={() => dispatch({ type: "ADD" })}>
          ADD
        </button>
      </div>

      <div style={divStyle}>
        <ul>
          {state.todos.map((i) => (
            <li key={i.id}>
              <input
                style={{ width: 20 }}
                type="checkbox"
                checked={i.done}
                onChange={() =>
                  dispatch({ type: "CHECKED", payload: { id: i.id } })
                }
              />
              {i.title}
              <button
                style={{ marginLeft: 20, marginTop: 10 }}
                onClick={() =>
                  dispatch({
                    type: "EDIT",
                    payload: {
                      id: i.id,
                      new_value: prompt("Edit Item", i.title),
                    },
                  })
                }
              >
                Edit
              </button>
              <button
                style={{ marginLeft: 20, marginTop: 10 }}
                onClick={() =>
                  dispatch({ type: "DELETE", payload: { id: i.id } })
                }
              >
                Delete
              </button>
            </li>
          ))}
        </ul>
      </div>
    </>
  );
}
```

## Code me `reducer` ka use karny sy kia faida huwa ?

- ## **Single Function for All Actions**:
  - ### Sab actions ko ek hi `reducer` function se handle kiya, `useState` me har action ke liye alag state setters ki zarurat hoti.
- ## **Centralized State Management**:

  - ### Sab state variables (`todos`, `nextId`, `todoValue`) ko ek hi object me manage kiya, `useState` me inhe alag-alag handle karna padta.

- ## **Scalability**:

  - ### Asaan tareeke se naye actions aur logic ko reducer me add kar sakte hain, jabki `useState` me yeh difficult hota.
