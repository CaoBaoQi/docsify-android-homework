# 登录V2

- 美化 (按钮按压变化)
- 按钮点击事件

```xml
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <solid android:color="#16646A64" />  <!-- 填充颜色 -->
    <stroke android:color="#000000" /> <!-- 边框颜色 -->
    <corners android:radius="10dp" />   <!-- 圆角半径 -->
</shape>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:state_pressed="false"
        android:drawable="@drawable/btn_unpress">
    </item>
    <item
            android:state_pressed="true"
            android:drawable="@drawable/btn_press">
    </item>
</selector>
```

```xml
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <solid android:color="@color/btn_press"/>
    <stroke android:color="@color/btn_press"/>
    <corners android:radius="15dp"/>
</shape>
```

```xml
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <solid android:color="@color/btn_unpress"/>
    <stroke android:color="@color/btn_unpress"/>
    <corners android:radius="5dp"/>
</shape>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
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

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ImageButton button = findViewById(R.id.iv_head);

        button.setOnClickListener(v -> Toast.makeText(MainActivity.this,"您点击了登陆图标",Toast.LENGTH_SHORT).show());
    }
}
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128193851813.png" alt="image-20231128193851813" style="zoom:67%;" />