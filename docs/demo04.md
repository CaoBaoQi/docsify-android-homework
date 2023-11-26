# Android 表单

- 文本显示框 TextView
- 文本编辑框 EditView
- 按钮 Button
- 图片视图 ImageView

## 1.1 实战-登录界面

```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/white"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <!--头像-->
    <ImageView
        android:layout_width="70dp"
        android:layout_height="70dp"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="70dp"
        android:background="@drawable/avata"/>

    <!--用户名-->
    <EditText
        android:layout_width="fill_parent"
        android:layout_height="40dp"
        android:layout_gravity="center_horizontal"
        android:layout_marginLeft="35dp"
        android:layout_marginRight="35dp"
        android:layout_marginTop="35dp"
        android:drawableLeft="@drawable/username"
        android:drawablePadding="10dp"
        android:gravity="center_vertical"
        android:hint="@string/usernameMain"
        android:paddingLeft="8dp"
        android:textColor="#a3a3a3"
        android:textSize="14sp"/>

    <!--密码-->
    <EditText
        android:layout_width="fill_parent"
        android:layout_height="40dp"
        android:layout_gravity="center_horizontal"
        android:layout_marginLeft="35dp"
        android:layout_marginRight="35dp"
        android:layout_marginTop="5dp"
        android:drawableLeft="@drawable/password"
        android:drawablePadding="10dp"
        android:gravity="center_vertical"
        android:hint="@string/passwordMain"
        android:inputType="textPassword"
        android:paddingLeft="8dp"
        android:textColor="#a3a3a3"
        android:singleLine="true"
        android:textSize="14sp"/>
    <!--登录-->
    <Button
        android:layout_width="fill_parent"
        android:layout_height="40dp"
        android:layout_gravity="center_horizontal"
        android:layout_marginLeft="35dp"
        android:layout_marginRight="35dp"
        android:layout_marginTop="15dp"
        android:background="#03A9F4"
        android:text="@string/loginMain"
        android:textColor="@color/white"
        android:textSize="18sp"/>

    <!--注册 和 找回密码-->
    <LinearLayout
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:layout_marginLeft="35dp"
        android:layout_marginRight="35dp"
        android:layout_marginTop="8dp"
        android:gravity="center_horizontal"
        android:orientation="horizontal">

        <TextView
            android:layout_width="1dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:gravity="center_horizontal"
            android:padding="9dp"
            android:text="@string/registerMain"
            android:textColor="#2196F3"
            android:textSize="14sp"/>

        <TextView
            android:layout_width="1dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:gravity="center_horizontal"
            android:padding="9dp"
            android:text="@string/findPasswordMain"
            android:textColor="#2196F3"
            android:textSize="14sp"/>

    </LinearLayout>

</LinearLayout>
```



![image-20231017180553612](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180553612.png)

## 1.2 布局美化 (登录 V2)

- 图片按钮
- 自定义 XML 图片
- selector XML 图片

```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ImageButton button = findViewById(R.id.iv_head);

        button.setOnClickListener(v -> Toast.makeText(MainActivity.this,"您点击了登陆图标",Toast.LENGTH_SHORT).show());

    }
```

```xml
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <solid android:color="#16646A64" />  <!-- 填充颜色 -->
    <stroke android:color="#000000" /> <!-- 边框颜色 -->
    <corners android:radius="10dp" />   <!-- 圆角半径 -->
</shape>

```

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" android:shape="rectangle">
    <solid
        android:color="#69DB8F"/>
    <stroke android:color="#7FEAAA"></stroke>
    <corners android:radius="5dp"/>
</shape>

```

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" android:shape="rectangle">
    <solid
        android:color="#B5407C"/>
    <stroke android:color="#9B1B5C"></stroke>
    <corners android:radius="5dp"/>
</shape>

```

```xml
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:state_pressed="true"
        android:drawable="@drawable/btn_press">
    </item>
    <item
        android:state_pressed="false"
        android:drawable="@drawable/btn_unpress">
    </item>
</selector>
```

