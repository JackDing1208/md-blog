数组中可能存在undefined，“”等多余元素，可以使用filter方法配合Boolean函数删除，缺点是会把0删除

```javascript
const a = [1,2,4,0,"",undefined,false]
console.log(a.filter(Boolean))  // [1,2,4]
```

