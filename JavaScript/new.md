两种理解

new 作为一个函数

```javascript
function myNew(Con, ...args) {
  let obj = {}
  // obj.__proto__ = Con.prototype
  Object.setPrototypeOf(obj, Con.prototype)
  let result = Con.apply(obj, args)
  return result instanceof Object ? result : obj
}
```



new XXX 整体作为一个函数，new实现了一部分XXX中被省略的代码

```javascript
function XXX(name,age){
	// let this = {}
  // this.__proto__ = XXX.prototype 
  this.name = name 
  this.age = age
  // return this
}
```



