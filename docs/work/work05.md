# 支付

- dialog 通知栏与 Toat 的基本使用

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              xmlns:app="http://schemas.android.com/apk/res-auto"
              xmlns:tools="http://schemas.android.com/tools"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:orientation="vertical"
              tools:context=".MainActivity">

    <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginVertical="15dp"
            android:layout_marginBottom="8dp"
            android:gravity="center"
            android:text="付款详情"
            android:textSize="30sp"/>

    <View
            android:layout_width="match_parent"
            android:layout_height="0.5dp"
            android:background="#A8A8A8"/>

    <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="60dp"
            android:layout_marginTop="10dp"
            android:layout_marginBottom="10dp"
            android:orientation="horizontal"
            android:paddingLeft="10dp">

        <ImageView
                android:layout_width="60dp"
                android:layout_height="60dp"
                android:src="@drawable/ali_pay"/>

        <TextView
                android:layout_width="wrap_content"
                android:layout_height="match_parent"
                android:gravity="center_vertical"
                android:paddingLeft="20dp"
                android:text="支付宝"
                android:textColor="#A6A6A6"
                android:textSize="25sp"/>

    </LinearLayout>

    <View
            android:layout_width="match_parent"
            android:layout_height="0.5dp"
            android:background="#A8A8A8"/>

    <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="60dp"
            android:layout_marginTop="10dp"
            android:layout_marginBottom="10dp"
            android:orientation="horizontal"
            android:paddingLeft="10dp">

        <ImageView
                android:layout_width="60dp"
                android:layout_height="60dp"
                android:src="@drawable/wx_pay"/>

        <TextView
                android:layout_width="wrap_content"
                android:layout_height="match_parent"
                android:gravity="center_vertical"
                android:paddingLeft="20dp"
                android:text="微信支付"
                android:textColor="#A6A6A6"
                android:textSize="25sp"/>

    </LinearLayout>


    <View
            android:layout_width="match_parent"
            android:layout_height="0.5dp"
            android:background="#A8A8A8"/>

    <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="60dp"
            android:layout_marginTop="10dp"
            android:layout_marginBottom="10dp"
            android:orientation="horizontal"
            android:paddingLeft="10dp">

        <ImageView
                android:layout_width="60dp"
                android:layout_height="60dp"
                android:src="@drawable/card_pay"/>

        <TextView
                android:layout_width="wrap_content"
                android:layout_height="match_parent"
                android:gravity="center_vertical"
                android:paddingLeft="20dp"
                android:text="银行卡"
                android:textColor="#A6A6A6"
                android:textSize="25sp"/>
    </LinearLayout>

    <View
            android:layout_width="match_parent"
            android:layout_height="0.5dp"
            android:background="#A8A8A8"/>

    <TextView
            android:id="@+id/tv_sum"
            android:layout_width="match_parent"
            android:layout_height="40dp"
            android:gravity="center_vertical|right"
            android:text="需付款？50元"
            android:textColor="#A8A8A8"
            android:paddingRight="10dp"
            android:textSize="20sp"/>

    <View
            android:layout_width="match_parent"
            android:layout_height="0.5dp"
            android:background="#A8A8A8"/>

    <Button
            android:id="@+id/btn_submit"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="确认支付"
            android:textSize="20sp"/>

</LinearLayout>
```

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button submit = findViewById(R.id.btn_submit);


        submit.setOnClickListener(v -> {
            AlertDialog.Builder payBbuilder = new AlertDialog.Builder(MainActivity.this);

            TextView textV = findViewById(R.id.tv_sum);
            textV.setText("需付款？ 100 元");

            payBbuilder
                    .setTitle("Ask")
                    .setIcon(R.drawable.manner)
                    .setMessage("是否支付")
                    .setPositiveButton("确认支付", (dialog, which) -> {
                        AlertDialog.Builder sucbuilder = new AlertDialog.Builder(MainActivity.this);
                        sucbuilder
                                .setTitle("恭喜您支付成功")
                                .setPositiveButton("确定", (dialog1, which1) -> {
                                    Toast.makeText(MainActivity.this, "欢迎下次光临", Toast.LENGTH_SHORT).show();
                                })
                                .create().show();
                    })
                    .setNegativeButton("取消支付", (dialog, which) -> Toast.makeText(MainActivity.this, "您取消了支付", Toast.LENGTH_SHORT).show())
                    .create().show();
        });
    }
}
```



<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128194520578.png" alt="image-20231128194520578" style="zoom:80%;" />