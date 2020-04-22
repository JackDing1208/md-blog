# useRef

## 基本用法

基本用法如下，注意要使用current来访问

```jsx
export default function App() {
  const inputRef = useRef();
  useEffect(()=>{
    inputRef.current.value = "Xxx"
  },[])

  return (
    <div className="App">
      <h1>Hello CodeSandbox</h1>
      <input ref={inputRef}/> 
    </div>
  );
}

```

但是函数组件不接受ref属性，一般需要改用forwardRef

```jsx
export default function App() {
  const inputRef = useRef(null);
  const fnRef = useRef(null);
  
  useEffect(()=>{
    inputRef.current.value = "Xxx"
  },[])

  return (
    <div className="App">
      <h1>Hello CodeSandbox</h1>
      <input ref={inputRef}/> 
      <ButtonRef ref={fnRef}/>
    </div>
  );
}

const ButtonRef = React.forwardRef(Button)

function Button (props,ref){
  console.log(props)  
  console.log(ref)
  return (
     <button ref={ref}>haha</button>
  )
}
```





## 其他技巧

useRef跨渲染周期时返回的同一个对象，可以当做state来保存变量，并且current改变时不会触发页面刷新
如果需要刷新页面可以通过proxy代理useRef，变化时调用任意setState即可刷新页面

