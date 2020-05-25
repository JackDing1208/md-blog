# generator

```js
function *foo(x) {
    var y = 2 * (yield (x + 1));
    var z = yield (y / 3);
    return (x + y + z);
}

var it = foo( 5 );

// note: not sending anything into `next()` here
console.log( it.next() );       // { value:6, done:false }
console.log( it.next( 12 ) );   // { value:8, done:false }
console.log( it.next( 13 ) );   // { value:42, done:true }
```

- 函数加*，内部用yield关键字
- 第一次调用返回genertor对象
- 调用next方法执行到下一次yield，返回`{value:xxx,done:false}`
- value为本次yield的返回值，没有执行到return前done为false
- next的参数会重新给上一次的yield赋值，