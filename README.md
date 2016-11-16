# ColorFilter
# Android 更改纯色背景图片颜色，可实现一张背景圆形图片展示不同颜色
项目中可能会遇到比如多个纯色圆形背景列表或者说纯色圆形头像背景，一般让UI设计师设计多张背景图；但是有更好的方法只需一张图就可以搞定。
当然完全也不用麻烦我们的UI设计师啦，直接画一个圆形背景图不就行了。

>- 用shape画圆形图

>- View设置该背景

>- 代码里设置setColorFilter即可

首先画个圆形图，大家都比较熟悉，再次记录下（画一个白色圆形图）：

		<shape xmlns:android="http://schemas.android.com/apk/res/android"
		    android:shape="oval">
		    <solid android:color="@color/white" />
		    <size
		        android:width="50dp"
		        android:height="50dp" />
		</shape>

然后设置该背景：

		<ImageView
	        android:id="@+id/mColor"
	        android:layout_width="60dp"
	        android:layout_height="60dp"
	        android:background="@android:color/transparent"
	        android:src="@drawable/dot_white" />

最后在需要更改颜色设置颜色：

		mColor.setColorFilter(0xFFFF0000);//设置红色颜色

这就完成了，是不是很方便。主要还是setColorFilte，当然该属性支持xml里设置的。

setColorFilter(ColorFilter filter)是什么呢？
设置颜色过滤，这个方法需要我们传入一个ColorFilter参数同样也会返回一个ColorFilter实例。我们在setColorFilter(ColorFilter filter)的时候可以直接传入ColorMatrixColorFilter、LightingColorFilter或PorterDuffColorFilter的子类对象作为参数。

我们采用默认的直接颜色，我们进入源代码可以发现默认是PorterDuff.Mode.SRC_ATOP

		/**
	     * Set a tinting option for the image. Assumes
	     * {@link PorterDuff.Mode#SRC_ATOP} blending mode.
	     *
	     * @param color Color tint to apply.
	     * @attr ref android.R.styleable#ImageView_tint
	     */
	    @RemotableViewMethod
	    public final void setColorFilter(int color) {
	        setColorFilter(color, PorterDuff.Mode.SRC_ATOP);
	    }

至于属性参数设置为PorterDuff.Mode。
至于该参数有什么不同呢，网上也有很多，就不累赘了，找个大神的实验可以理解下[点击查看](http://blog.csdn.net/t12x3456/article/details/10432935)

### 注意 ###

1. 我们画的圆形的图片不能是透明的，透明就没法进行填充过滤啦。
2. 有的如果不生效，可以尝试添加下设置背景为透明

		android:background="@android:color/transparent"
但是我进行了测试添加不添加，都是生效的。

