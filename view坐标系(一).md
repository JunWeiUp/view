微博上有幸认识了GcsSloop,并给我提了非常好的意见，以后文章的干货一点会更多！

赫赫，好了该说正题了，view可以说是非常重要的，现在很多开发者只会去用，很难知道为什么要去这么做，一旦出了问题就Stack Overflow一下，这种程序员就是面向Stack Overflow编程 哈哈，好了 ，今天开始我会分几篇文章给大家讲解View的大部分基本原理。当你遇到嵌套，触摸冲突，自定义动画效果就不会害怕啦，这也是证明你通向Android高级开发工程师的第一步。

AndroidView体系是界面的核心，在这个系列中我分为多个章节陆续讲到 View坐标系、View的滑动机制、View的事件分发机制 、View的绘制流程 等等 来介绍Android View体系。 我们从最基础的坐标系开始！

1.View介绍

View是Android所有控件的基类，而且ViewGroup也是继承View的，下站图可以让大家更加直观的让大家了解View的体系.
![](http://upload-images.jianshu.io/upload_images/489570-631e06fb624c34b9.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


2.坐标系

Android中分为两种Android坐标系和视图坐标系

(-) Android坐标系

Android坐标系还是比较简单的， 将屏幕的左上角的顶点作为Android坐标系的原点，这个原点向右是X轴正方向，原点向下是Y轴正方向。

还是看图比较直观：（虽然是我百度的哈哈）
![](http://upload-images.jianshu.io/upload_images/489570-7430da1a80125cf4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


在MotionEvent中的getRawX()和getRawY()获取的坐标都是Android坐标系的坐标。

(二)视图坐标系

顾名思义 Android的屏幕是有限的 ，有时候view会很大，我们通过屏幕能看到的View大小称为视图，

我们还是直接看图吧！（哈哈）

![](http://upload-images.jianshu.io/upload_images/489570-7cc507c5f1cf433f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


View自身坐标﻿﻿
如下方法可以获得View到其父控件（ViewGroup）的距离：

getTop()：获取View自身顶边到其父布局顶边的距离

getLeft()：获取View自身左边到其父布局左边的距离

getRight()：获取View自身右边到其父布局左边的距离

getBottom()：获取View自身底边到其父布局顶边的距离
MotionEvent提供的方法﻿﻿﻿
getX()：获取点击事件距离控件左边的距离，即视图坐标

getY()：获取点击事件距离控件顶边的距离，即视图坐标

getRawX()：获取点击事件距离整个屏幕左边距离，即绝对坐标

getRawY()：获取点击事件距离整个屏幕顶边的的距离，即绝对坐标
今天就写到这里 ，如果那里有不明白的可以直接在评论回复！

祝大家过一个好的 5.1！