# 登录

- 基础控件 (ImageView、EditText、Button) 的使用
- 基础布局 (LinearLayout)

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
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

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128193045638.png" alt="image-20231128193045638" style="zoom:67%;" />