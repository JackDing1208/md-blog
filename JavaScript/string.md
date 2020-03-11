# String

## String和unicode

### 获取unicode编码——charCodeAt

```
let a = "jack"
let b = a.charCodeAt()
console.log(b) //106
```

不传时默认参数为0，表示字符串第一个字符的下标

### 根据unicode获取字符——fromCharCode

```
let a = String.fromCharCode(2030)
console.log(a)   // "你"
```

