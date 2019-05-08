---
title: 用css3创建页面加载动画
date: 2018-09-15 15:19:41
tags: css
categories: 翻译
---



> 原文[Create a Bouncing Page Loader with CSS3 Animations](https://scotch.io/tutorials/create-a-bouncing-page-loader-with-css3-animations)

我需要一个页面加载时的loader，查找了之后最终决定自己做一个

### html

html页面结构

```html
<p>A simple representation of an animated bouncing loader!</p>

<div class="loader">
  <span></span>
  <span></span>
  <span></span>
</div>
```

class为`loader `的`div`就是组件的主体，其中三个`span`为三个动画元素

### CSS样式 

```css
body {
  background: #2C294F;
  padding: 2rem;
}

p {
  font: 1rem/1.45 "Operator Mono";
  color: #A599E9;
  text-align: center;
}

.loader {
  display: flex;
  justify-content: center;
  align-items: center;
}

/_ Loader circles _/
.loader > span {
  background: #FAD000;
  border-radius: 50%;
  margin: 5rem 0.5rem;
  animation: bouncingLoader 0.6s infinite alternate;
}

.loader > span:nth-child(2) {
  animation-delay: 0.2s;
}

.loader > span:nth-child(3) {
  animation-delay: 0.4s;
}
```

loader使用了flex布局。这样可以 使用loader组件在垂直和水平方向上都 居中 

span元素设置border-radius使其变为圆形

每个span元素都 有一个animation属性，其中定义了一个bouncingLoader的keyframe—稍后补充，infinite表示无限循环

第二个元素动画延迟0.2秒，第三个元素动画延迟0.4秒

### Animation Keyframe

keyframe用于定义动画在一个周期内的行为，本例中定义的名字为`bouncingLoader`

keyframe中有两个关键字from 和to ，来定义元素的起始位置形状属性等 ，和结束的位置形状属性等

也可以 用0%来代替from,用100%来代替to

下面是本例中的keyframe

```css
/_ Define the animation called bouncingLoader. _/
@keyframes bouncingLoader {
  from {
    width: 0.1rem;
    height: 0.1rem;
    opacity: 1;
    transform: translate3d(0);
  }
  to {
    width: 1rem;
    height: 1rem;
    opacity: 0.1;
    transform: translate3d(0, -1rem, 0);
  }
}
```

此案例中使用from 和 to 来定义样式，如宽度，高度，透明度，为了实现小球的跳动效果 ，使用的`transform`改变来移动元素

在transfrom属性中，使用translate3d方法 ，此方法接受三个参数（x，y, z),分别表示三个维度的移动

###　animation连写

```
animation: animation-name, animation-duration, animation-iteration-count, animation-direction;
```

`animation-name` 定义动画的名字

`animation-duration`： 定义动画的时间 周期

`animation-iteration-count`定义动画循环次数

`animation-direction`定义动画是否轮流反向播放

综上本例中

```css
animation: bouncingLoader 0.6s infinite alternate;
```

动画名字为`bouncingLoader`

动画时长为0.6秒

无限次循环

`alternate`动画应该轮流反向播放。