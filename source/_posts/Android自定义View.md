title: "Android自定义View"

date: 2014-12-15 23:52:41

tags: [Android]
categories:
 Android
---
## 我还没有像cha妍一样放弃博客！		
  今天就来总结一下Android中的自定义View。可以说重载 onMeasure()，onLayout()，onDraw()三个函数构建了自定义View的外观形象。再加上onTouchEvent()等重载视图的行为，可以构建任何我们需要的可感知到的自定义View。		
  不管是自定义View还是系统提供的TextView这些，它们都必须放置在 LinearLayout等一些ViewGroup中，因此理论上我们可以很好的理解onMeasure()，onLayout()，onDraw()这三个函数：     
  1. View本身大小多少，这由onMeasure()决定    
  2. View在ViewGroup中的位置如何，这由onLayout()决定
  3. 如何绘制这个View，由onDraw()来决定

## 举个TextView的栗子
	protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
         int widthMode = MeasureSpec.getMode(widthMeasureSpec);
         int heightMode = MeasureSpec.getMode(heightMeasureSpec);
         int widthSize = MeasureSpec.getSize(widthMeasureSpec);
         int heightSize = MeasureSpec.getSize(heightMeasureSpec);
         int width;
         int height;
         ... 
         if (widthMode == MeasureSpec.EXACTLY) {  
           // Parent has told us how big to be. So be it.
             width = widthSize;          
         } 
         else {
           if (mLayout != null && mEllipsize == null) { 
                      des = desired(mLayout);             
            }  
                      ...    
         }       
         setMeasuredDimension(width, height);  
    }


我们要理解的是widthMeasureSpec, heightMeasureSpec这两个参数是从哪里来的？onMeasure()函数由包含这个View的具体的ViewGroup调用，因此值也是 从这个ViewGroup中传入的。这里我直接给出答案：子类View的这两个参数，由ViewGroup中的 layout_width，layout_height和padding以及View自身的layout_margin共同决定。权值weight也是尤其需要考虑的因素，有它的存在情况可能会稍微复杂点。	
## 	widthMeasureSpec,heightMeasureSpec的获取
了解了这两个参数的来源，还要知道这两个值的作用。我们只取 heightMeasureSpec作说明。这个值由**高32位**和**低16位**组成，高32位保存的值叫specMode，可以通过如代码中所示的 MeasureSpec.getMode()获取；低16位为specSize，同样可以由MeasureSpec.getSize()获取。那么 specMode和specSize的作用有是什么呢？要想知道这一点，我们需要知道代码中的最后一行，所有的View的onMeasure()的最后一行都会调用setMeasureDimension()函数的作用——这个函数调用中传进去的值是View最终的视图大小。也就是说 onMeasure()中之前所作的所有工作都是为了最后这一句话服务的。
>	具体怎么用下次再说。( >﹏<。)～ 