```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#FFFFFF"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <!--头像-->
    <ImageButton
        android:id="@+id/iv_head"
        android:layout_width="70dp"
        android:layout_height="70dp"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="70dp"
        android:background="@drawable/avata"/>

    <!--用户名-->
    <EditText
        android:id="@+id/et_user_name"
        android:layout_width="fill_parent"
        android:layout_height="40dp"
        android:background="@drawable/rectangle_shape"
        android:layout_gravity="center_horizontal"
        android:layout_marginLeft="35dp"
        android:layout_marginRight="35dp"
        android:layout_marginTop="35dp"
        android:drawableLeft="@drawable/username"
        android:drawablePadding="10dp"
        android:gravity="center_vertical"
        android:hint="@string/usernameMain"
        android:paddingLeft="8dp"
        android:textColor="#a3a3a3"
        android:textSize="14sp"/>

    <!--密码-->
    <EditText
        android:id="@+id/et_psw"
        android:layout_width="fill_parent"
        android:layout_height="40dp"
        android:background="@drawable/rectangle_shape"
        android:layout_gravity="center_horizontal"
        android:layout_marginLeft="35dp"
        android:layout_marginRight="35dp"
        android:layout_marginTop="5dp"
        android:drawableLeft="@drawable/password"
        android:drawablePadding="10dp"
        android:gravity="center_vertical"
        android:hint="@string/passwordMain"
        android:inputType="textPassword"
        android:paddingLeft="8dp"
        android:textColor="#a3a3a3"
        android:singleLine="true"
        android:textSize="14sp"/>

    <!--登录-->
    <Button
        android:id="@+id/btn_login"
        android:layout_width="fill_parent"
        android:layout_height="40dp"
        android:layout_gravity="center_horizontal"
        android:layout_marginLeft="35dp"
        android:layout_marginRight="35dp"
        android:layout_marginTop="15dp"
        android:background="@drawable/btn_selector"
        android:text="@string/loginMain"
        android:textColor="@color/white"
        android:textSize="18sp"/>

    <!--注册 和 找回密码-->
    <LinearLayout
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:layout_marginLeft="35dp"
        android:layout_marginRight="35dp"
        android:layout_marginTop="8dp"
        android:gravity="center_horizontal"
        android:orientation="horizontal">

        <TextView
            android:layout_width="1dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:gravity="center_horizontal"
            android:padding="9dp"
            android:text="@string/registerMain"
            android:textColor="#2196F3"
            android:textSize="14sp"/>

        <TextView
            android:layout_width="1dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:gravity="center_horizontal"
            android:padding="9dp"
            android:text="@string/findPasswordMain"
            android:textColor="#2196F3"
            android:textSize="14sp"/>

    </LinearLayout>


</LinearLayout>
```



![image-20231017180604736](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180604736.png)

## 1.3 实战-注册页面

```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
```

```xml
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <solid android:color="#16646A64" />  <!-- 填充颜色 -->
    <stroke android:color="#000000" /> <!-- 边框颜色 -->
    <corners android:radius="10dp" />   <!-- 圆角半径 -->
</shape>

```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#FFFFFF"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <!--头像-->
    <ImageView
        android:layout_width="70dp"
        android:layout_height="70dp"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="70dp"
        android:background="@drawable/avata"/>

    <!--用户名-->
    <EditText
        android:layout_width="fill_parent"
        android:layout_height="40dp"
        android:background="@drawable/rectangle_shape"
        android:layout_gravity="center_horizontal"
        android:layout_marginLeft="35dp"
        android:layout_marginRight="35dp"
        android:layout_marginTop="35dp"
        android:drawableLeft="@drawable/username"
        android:drawablePadding="10dp"
        android:gravity="center_vertical"
        android:hint="@string/usernameMain"
        android:paddingLeft="8dp"
        android:textColor="#a3a3a3"
        android:textSize="14sp"/>

    <!--密码-->
    <EditText
        android:layout_width="fill_parent"
        android:layout_height="40dp"
        android:background="@drawable/rectangle_shape"
        android:layout_gravity="center_horizontal"
        android:layout_marginLeft="35dp"
        android:layout_marginRight="35dp"
        android:layout_marginTop="5dp"
        android:drawableLeft="@drawable/password"
        android:drawablePadding="10dp"
        android:gravity="center_vertical"
        android:hint="@string/passwordMain"
        android:inputType="textPassword"
        android:paddingLeft="8dp"
        android:textColor="#a3a3a3"
        android:singleLine="true"
        android:textSize="14sp"/>


    <EditText
        android:layout_width="fill_parent"
        android:layout_height="40dp"
        android:background="@drawable/rectangle_shape"
        android:layout_gravity="center_horizontal"
        android:layout_marginLeft="35dp"
        android:layout_marginRight="35dp"
        android:layout_marginTop="5dp"
        android:drawableLeft="@drawable/password"
        android:drawablePadding="10dp"
        android:gravity="center_vertical"
        android:hint="@string/passwordAgainMain"
        android:inputType="textPassword"
        android:paddingLeft="8dp"
        android:textColor="#a3a3a3"
        android:singleLine="true"
        android:textSize="14sp"/>


    <!--用户名-->
    <EditText
        android:layout_width="fill_parent"
        android:layout_height="40dp"
        android:background="@drawable/rectangle_shape"
        android:layout_gravity="center_horizontal"
        android:layout_marginLeft="35dp"
        android:layout_marginRight="35dp"
        android:layout_marginTop="5dp"
        android:drawableLeft="@drawable/username"
        android:drawablePadding="10dp"
        android:gravity="center_vertical"
        android:hint="@string/userMain"
        android:paddingLeft="8dp"
        android:textColor="#a3a3a3"
        android:textSize="14sp"/>

    <!--注册-->
    <Button
        android:layout_width="fill_parent"
        android:layout_height="40dp"
        android:layout_gravity="center_horizontal"
        android:layout_marginLeft="35dp"
        android:layout_marginRight="35dp"
        android:layout_marginTop="15dp"
        android:background="#03A9F4"
        android:text="@string/registerMain"
        android:textColor="@color/white"
        android:textSize="18sp"/>


</LinearLayout>
```



![image-20231017170001353](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017170001353.png)