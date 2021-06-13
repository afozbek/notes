---
description: We are examining React's useContext hook
---

# How Context Helps for State Management

### State Management

While developing React application, you are most likely will have different pages, components to render. In this case most components itself has the hooks we can use\(functional components\) to create component state. And you also pass some internal state as a prop to subcomponents.

```jsx
// components/TodoList.js

const TodoList = () => {
  const [todoList, setTodoList] = useState([]);
    const [user, setUser] = useState({})

  return (
    <>
            <Header user={user}/>
            <Body user={user}/>
            <Footer user={user}/>
      {
        todoList.map(todo => <Todo todo={todo} key={todo.id} user={user}/>)
      }            
    </>
  );
}
```

### Context API

React Context is a state management API which is in the React's core package. We can use Context API for pretty much anything that we need from state manegement library. Main purpose of using it is sharing data across multiple components without passing them via props.

All context consumers are **re-rendered** whenever a value passed to the Provider changes. One way to fix this is to use useMemo hook which would **memoize** the value object. It would only be re-created when **dependency** value changes.

In this article we will try to manage our todoList using Context API

#### Creating TodoListContext

```jsx
// contexts/todoListContext.js

const TodoListContext = createContext([]);

const TodoListContextProvider = (props) => {
  const [todoList, setTodoList] = useState([]);

  // Only rerender when todoList changes
  const value = useMemo(() => [todoList, setTodoList], [todoList]);
  return (
    <TodoListContext.Provider value={value}>
      {props.children}
    </TodoListContext.Provider>
  )
}
```

We can also create a custom hook and manage some logic inside of our hook.

```jsx
// contexts/todoListContext.js

const useTodoList = () => {
  const context = useContext(TodoListContext);
  if (!context) {
    throw new Error("useTodoList must be used inside TodoListProvider")
  }

  return context;
}
```

After that we can use this hook in the components

```jsx
// components/TodoList.js

const TodoList = () => {
  const [todoList, setTodoList] = useTodoList();

    const addTodo = (todo) => setTodoList([...todoList, todo]);

  return (
    <>
      {
        todoList.map(todo => <Todo todo={todo} key={todo.id} />)
      }
            <button onClick={() => { addTodo({ id: Math.random(), name: "New Todo" })}}>Add Todo</button>
    </>
  );
}
```

Then what we can do to improve the hook is tha we can remove any external logic from components and adding them to the hook itself. So we can remove addTodo function from here and move it to the useTodoList hook. And we can also use useReducer instead of useState in this situation.

**useReducer** can reduce the complexity of the actions and increase usability

```jsx
// contexts/todoListContext.js

const todoReducer = (state, action) => {
  switch (action.type) {
    case "NEW": return [...state, action.payload]
    case "DELETE": return state.filter(todo => todo.id != action.payload);
    default: return state;
  }
}

const useTodoList = () => {
  const context = useContext(TodoListContext);
  if (!context) {
    throw new Error("useTodoList must be used inside TodoListProvider")
  }

    const [todoList, setTodoList] = context;

    // Hook Functions
  const addTodo = (todo) => dispatch({ type: "NEW", payload: todo })
  const removeTodo = (todoId) => dispatch({ type: "DELETE", payload: todoId });

  return {
        todoList,
        setTodoList,
        addTodo,
        removeTodo
    };
}
```

Final code will look like this;

```jsx
const TodoListContext = createContext([]);

const todoReducer = (state, action) => {
  switch (action.type) {
    case "NEW": return [...state, action.payload]
    case "DELETE": return state.filter(todo => todo.id != action.payload);
    default: return state;
  }
}

const TodoListContextProvider = (props) => {
  const [state, dispatch] = useReducer(todoReducer, []);

  const value = useMemo(() => [state, dispatch], [state]);
  return (
    <TodoListContext.Provider value={value}>
      {props.children}
    </TodoListContext.Provider>
  )
}

const useTodoList = () => {
  const context = useContext(TodoListContext);
  if (!context) {
    throw new Error("useTodoList must be used inside TodoListProvider")
  }

  const [state, dispatch] = context;

  // Hook Functions
  const addTodo = (todo) => dispatch({ type: "NEW", payload: todo })
  const removeTodo = (todoId) => dispatch({ type: "DELETE", payload: todoId });

  return {
    todos: state,
    dispatch,
    addTodo,
    removeTodo
  };
}

export { TodoListContextProvider, useTodoList
```

#### Reference

[Application State Management with React](https://kentcdodds.com/blog/application-state-management-with-react)

[How to use React Context effectively](https://kentcdodds.com/blog/how-to-use-react-context-effectively)

[Hooks API Reference - React](https://reactjs.org/docs/hooks-reference.html#usecontext)

