# MVC与MVVM

## MVC

![img](https://pic1.zhimg.com/v2-cba08bb7a0644050404a05a13a65f668_b.jpg)

前端MVC是很经典的设计思想，分为Model、View、Controller，主要作用如下：

- Model：数据模型，用来存储数据
- View：视图界面，用来展示UI界面和响应用户交互
- Controller：控制器，监听模型数据的改变和控制视图行为、处理用户交互

## MVVM

MVVM是MVC的增强版，实质上和MVC没有本质区别。利用View-Model替代Contorller实现了View和Model的数据绑定，用数据“绑定”的形式让数据更新的事件不需要开发人员手动去，而是自动地双向同步。数据绑定可以认为是Observer模式或者是Publish/Subscribe模式，原理都是为了用一种统一的集中的方式实现频繁需要被实现的数据更新问题。

