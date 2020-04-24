# useReducer和useContext

这些hooks都是从redux思想中衍生出来的，根据能不用redux就不要用redux原则，以后可以用这些hooks替代redux

useReducer其实和useState差不多，只是当需要多种方法操作state时可以参考redux的reducer使用

useContext则主要是方便子组件获取context，整体类似react-redux

```JSX
import React,{useContext,useReducer,createContext} from "react";
import "./styles.css";


const store = {
  "xxx":1,
  "yyy":2,
}

const reducer  = (state,action)=>{
  switch(action.type){
    case "add":
      return {...state,xxx:state.xxx+ action.value}
    case "minus":
      return {...state,xxx:state.xxx+ action.value}  
    default:
      return state
  }
}

const Context = createContext(null)

export default function App() {
  const [state,dispatch]=useReducer(reducer,store)
  return (
    <Context.Provider value={{state,dispatch}}>
      <div className="App">
        <Demo1/>
      </div>
    </Context.Provider>
  );
}

const Demo1 = ()=>{
  const {state} = useContext(Context)
  return(
    <div>
      <div>{state.xxx}</div>
      <Demo2/>
    </div>
  ) 
}


function Demo2 () {
  const {dispatch} = useContext(Context)
  const add = ()=>{
    dispatch({type:"add",value:1})
  }
  return (<button onClick={add}>Demo2</button>)
}
```

