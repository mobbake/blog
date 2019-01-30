---
title: Emmet使用手册
date: 2017-10-10 14:53:02
tags: emmet
categories: 开发手册
---

## 简介

Emmet可以快速的编写HTML代码，输入缩写，按tab即可生成相应代码。

大多数编辑器已默认安装Emmet
<!--more-->

## 语法

### Child: >  后代

缩写：`nav>ul>li`

```html
<nav>
    <ul>
        <li></li>
    </ul>
</nav>
```

### Sibling: + 同级

缩写：`div+p+bq`

```html
<div></div>
<p></p>
<blockquote></blockquote>
```

### Climb-up: ^ 父级

缩写：`div+div>p>span+em^bq`

```html
<div></div>
<div>
    <p><span></span><em></em></p>
    <blockquote></blockquote>
</div>
```

缩写：`div+div>p>span+em^^bq`

```html
<div></div>
<div>
    <p><span></span><em></em></p>
</div>
<blockquote></blockquote>
```

### `()` 分组

缩写：`(div>dl>(dt+dd)*3)+footer>p`

```html
<div>
    <header>
        <ul>
            <li><a href=""></a></li>
            <li><a href=""></a></li>
        </ul>
    </header>
    <footer>
        <p></p>
    </footer>
</div>
```

### Multiplication: `*`

使用 * 生成多个相同元素

缩写：`ul>li*5`

```html
<ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
</ul>
```

### Item numbering: `$`

缩写：`ul>li.item$*5`

```html
<ul>
    <li class="item1"></li>
    <li class="item2"></li>
    <li class="item3"></li>
    <li class="item4"></li>
    <li class="item5"></li>
</ul>
```


缩写：`h$[title=item$]{Header $}*3`

```html
<h1 title="item1">Header 1</h1>
<h2 title="item2">Header 2</h2>
<h3 title="item3">Header 3</h3>
```

缩写：`ul>li.item$$$*5`

```html
<ul>
    <li class="item001"></li>
    <li class="item002"></li>
    <li class="item003"></li>
    <li class="item004"></li>
    <li class="item005"></li>
</ul>
```

缩写：`ul>li.item$@-*5`

```html
<ul>
    <li class="item5"></li>
    <li class="item4"></li>
    <li class="item3"></li>
    <li class="item2"></li>
    <li class="item1"></li>
</ul>
```

缩写：`ul>li.item$@3*5`

```html
<ul>
    <li class="item3"></li>
    <li class="item4"></li>
    <li class="item5"></li>
    <li class="item6"></li>
    <li class="item7"></li>
</ul> 
```

### ID and CLASS attributes

缩写： `#header`
```    
<div id="header"></div> 
```

缩写：`.title`
```
<div class="title"></div> 
```

缩写：`form#search.wide`
```
<form id="search" class="wide"></form>
```

### 自定义属性


缩写：`p[title="Hello world"]`
```
<p title="Hello world"></p>
```
缩写：`td[rowspan=2 colspan=3 title]`
```
<td rowspan="2" colspan="3" title=""></td>
```
缩写：`[a='value1' b="value2"]`
```
<div a="value1" b="value2"></div> 
```
### 文本 Text: {}


缩写：`a{Click me}`

```
<a href="">Click me</a>
```

缩写：`p>{Click }+a{here}+{ to continue}`

```
<p>Click <a href="">here</a> to continue</p>
```

> [官方语法速查表](http://docs.emmet.io/cheat-sheet/ "官方语法速查表")