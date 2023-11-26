# 🌈目标

- [x] Android 中的组件和布局
- [x] 美化布局
- [x] Android 控件

Android 程序主要分为三部分：

- 界面设计
- 代码流程控制
- 资源建设

其中代码和资源主要是由开发者进行编写和维护的，对于大部分用户来说是不关心的，展现在用户面前的最直观的就是界面设计。作为一个程序设计者，必须首先考虑用户的体验，只有用户满意了开发的产品，应用才能推广， 才有价值，因此界面设计尤为重要。

控件是 Android 项目开发的基本组成单位，通过使用组件可以高效地开发 Android 程序，所以熟练掌握控件的使用时进行 Android 程序开发的重要前提。

# View 和 View Group

Android 中所有的组件都继承于 View 类，View 类代表的就是屏幕上的一块空白的矩形区域，该空白区域可用于绘画和事件处理。不同的界面组件，相当于对这个矩形区域做了一些处理，如文本显示框、按钮等。

View 类有一个重要的子类，ViewGroup。ViewGroup 类是所有布局类和容器组件的基类，它是一个不可见的容器，它里面还可以添加 View 组件或 ViewGroup 组件，主要用于定义它所包含的组件的排列方式，例如，网格排列或线性排列等。通过 View 和 ViewGroup 的组合使用，从而使得整个界面呈现出一种层次结构。ViewGroup 内包含的组件如下图所示：



![image-20231017180507941](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180507941.png)



Android 中控制组件的显示方式有两种：

- 通过 XML 布局文件来设置组件的属性进行控制
- 通过 java 代码调用相应的方法进行控制

这两种方式控制 Android 界面显示的效果是完全一样的。实际上 XML 文件的属性与 java 代码中方法之间存在着一一对应关系，在此列出常用的属性供参考：



||||
|-|-|-|
|XML 属性|对应方法 |说明|
|android: alpha|setAlpha|设置组件的透明度|
|android: background|setBackground|设置组件的背景|
|android: clickable|setClickable|设置组件是否可以触发单击事件|
|android: focusable|setFocusable|设置组件是否可以得到焦点|
|android: id|setId|设置组件的唯一 ID|
|android: minHeight|setMinHeight|设置组件的最小高度|
|android: minWidth|setMinWidth|设置组件的最小宽度|
|android: padding|setPadding|在组件四边设置边距|
|android: scaleX|setScaleX|设置组件在 X 轴方向的缩放|
|android: visibility|setVisibility|设置组件是否可见|




几乎每个界面组件都需要设置

- android: layout_height
- android: layout_width

这两个属性，用于指定该组件的高度和宽度，主要有一下三种取值：

1. fill_parent: 表示组件的高或宽与其父容器的高或宽相同
2. wrap_content: 表示组件的高或宽恰好能包裹内容，随着内容的变化而变化
3. match_parent: 该属性值与 fill_parent 完全相同。（Android 2.2 之后推荐使用 match_parent 代替 fill_parent）

虽然使用 XML 和 java 都可以控制界面的显示，但是它们又有各自的优缺点：

1. 完全使用 java 代码来控制界面不仅繁琐，而且界面和代码相混合，不利于解耦、分工。
2. 完全使用 XML 布局文件虽然方便、便捷，但灵活性不好，不能动态改变属性值。

因此我们经常会混合使用这两种方式来控制界面，一般来说，习惯将：

- 变化小、比较固定、初始化的属性放在 XML 文件中管理
- 需要动态变化的属性则交给 java 代码控制

例如：可以在 XML 布局文件中设置文本显示框的高度和宽度以及初始化时显示文字，在代码中根据实际需要动态地改变现实的文字。

# Android 布局

Android 中的布局管理器本身也是一个界面组件，所有的布局管理器都是 ViewGroup 类的子类，都可以当作容器类来使用。因此，可以在一个布局管理器中嵌套其他布局管理器。Android 中布局管理器可以根据运行平台来调整组件的大小，具有良好的平台无关性。

## 1.1 线性布局

```XML
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    tools:context=".MainActivity">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="130dp"
            android:orientation="horizontal">

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="match_parent"
                android:gravity="center"
                android:layout_weight="1"
                android:text="红色"
                android:textSize="25sp"
                android:background="#DD4D4D">
            </TextView>

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="match_parent"
                android:gravity="center"
                android:layout_weight="2"
                android:text="绿色"
                android:textSize="25sp"
                android:background="#4DAC51">
            </TextView>

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="match_parent"
                android:gravity="center"
                android:layout_weight="3"
                android:text="蓝色"
                android:textSize="25sp"
                android:background="#1B1B71">
            </TextView>

        </LinearLayout>


        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center_horizontal"
            android:orientation="vertical">

            <ImageView
                android:layout_width="150dp"
                android:layout_height="150dp"
                android:scaleType="fitCenter"
                android:padding="3dp"
                android:src="@drawable/mcdd_01">
            </ImageView>

            <ImageView
                android:layout_width="150dp"
                android:layout_height="150dp"
                android:scaleType="fitCenter"
                android:padding="3dp"
                android:src="@drawable/mcdd_02">
            </ImageView>

            <ImageView
                android:layout_width="150dp"
                android:layout_height="150dp"
                android:scaleType="fitCenter"
                android:padding="3dp"
                android:src="@drawable/mcdd_03">
            </ImageView>

            <ImageView
                android:layout_width="150dp"
                android:layout_height="150dp"
                android:scaleType="fitCenter"
                android:padding="3dp"
                android:src="@drawable/mcdd_04">
            </ImageView>

        </LinearLayout>

    </LinearLayout>


</ScrollView>


```

