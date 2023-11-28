# 个人中心

- 多种方式实现事件监听
- 按钮点击事件

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              xmlns:app="http://schemas.android.com/apk/res-auto"
              xmlns:tools="http://schemas.android.com/tools"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:orientation="vertical"
              tools:context=".MainActivity">

    <LinearLayout
            android:id="@+id/ll_head"
            android:layout_width="match_parent"
            android:layout_height="200dp"
            android:background="#3F51B5"
            android:orientation="vertical">

        <ImageButton
                android:onClick="login"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_gravity="center_horizontal"
                android:scaleType="centerCrop"
                android:layout_marginTop="40dp"
                android:background="#0000"
                android:src="@drawable/avata"/>

        <TextView
                android:id="@+id/tv_login"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="center_horizontal"
                android:layout_marginTop="10dp"
                android:text="单击登录"
                android:textColor="@color/white"
                android:textSize="16sp"/>
    </LinearLayout>

    <RelativeLayout
            android:id="@+id/rl_order"
            android:layout_width="match_parent"
            android:layout_height="45dp"
            android:background="#F7F8F8"
            android:gravity="center_vertical"
            android:paddingLeft="10dp"
            android:paddingRight="10dp">

        <ImageView
                android:id="@+id/iv_order"
                android:layout_width="20dp"
                android:layout_height="20dp"
                android:layout_centerVertical="true"
                android:layout_marginLeft="25dp"
                android:src="@drawable/password"/>

        <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_centerVertical="true"
                android:layout_marginLeft="25dp"
                android:layout_toRightOf="@+id/iv_order"
                android:text="我的订单"
                android:textColor="#A3A3A3"
                android:textSize="16sp"/>

        <ImageView
                android:layout_width="15dp"
                android:layout_height="15dp"
                android:layout_alignParentRight="true"
                android:layout_centerVertical="true"
                android:layout_marginRight="25dp"
                android:src="@drawable/username"/>

        <View
                android:layout_width="match_parent"
                android:layout_height="1dp"
                android:background="#E3E3E3"/>

    </RelativeLayout>
    <RelativeLayout
            android:id="@+id/rl_address"
            android:layout_width="match_parent"
            android:layout_height="45dp"
            android:background="#F7F8F8"
            android:gravity="center_vertical"
            android:paddingLeft="10dp"
            android:paddingRight="10dp">

        <ImageView
                android:id="@+id/iv_address"
                android:layout_width="20dp"
                android:layout_height="20dp"
                android:layout_centerVertical="true"
                android:layout_marginLeft="25dp"
                android:src="@drawable/password"/>

        <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_centerVertical="true"
                android:layout_marginLeft="25dp"
                android:layout_toRightOf="@+id/iv_address"
                android:text="我的地址"
                android:textColor="#A3A3A3"
                android:textSize="16sp"/>

        <ImageView
                android:layout_width="15dp"
                android:layout_height="15dp"
                android:layout_alignParentRight="true"
                android:layout_centerVertical="true"
                android:layout_marginRight="25dp"
                android:src="@drawable/username"/>

        <View
                android:layout_width="match_parent"
                android:layout_height="1dp"
                android:background="#E3E3E3"/>

    </RelativeLayout>
    <RelativeLayout
            android:id="@+id/rl_logout"
            android:layout_width="match_parent"
            android:layout_height="45dp"
            android:background="#F7F8F8"
            android:gravity="center_vertical"
            android:paddingLeft="10dp"
            android:paddingRight="10dp">

        <ImageView
                android:id="@+id/iv_logout"
                android:layout_width="20dp"
                android:layout_height="20dp"
                android:layout_centerVertical="true"
                android:layout_marginLeft="25dp"
                android:src="@drawable/password"/>

        <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_centerVertical="true"
                android:layout_marginLeft="25dp"
                android:layout_toRightOf="@+id/iv_logout"
                android:text="退出登录"
                android:textColor="#A3A3A3"
                android:textSize="16sp"/>

        <ImageView
                android:layout_width="15dp"
                android:layout_height="15dp"
                android:layout_alignParentRight="true"
                android:layout_centerVertical="true"
                android:layout_marginRight="25dp"
                android:src="@drawable/username"/>

        <View
                android:layout_width="match_parent"
                android:layout_height="1dp"
                android:background="#E3E3E3"/>

    </RelativeLayout>


</LinearLayout>
```

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        RelativeLayout rlOrder = findViewById(R.id.rl_order);
        RelativeLayout rlAddress = findViewById(R.id.rl_address);
        RelativeLayout rlLogout = findViewById(R.id.rl_logout);

        rlOrder.setOnClickListener(view -> dialog("下一步将查询个人订单"));
        rlAddress.setOnClickListener(view -> dialog("下一步将编辑个人地址"));
        rlLogout.setOnClickListener(view -> dialog("下一步将退出登录"));
    }

    public void login(View view) {
        dialog("下一步将跳转到登陆页面");
    }


    private void dialog(String msg) {
        AlertDialog.Builder builder = new AlertDialog.Builder(this);

        builder
                .setMessage(msg)
                .setPositiveButton("确定", (dialogInterface, i) -> {
                    Toast.makeText(this, msg, Toast.LENGTH_SHORT).show();
                }).create().show();
    }
}
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128194259432.png" alt="image-20231128194259432" style="zoom:80%;" />