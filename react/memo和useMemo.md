# memo

一般希望子组件不再重新渲染可以用到React.memo包装，其原理类似PureComponent，当父组件重新渲染时，只在props改变时才会重新渲染

```jsx
export default function App() {
  const  [n,setN]=  useState(0) 
  return (
    <div className="App">
      <div onClick={()=>{
        setN(n=>n+1)}
      }>{n}</div>
      <Memoed/>  
    </div>
  );
}

const Memoed = React.memo(Demo)

function Demo (){
  console.log("我又渲染了")
  return (
   <div>Memo</div>
   )
}
```

PureComponent实际上是将shouldComponentUpdate方法定义好的Component，只对props进行浅对比，因此当props为一个function或者obj时，即使是同样的function也会导致组件重新渲染，此时就可以用到useEffect将prop包装

```javascript
  const obj = useMemo(()=>{return {xxx:1}},[xxx])
  const fn = useMemo(()=>{
    return ()=>{console.log("xxx")}
  },[xxx])
```

如果觉得fn这种写法看起来很诡异，可以直接用useCallback语法糖

```javascript
  const fn = useCallback(()=>{
    console.log("xxx")
  },[xxx])
```

