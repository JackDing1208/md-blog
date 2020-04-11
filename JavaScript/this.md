# this是什么

## 常规理解

书上概念一般把this当成上下文，随后引申出上下文又是什么这种问题，结果一般就是死记硬背在各种情况下this是啥：

1. 调用对象的方法时，this默认指向该对象
2. 函数调用时未指定this，浏览器环境下this指向window全局对象，严格模式下是undefined
3. 箭头函数里的this指向外面的this
4. 构造函数里的this指向返回的对象
5. class中的this指向class本身

## 本质

所以JS设计者为什么要设计的这么坑，因为this本质上是在**函数调用时隐式传的第一个参数**，比如：

```javascript
fn(1,2)
// fn.call(undefined,1,2)
obj.fn(1,2)
//obj.fn.call(obj,1,2)
array[0]("hi")
//array[0].call(array,1,2)
```

参数是在函数调用时才能确定的，虽然JS会默认帮你传参，但是很多情况下传的都不是你想要的

```javascript
let obj = {
  f1(){
    console.log(this)
  }
}
obj.f1()
let f2 = obj.f1
f2()
```

## 箭头函数的this

箭头函数无法指定this，它是把this当成一个外部的变量，在其定义时就确定了，而不是调用时的参数

## 面试题

```javascript
let length = 10 // let 声明的变量不会变为window的属性，window.length自己去看mdn是啥
function fn (){
	console.log(this.length)
}
let obj ={
 length : 5,
 method(fn){
 	fn()
 	arguments[0]() //fn.call(arguments),arguments.length不包括this
 }
}
obj.method(fn,1,2)
```