![image-20231017180522417](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180522417.png)

## 1.2 表格布局



```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <ImageView
        android:layout_width="match_parent"
        android:layout_height="150dp"
        android:scaleType="centerCrop"
        android:src="@drawable/jinzhong_12"/>

    <TableLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:gravity="center"
        android:paddingTop="5dp">

        <TableRow>
            <ImageView
                android:layout_width="83dp"
                android:layout_height="83dp"
                android:layout_marginStart="3dp"
                android:src="@drawable/logo"/>
            <ImageView
                android:layout_width="83dp"
                android:layout_height="83dp"
                android:src="@drawable/logo"/>
            <ImageView
                android:layout_width="83dp"
                android:layout_height="83dp"
                android:src="@drawable/logo"/>
            <ImageView
                android:layout_width="83dp"
                android:layout_height="83dp"
                android:src="@drawable/logo"/>
            <ImageView
                android:layout_width="83dp"
                android:layout_height="83dp"
                android:src="@drawable/logo"/>
        </TableRow>

        <TableRow>
            <ImageView
                android:layout_width="83dp"
                android:layout_height="83dp"
                android:src="@drawable/logo"/>
            <ImageView
                android:layout_width="83dp"
                android:layout_height="83dp"
                android:src="@drawable/logo"/>
            <ImageView
                android:layout_width="83dp"
                android:layout_height="83dp"
                android:src="@drawable/logo"/>
            <ImageView
                android:layout_width="83dp"
                android:layout_height="83dp"
                android:src="@drawable/logo"/>
            <ImageView
                android:layout_width="83dp"
                android:layout_height="83dp"
                android:src="@drawable/logo"/>
        </TableRow>

    </TableLayout>



</LinearLayout>
```



![image-20231017180532954](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180532954.png)

## 1.3 相对布局



```XML
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/tv_hello_world"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="发现新版本，需要更新吗？"
        android:textSize="20sp"
        android:layout_centerInParent="true" />

    <Button
        android:id="@+id/bt_update"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="现在更新"
        android:layout_toLeftOf="@+id/bt_no_update"
        android:layout_below="@+id/tv_hello_world" />

    <Button
        android:id="@+id/bt_no_update"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="以后再说"
        android:layout_alignRight="@+id/tv_hello_world"
        android:layout_below="@+id/tv_hello_world" />


</RelativeLayout>
```

![image-20231017164021320](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017164021320.png)

## 1.4 层布局

```XML
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:layout_width="300dp"
        android:layout_height="300dp"
        android:background="#f00"
        android:layout_gravity="center"/>
    <TextView
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:background="#5E794EED"
        android:layout_gravity="center"/>

    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="#70B5CA"
        android:layout_gravity="center"/>
</FrameLayout>
```

![image-20231017164228258](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017164228258.png)

## 1.5 网格布局

```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <ImageView
        android:layout_width="match_parent"
        android:layout_height="150dp"
        android:scaleType="centerCrop"
        android:src="@drawable/jinzhong_11"/>

    <GridLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:foregroundGravity="center"
        android:columnCount="5"
        android:orientation="horizontal"
        android:rotation="2">

        <ImageView
            android:layout_width="73dp"
            android:layout_height="73dp"
            android:clickable="true"
            android:src="@drawable/logo"/>
        <ImageView
            android:layout_width="73dp"
            android:layout_height="73dp"
            android:src="@drawable/logo"/>
        <ImageView
            android:layout_width="73dp"
            android:layout_height="73dp"
            android:src="@drawable/logo"/>
        <ImageView
            android:layout_width="73dp"
            android:layout_height="73dp"
            android:src="@drawable/logo"/>
        <ImageView
            android:layout_width="73dp"
            android:layout_height="73dp"
            android:src="@drawable/logo"/>
        <ImageView
            android:layout_width="73dp"
            android:layout_height="73dp"
            android:src="@drawable/logo"/>
        <ImageView
            android:layout_width="73dp"
            android:layout_height="73dp"
            android:src="@drawable/logo"/>
        <ImageView
            android:layout_width="73dp"
            android:layout_height="73dp"
            android:src="@drawable/logo"/>
        <ImageView
            android:layout_width="73dp"
            android:layout_height="73dp"
            android:src="@drawable/logo"/>
        <ImageView
            android:layout_width="73dp"
            android:layout_height="73dp"
            android:src="@drawable/logo"/>
    </GridLayout>

</LinearLayout>
```

![image-20231017165007511](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017165007511.png)



