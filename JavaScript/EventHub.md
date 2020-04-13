# EventHub

经典的发布订阅模式中的事件中心手写版

```javascript
class EventHub {
  store = {}
  on(type, callback) {
    this.store[type] = this.store[type] || []
    this.store[type].push(callback)
  }
  emit(type, params) {
    this.store[type] = this.store[type] || []
    this.store[type].forEach(fn=>{fn(params)}) 
  }
}

let hub = new EventHub()
hub.on("xxx",(value)=>{console.log(value)})
hub.emit("xxx",222)
```

