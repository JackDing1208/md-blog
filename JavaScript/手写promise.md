## 存在问题

- then的链式调用没实现
- 使用其他微任务替换setTimeout（setImmediate,nextTick）

```javascript
class Promise2 {
  status = "pending"
  succeedCallback = []
  failCallback = []

  constructor(fn) {
    if (typeof fn !== "function") {
      throw new Error("Promise必须接受函数")
    }
    fn(this.resolve.bind(this), this.reject.bind(this))
  }
  resolve(result) {
    if(this.status !== "pending" )return
    this.status = "fulfilled"
    setTimeout(() => {
      this.succeedCallback.forEach((callback) => {
        if (typeof callback === "function") {
          callback.call(undefined, result)
        }
      })
    }, 0)
  }
  reject(reason) {
    if(this.status !== "pending" )return
    this.status = "rejected"
    setTimeout(() => {
      this.succeedCallback.forEach((callback) => {
        if (typeof callback === "function") {
          callback.call(undefined, result)
        }
      })
    }, 0)
  }
  then(succeed, fail) {
    this.succeedCallback.push(succeed)
    this.failCallback.push(fail)
  }
}

function nextTick(fn) {
    var counter = 1;
    var observer = new MutationObserver(fn);
    var textNode = document.createTextNode(String(counter));

    observer.observe(textNode, {
      characterData: true
    });

    counter = counter + 1;
    textNode.data = String(counter);
}


let xxx = new Promise2((resolve, reject) => {
  setTimeout(()=>{
    resolve(22222)
  },1000) 
})

xxx.then((value) => {
  console.log("then", value)
})

```

