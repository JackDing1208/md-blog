



目前个人全面改用hooks很少写class组件，但由于以往项目中用到的一些生命周期将被废弃，总结一下新的生命周期用法，

## 废弃原因

react 17 将推出新的渲染方—— **异步渲染**（ Async Rendering），提出一种可被打断的生命周期，而可以被打断的阶段正是实际 `dom` 挂载之前的虚拟 `dom` 构建阶段，也就是要被去掉的三个生命周期 `componentWillMount`，`componentWillReceiveProps` 和 `componentWillUpdate`。

