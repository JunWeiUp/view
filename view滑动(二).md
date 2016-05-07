#前言
     view的滑动是Android自定义控件的基础内容，我们在开发过程中难免会遇到view的滑动问题，
    实现view的滑动有很多种方式，给大家讲几个基本的滑动方法

#view的滑动
##1.layout()
view中会调用onLayout()方法来摆放位置，我们也可以直接用onLayout的left、top、right、bottom这四种属性来控制View的位置。比如我们自定义一个View，在onTouchEvent()方法中获取触摸点的坐标，放入onlayout()中，这样就可以实现随着触摸的位置变化而滑动，如图：

    ...
     public boolean onTouchEvent(MotionEvent event) {
        //获取到手指处的横坐标和纵坐标
        int x = (int) event.getX();
        int y = (int) event.getY();

      switch (event.getAction()) {
       case MotionEvent.ACTION_DOWN: 
          lastX = x; 
          lastY = y; 
           break;
      case MotionEvent.ACTION_MOVE:
                //计算移动的距离
                int offsetX = x - lastX;
                int offsetY = y - lastY;
                //调用layout方法来重新放置它的位置
                layout(getLeft()+offsetX, getTop()+offsetY,
                        getRight()+offsetX , getBottom()+offsetY);
                break;
        ...
    }
    ...

##2.也可以通过offsetLeftAndRight()和offsetTopAndBottom()方法
这个和onlayout大致相同，只不过这个方法传入的是偏移量，我就直接放代码啦

                   case MotionEvent.ACTION_MOVE:
                //计算移动的距离
                int offsetX = x - lastX;
                int offsetY = y - lastY;
                //对left和right进行偏移
                offsetLeftAndRight(offsetX);
                //对top和bottom进行偏移
                offsetTopAndBottom(offsetY);
                break;

##3.LayoutParams(通过改变参数达到滑动的目的)
LayoutParams中保存了view的布局参数，我们通过不短的改变view参数，从而达到滑动的目的，
比如我们想实现viewpage 两个条目切换的时候下面有有一个滑动的滑条那么就可以用这种方式
![Paste_Image.png](http://upload-images.jianshu.io/upload_images/1507947-7fa3d90e2ff0b279.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

        indicatorLine.post(new Runnable() {
            @Override
            public void run() {
                indicatorLine.measure(0, 0);
                int indicatorLineWidth = indicatorLine.getMeasuredWidth();
                originalIndicatorLineLeftMargin = rightTitleMarginLeft +
                (float) leftTitleWidth / 2 - (float) DimenUtil.dip2px(IntentionMajorActivity.this, 65) / 2 - textDistence;
                indicatorLineLayoutParams.leftMargin = (int) originalIndicatorLineLeftMargin;
                indicatorLine.setLayoutParams(indicatorLineLayoutParams);
            }
        });
    }

##4.scollTo与scollBy
scollTo(x,y)表示移动到某个具体的坐标点，而scollBy(dx,dy)则表示移动的增量为dx、dy。其实scollBy最终也是要调用scollTo的。scollTo、scollBy移动的是View的内容，如果在ViewGroup中使用则是移动他所有的子View。我们将ACTION_MOVE中的代码替换成如下代码：
  
       ((View)getParent()).scrollBy(-offsetX,-offsetY);

如果我们要让view随着手指的触摸方向移动我们就要把偏移量设为负值

#后言

还有一种滑动方式那就是通过动画的方式进行滑动，那么不在今天讲述的范围，
由于本人水平有限，某些地方可能存在误解或不准确，如果你对此有疑问可以[gitHub](https://github.com/JunWeiUp/view)上提交issues进行反馈。


参考自：
http://blog.csdn.net/itachi85/article/details/50724558
http://www.linuxidc.com/Linux/2015-11/125390.htm