# 注册

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

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128194053672.png" alt="image-20231128194053672" style="zoom:67%;" />