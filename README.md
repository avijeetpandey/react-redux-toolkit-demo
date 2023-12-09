## React redux toolkit demo

A repository to demonstrate usage of redux toolkit with react and javascript , while create a todo list application

### Notes

`Redux` or for that matter any state management library came into existance , due to a problem that data/state of the application is not available at a central place inside the application and in order to pass data between the react components we use to have prop drilling but again that comes at a cost that , the component that doesnot even needs the data have to accept it and as the component/application grows it becomes a tedious task to manage the application.

## Evolution

`Flow` ==> `Redux` ==> `React-Redux` (binding for react using react) ==> `Redux tool kit`

### Working

In order to work with redux tool kit there are following steps

- create a store with `configureStore` and register the reducer
- create a slice/ reducer that will basically hold the logic on what to do

```js
import { createSlice, nanoid } from "@reduxjs/toolkit";

const initialState = {
  todos: [{ id: 1, text: "Hello world" }]
};

export const todoSlice = createSlice({
  name: "todo",
  initialState,
  reducers: {
    addTodo: (state, action) => {
      const todo = { id: nanoid(), text: action?.payload };
      state.todos.push(todo);
    },
    removeTodo: (state, action) => {
      state.todos = state.todos.filter((todo) => action.payload !== todo.id);
    }
  }
});

export const { addTodo, removeTodo } = todoSlice.actions;

export default todoSlice.reducer;
```

- use hooks like `useSelector` and `useDispatch` to select the state and manipulate the state

```js
import { useState } from "react";
import { useDispatch } from "react-redux";
import { addTodo } from "../slices/todoSlice";

const [input, setInput] = useState("");
const dispatch = useDispatch();

const addTodoHandler = (e) => {
  e.preventDefault();
  dispatch(addTodo(input));
  setInput("");
};
```

```js
const todos = useSelector((state) => state.todos);
const dispatch = useDispatch();
```
