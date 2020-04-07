# JSONP

## 出现原因

上古时期没有ajax，通过表单submit的方式发请求会导致页面刷新，因此想到了通过各种标签的src属性向服务端发请求，其中比较靠谱的是通过<script>标签，服务端返回的响应内容会作为javascript代码直接执行

## 实现过程

1. 请求方创建动态 script标签，其中src 指向响应方，同时将回调函数的名字作为查询参数一起发过去（src="yoyo.com?callback=xxx）
2. 响应方根据查询参数callback，将对应的响应内容通过执行回调函数的JS代码一起传给请求方（xxx('你要的数据'）) （xxx.call(undefined, '你要的数据')
3. 浏览器接收到响应，就会执行 xxx.call(undefined, '你要的数据')对应渲染页面，同时将页面中的script标签删掉

**服务端返回的参数形式一般为JSON，加上前后代码看起来像padding，合起来就叫JSONP**

**JSONP只能发get请求，但是默认支持跨域，基本已经过时**

## 代码示例

### 客户端

```javascript
button.addEventListener('click', (e)=>{
    let script = document.createElement('script')
    let functionName = 'jack'+ parseInt(Math.random()*10000000 ,10)  //随机函数名
    window[functionName] = function(){  
        if(response==="success"){
        amount.innerText = amount.innerText  - 1
        }
    }
    script.src = '/pay?callback=' + functionName
    document.body.appendChild(script)     //script在body中才有用
    script.onload = function(e){ // 状态码是 200~299 则表示成功
        e.currentTarget.remove()
        delete window[functionName] // 请求完了就干掉这个随机函数
    }
    script.onerror = function(e){ // 状态码大于等于 400 则表示失败
        e.currentTarget.remove()
        delete window[functionName] // 请求完了就干掉这个随机函数
    }
})
```

### 服务端

```javascript
if (path === '/pay'){
    let amount = fs.readFileSync('./db', 'utf8')
    amount -= 1
    fs.writeFileSync('./db', amount)
    let callbackName = query.callback
    response.setHeader('Content-Type', 'application/javascript')
    response.write(`
        ${callbackName}.call(undefined, 'success')
    `)
    response.end()
}
```

## 其他

1. 查询参数统一为callback
2. 本地的动态函数名字随机生成防止影响全局变量
3. 可以直接使用jQuery实现，不要与ajax弄混

```
$.ajax({
 url: "http://jack.com:8002/pay",
 dataType: "jsonp",
 success: function( response ) {
     if(response === 'success'){
     amount.innerText = amount.innerText - 1
     }
 }
 })
```

