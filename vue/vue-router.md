# vue-router

## 基本原理

在页面中插入 <router-view> 标签后，vue-router会根据url中的hash将对应的组件渲染到router-view里面

## 使用方法

### 基本路由

一般由path和component组成，redurect可直接重定向到其他页面，路径复杂时可以添加name方便跳转

```
const router = new Router({
  routes: [
    {
      path: "/",
      redirect: "login"
    },
    {
    	name:"login"
      path: "/login",
      component: Login,
    },
```



### 多层路由嵌套

在children中添加子路由，要注意路径的写法

```javascript
const router = new Router({
  routes: [
    {
      path: "/",
      redirect: "login"
    },
    {
      path: "/login",
      component: Login,
    },
    {
      path: "/dashboard",
      component: Dashboard,
      //子路由路径开头不能加/
      children: [{
        path: "/",
        redirect: "home",
      }, {
        path: "home",
        component: Home,
      }, {
        path: "company",
        component: CompanyFile,
      }, {
        path: "share",
        component: ShareFile,
      }],
    },
    {
      path: "*",
      component: Page404,
    },
  ],
})
```

### 单页面多个router-view

给router-view绑定name属性，在components中配置每个router-view的组件，没有名字的默认为default、

```javascript
const router = new Router({
  routes: [
    {
      path: "/login",
      components:{
        header:Header,
        main:Main,
        default:Root
      } 
    },
```



### 跳转方法

- <router-link>标签可以跟根据配置路由的path或者name点击跳转并传参

` <router-link :to="{name:'post',params:{id:value.id}}">`

- $router提供push、replace、go等方法跳转

直接使用this.$router.push("/home")方法，新版本中该方法为异步会返回Promise，相同路径跳转会报错，需要添加`.catch((error)=>{console.log(error)})`处理错误

replace方法跳转到的页面不会向 navigation stack 添加记录，无法返回到该页面

go方法参数为数字，一般用来返回上一页go(-1)