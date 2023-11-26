# 安卓视图

# View 和 View Group

Android 中所有的组件都继承于 View 类，View
类代表的就是屏幕上的一块空白的矩形区域，该空白区域可用于绘画和事件处理。不同的界面组件，相当于对这个矩形区域做了一些处理，如文本显示框、按钮等。

View 类有一个重要的子类，ViewGroup。ViewGroup 类是所有布局类和容器组件的基类，它是一个不可见的容器，它里面还可以添加
View 组件或 ViewGroup 组件，主要用于定义它所包含的组件的排列方式，例如，网格排列或线性排列等。通过 View
和 ViewGroup 的组合使用，从而使得整个界面呈现出一种层次结构。ViewGroup 内包含的组件如下图所示：

![image-20231017180507941](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180507941.png)

Android 中控制组件的显示方式有两种：

- 通过 XML 布局文件来设置组件的属性进行控制
- 通过 java 代码调用相应的方法进行控制

这两种方式控制 Android 界面显示的效果是完全一样的。实际上 XML 文件的属性与 java
代码中方法之间存在着一一对应关系，在此列出常用的属性供参考：

|XML 属性|对应方法 |说明|
|-|-|-|
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
3. match_parent: 该属性值与 fill_parent 完全相同。（Android 2.2 之后推荐使用 match_parent 代替
   fill_parent）

虽然使用 XML 和 java 都可以控制界面的显示，但是它们又有各自的优缺点：

1. 完全使用 java 代码来控制界面不仅繁琐，而且界面和代码相混合，不利于解耦、分工。
2. 完全使用 XML 布局文件虽然方便、便捷，但灵活性不好，不能动态改变属性值。

因此我们经常会混合使用这两种方式来控制界面，一般来说，习惯将：

- 变化小、比较固定、初始化的属性放在 XML 文件中管理
- 需要动态变化的属性则交给 java 代码控制

例如：可以在 XML 布局文件中设置文本显示框的高度和宽度以及初始化时显示文字，在代码中根据实际需要动态地改变现实的文字。
