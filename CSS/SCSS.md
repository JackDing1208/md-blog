# SCSS

## 语言由来

ruby社区的工程师觉得CSS很难用于是发明了sass，sass可以理解为简洁版CSS，但是传统前端表示看不懂，于是设计者在sass新增功能的基础上改的比较像CSS，从而方便传统前端使用，最终形成了SCSS

## 使用配置

由于是预编译的CSS，使用时需要用webpack的相关loader进行转译，一般配置如下：

```
{
  test: /\.scss$/,
  use: ['style-loader', 'css-loader', 'sass-loader']  //顺序不能变！！！
},
```

## 常用语法

1. 声明变量

```scss
$avtive-color:red;
div{
   border: 1px solid $active-color
}
```

2. 选择器嵌套，可配合>使用

```scss
body {
    height: 100vh;
    background: grey;

    .xxx {
        height: 50vh;
        background: yellow;

        > .x {
            height: 25vh;
            background: blue;
        }
    }
}
```

3. 选择器复用

```scss
.xxx{
  backgrond:red;
  &:hover{
    backgrond:blue;
  }
}  
```

4. 函数function

示例：rem 替换 vw时自动计算占比

```less
$designWidth: 640;
@function px($px){
   return $px/$designWidth * 10 + rem;
}
.box{
   width:px(320)
}
```

5. 引入外部CSS

```scss
@import 'markdown-css'
```

6. mixin直接复用

```scss
@mixin debug{
  border:1px solid red;
}

.xxx{
  @include debug;
}
```

可以配合变量使用

```less
@mixin debug($color:red) {
    border: 1px solid $color;
}

.text {
    @include debug(blue);
    height: 100%;
    margin: 0.5em 0.5em;
}
```

7. placeholder，编译后会将使用相同CSS的选择器并列

```scss
%font{
    color:red;
}
.text1 {
    @extend %font;
    height: 100%;
    margin: 0.5em 0.5em;
}
.text2 {
    @extend %font;
    height: 100%;
    margin: 0.5em 0.5em;
}
```

8. 配合变量循环生成CSS

```scss
$class: col-;
@for $n from 1 through 24 {
    .#{$class}#{$n} {
        width: ($n/24)*100%;
    }
}

@for $n from 1 through 24 {
    .offset-#{$n} {
        margin-left: ($n/24)*100%;
    }
}
```