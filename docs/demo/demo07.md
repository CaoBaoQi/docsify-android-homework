# Listener

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:gravity="center"
        tools:context=".MainActivity">
    <Button
        android:id="@+id/main_btn_eventV1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
        android:text="@string/v1"/>
    <Button
            android:id="@+id/main_btn_eventV2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="@string/v2"/>
    <Button
            android:id="@+id/main_btn_eventV3"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="@string/v3"/>
    <Button
            android:id="@+id/main_btn_eventV4"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="@string/v4"/>


    <Button
            android:id="@+id/main_btn_eventV5"
            android:onClick="v5"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="@string/v5"/>



</LinearLayout>
```

```java
/**
 * OuterCustomListener
 *
 * @author Cola777jz
 * @date 2023/10/31 16:20
 * @since 1.0.0
 */
public class OuterCustomListener implements View.OnClickListener {
    private Context context;

    public OuterCustomListener(Context context) {
        super();
        this.context = context;
    }

    @Override
    public void onClick(View v) {
        Toast.makeText(context, "外部类 V3", Toast.LENGTH_SHORT).show();
    }
}
```

```java
/**
 * 启动
 *
 * @author cbq
 * @date 2023/11/1 16:46
 * @since 1.0.0
 */
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button v1 = findViewById(R.id.main_btn_eventV1);
        Button v2 = findViewById(R.id.main_btn_eventV2);
        Button v3 = findViewById(R.id.main_btn_eventV3);
        Button v4 = findViewById(R.id.main_btn_eventV4);

        v1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(MainActivity.this, "匿名内部类 V1", Toast.LENGTH_SHORT).show();

            }
        });

        v2.setOnClickListener(new InnerCustomListener());

        v3.setOnClickListener(new OuterCustomListener(MainActivity.this));

        v4.setOnClickListener(v -> {
            Toast.makeText(MainActivity.this, "Lambda 方式 | 匿名内部类 V4", Toast.LENGTH_SHORT).show();

        });
    }

    /**
     * 内部类
     */
    class InnerCustomListener implements View.OnClickListener{
        @Override
        public void onClick(View v) {
            Toast.makeText(MainActivity.this, "内部类 V2", Toast.LENGTH_SHORT).show();

        }
    }

    /**
     * 直接绑定到标签
     * @param view view
     */
    public void v5(View view) {
        Toast.makeText(MainActivity.this, "直接绑定到标签 V5", Toast.LENGTH_SHORT).show();
    }
}
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128202356112.png" alt="image-20231128202356112" style="zoom:80%;" />

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128202410191.png" alt="image-20231128202410191" style="zoom:80%;" />