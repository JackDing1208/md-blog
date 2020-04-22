# useState

首先根据原理简单实现一下useState

```jsx
import React,{useState} from "react";

let _state = []
let index = 0
const myUseState = (initValue)=>{
  const currentIndex = index
  _state[currentIndex] = _state[currentIndex] === undefined ? initValue:_state[currentIndex]
  const setState = (value)=>{
    _state[currentIndex]  = value
    index = 0 
    App.rerender(Math.random())
  }
  index++
  return [_state[currentIndex],setState]
}

export default function App() {
  const [n,setN] = myUseState(0)
  const [m,setM] = myUseState(0)
  App.rerender = useState(null)[1]

  return (
    <div className="App">
      <h1>counterN:{n}</h1>
      <h1>counterN:{m}</h1>
      <button onClick ={()=>{setN(n+1)}}>n+1</button>
      <button onClick ={()=>{setM(m+1)}}>m+1</button>
    </div>
  );
}
```

通过实现原理可以看出

1. 使用useState后每个组件的VDOM都有自己的_state和index属性
2. 每次调用useState会返回新的state和setState
3. setState不会改变当前state，而是rerender后返回新的state
4. 组件内部每次执行useState顺序必须相同，不支持if
5. 要避免每次返回新的state可以考虑使用useRef、useContext