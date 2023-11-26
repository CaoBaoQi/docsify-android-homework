# 布局

Android 中的布局管理器本身也是一个界面组件，所有的布局管理器都是 ViewGroup
类的子类，都可以当作容器类来使用。因此，可以在一个布局管理器中嵌套其他布局管理器。Android
中布局管理器可以根据运行平台来调整组件的大小，具有良好的平台无关性。

## 1.1 线性布局

```XML
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
        android:layout_height="wrap_content" tools:context=".MainActivity">

    <LinearLayout android:layout_width="match_parent" android:layout_height="wrap_content"
            android:orientation="vertical">

        <LinearLayout android:layout_width="match_parent" android:layout_height="130dp"
                android:orientation="horizontal">

            <TextView android:layout_width="wrap_content" android:layout_height="match_parent"
                    android:gravity="center" android:layout_weight="1" android:text="红色"
                    android:textSize="25sp" android:background="#DD4D4D"></TextView>

            <TextView android:layout_width="wrap_content" android:layout_height="match_parent"
                    android:gravity="center" android:layout_weight="2" android:text="绿色"
                    android:textSize="25sp" android:background="#4DAC51"></TextView>

            <TextView android:layout_width="wrap_content" android:layout_height="match_parent"
                    android:gravity="center" android:layout_weight="3" android:text="蓝色"
                    android:textSize="25sp" android:background="#1B1B71"></TextView>

        </LinearLayout>


        <LinearLayout android:layout_width="match_parent" android:layout_height="wrap_content"
                android:gravity="center_horizontal" android:orientation="vertical">

            <ImageView android:layout_width="150dp" android:layout_height="150dp"
                    android:scaleType="fitCenter" android:padding="3dp"
                    android:src="@drawable/mcdd_01"></ImageView>

            <ImageView android:layout_width="150dp" android:layout_height="150dp"
                    android:scaleType="fitCenter" android:padding="3dp"
                    android:src="@drawable/mcdd_02"></ImageView>

            <ImageView android:layout_width="150dp" android:layout_height="150dp"
                    android:scaleType="fitCenter" android:padding="3dp"
                    android:src="@drawable/mcdd_03"></ImageView>

            <ImageView android:layout_width="150dp" android:layout_height="150dp"
                    android:scaleType="fitCenter" android:padding="3dp"
                    android:src="@drawable/mcdd_04"></ImageView>

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
        xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
        android:layout_height="match_parent" android:orientation="vertical"
        tools:context=".MainActivity">

    <ImageView android:layout_width="match_parent" android:layout_height="150dp"
            android:scaleType="centerCrop" android:src="@drawable/jinzhong_12" />

    <TableLayout android:layout_width="wrap_content" android:layout_height="wrap_content"
            android:layout_gravity="center_horizontal" android:gravity="center"
            android:paddingTop="5dp">

        <TableRow>
            <ImageView android:layout_width="83dp" android:layout_height="83dp"
                    android:layout_marginStart="3dp" android:src="@drawable/logo" />
            <ImageView android:layout_width="83dp" android:layout_height="83dp"
                    android:src="@drawable/logo" />
            <ImageView android:layout_width="83dp" android:layout_height="83dp"
                    android:src="@drawable/logo" />
            <ImageView android:layout_width="83dp" android:layout_height="83dp"
                    android:src="@drawable/logo" />
            <ImageView android:layout_width="83dp" android:layout_height="83dp"
                    android:src="@drawable/logo" />
        </TableRow>

        <TableRow>
            <ImageView android:layout_width="83dp" android:layout_height="83dp"
                    android:src="@drawable/logo" />
            <ImageView android:layout_width="83dp" android:layout_height="83dp"
                    android:src="@drawable/logo" />
            <ImageView android:layout_width="83dp" android:layout_height="83dp"
                    android:src="@drawable/logo" />
            <ImageView android:layout_width="83dp" android:layout_height="83dp"
                    android:src="@drawable/logo" />
            <ImageView android:layout_width="83dp" android:layout_height="83dp"
                    android:src="@drawable/logo" />
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
        xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
        android:layout_height="match_parent" tools:context=".MainActivity">

    <TextView android:id="@+id/tv_hello_world" android:layout_width="wrap_content"
            android:layout_height="wrap_content" android:text="发现新版本，需要更新吗？"
            android:textSize="20sp" android:layout_centerInParent="true" />

    <Button android:id="@+id/bt_update" android:layout_width="wrap_content"
            android:layout_height="wrap_content" android:text="现在更新"
            android:layout_toLeftOf="@+id/bt_no_update"
            android:layout_below="@+id/tv_hello_world" />

    <Button android:id="@+id/bt_no_update" android:layout_width="wrap_content"
            android:layout_height="wrap_content" android:text="以后再说"
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
        xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
        android:layout_height="match_parent" tools:context=".MainActivity">

    <TextView android:layout_width="300dp" android:layout_height="300dp" android:background="#f00"
            android:layout_gravity="center" />
    <TextView android:layout_width="200dp" android:layout_height="200dp"
            android:background="#5E794EED" android:layout_gravity="center" />

    <TextView android:layout_width="100dp" android:layout_height="100dp"
            android:background="#70B5CA" android:layout_gravity="center" />
</FrameLayout>
```

![image-20231017164228258](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017164228258.png)

## 1.5 网格布局

```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
        android:layout_height="match_parent" android:orientation="vertical"
        tools:context=".MainActivity">

    <ImageView android:layout_width="match_parent" android:layout_height="150dp"
            android:scaleType="centerCrop" android:src="@drawable/jinzhong_11" />

    <GridLayout android:layout_width="wrap_content" android:layout_height="wrap_content"
            android:layout_gravity="center_horizontal" android:foregroundGravity="center"
            android:columnCount="5" android:orientation="horizontal" android:rotation="2">

        <ImageView android:layout_width="73dp" android:layout_height="73dp" android:clickable="true"
                android:src="@drawable/logo" />
        <ImageView android:layout_width="73dp" android:layout_height="73dp"
                android:src="@drawable/logo" />
        <ImageView android:layout_width="73dp" android:layout_height="73dp"
                android:src="@drawable/logo" />
        <ImageView android:layout_width="73dp" android:layout_height="73dp"
                android:src="@drawable/logo" />
        <ImageView android:layout_width="73dp" android:layout_height="73dp"
                android:src="@drawable/logo" />
        <ImageView android:layout_width="73dp" android:layout_height="73dp"
                android:src="@drawable/logo" />
        <ImageView android:layout_width="73dp" android:layout_height="73dp"
                android:src="@drawable/logo" />
        <ImageView android:layout_width="73dp" android:layout_height="73dp"
                android:src="@drawable/logo" />
        <ImageView android:layout_width="73dp" android:layout_height="73dp"
                android:src="@drawable/logo" />
        <ImageView android:layout_width="73dp" android:layout_height="73dp"
                android:src="@drawable/logo" />
    </GridLayout>

</LinearLayout>
```

![image-20231017165007511](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017165007511.png)
