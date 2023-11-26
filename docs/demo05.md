# Android 控件

## 一、普通对话框

```java
 @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button commonDialog = findViewById(R.id.btn_common_dialog);

        showCommonDialog(commonDialog);
    }
    
     /**
     * 普通对话框
     *
     * @param button commonDialog
     */
    public void showCommonDialog(Button button) {
        button.setOnClickListener(v -> {
            AlertDialog.Builder alertDialogBuilder = new AlertDialog.Builder(MainActivity.this);
            alertDialogBuilder
                    .setTitle("commonDialog")
                    .setIcon(R.drawable.ic_launcher_background)
                    .setMessage("恭喜您支付成功")
                    .setNegativeButton("取消", (dialog, which) -> Toast.makeText(MainActivity.this, "您单击了取消按钮", Toast.LENGTH_SHORT).show())
                    .setPositiveButton("确定", (dialog, which) -> Toast.makeText(MainActivity.this, "您单击了确定按钮", Toast.LENGTH_SHORT).show()).create().show();
        });
    }
```



```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical"
    android:gravity="center">
    
        <Button
        android:id="@+id/btn_common_dialog"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="5dp"
        android:text="普通对话框"
        android:background="@color/white"
        android:textColor="#A52C2C"
        android:textSize="15sp"/>

</LinearLayout>
```

![image-20231017180620980](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180620980.png)



![image-20231017180628715](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180628715.png)

## 二、列表对话框

### 2.1 单选对话框

```java
 @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button singleDialog = findViewById(R.id.btn_single_dialog);

        showSingleDialog(singleDialog );
    }
    
    /**
     * 单选对话框
     *
     * @param button singleDialog
     */
    public void showSingleDialog(Button button) {
        String[] items = {"男", "女"};
        boolean[] checkedItems = {true, false};

        button.setOnClickListener(v -> {
            AlertDialog.Builder alertDialogBuilder = new AlertDialog.Builder(MainActivity.this);
            alertDialogBuilder
                    .setTitle("单选对话框")
                    .setSingleChoiceItems(items, 0, (dialog, which) -> {
                        for (int i = 0; i < checkedItems.length; i++) {
                            checkedItems[i] = false;
                        }
                        checkedItems[which] = true;
                    })
                    .setNegativeButton("取消", (dialog, which) -> dialog.dismiss())
                    .setPositiveButton("确定", (dialog, which) -> {
                        String str = "";
                        for (int i = 0; i < checkedItems.length; i++) {
                            if (checkedItems[i]) {
                                str = items[i];
                            }
                        }
                        Toast.makeText(MainActivity.this, "您选择了" + str, Toast.LENGTH_SHORT).show();
                    }).create().show();
        });
    }
```



```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical"
    android:gravity="center">
    
        <Button
        android:id="@+id/btn_single_dialog"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="5dp"
        android:text="单选对话框"
        android:background="@color/white"
        android:textColor="#9D25B1"
        android:textSize="15sp"/>
    

</LinearLayout>
```



![image-20231017180638889](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180638889.png)



### 2.2 多选对话框

```java
 @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button multipleDialog = findViewById(R.id.btn_multiple_dialog);

        showMultipleDialog(multipleDialog );
    }
    
     /**
     * 多选对话框
     *
     * @param button multipleDialog
     */
    public void showMultipleDialog(Button button) {
        String[] items = {"数学", "语文", "英语", "政治"};
        boolean[] checkedItems = {false, true, false, false};

        button.setOnClickListener(v -> {
            AlertDialog.Builder alertDialogBuilder = new AlertDialog.Builder(MainActivity.this);
            alertDialogBuilder
                    .setTitle("多选对话框")
                    .setMultiChoiceItems(items, checkedItems, (dialog, which, isChecked) -> {
                        if (isChecked) {
                            checkedItems[which] = true;
                        } else {
                            checkedItems[which] = false;
                            Toast.makeText(MainActivity.this, "您取消了" + items[which], Toast.LENGTH_SHORT).show();
                        }
                    })
                    .setNegativeButton("取消", (dialog, which) -> dialog.dismiss())
                    .setPositiveButton("确定", (dialog, which) -> {
                        StringBuilder str = new StringBuilder();
                        for (int i = 0; i < checkedItems.length; i++) {
                            if (checkedItems[i]) {
                                str.append(items[i]);
                            }
                        }
                        Toast.makeText(MainActivity.this, "您选择了" + str, Toast.LENGTH_SHORT).show();
                    }).create().show();
        });
    }
```



```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical"
    android:gravity="center">
    
     <Button
        android:id="@+id/btn_multiple_dialog"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="5dp"
        android:text="多选对话框"
        android:background="@color/white"
        android:textColor="#E3316D"
        android:textSize="15sp"/>

</LinearLayout>
```



![image-20231017180648699](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180648699.png)

## 三、进度对话框

### 3.1 不带进度条的对话框

```java
 @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button simpleProcessDialog = findViewById(R.id.btn_simple_process_dialog);

        showSimpleProcessDialog(simpleProcessDialog );
    }
    
      /**
     * 不带进度条的对话框
     *
     * @param button simpleProcessDialog
     */
    public void showSimpleProcessDialog(Button button) {
        button.setOnClickListener(v -> {
            ProgressDialog progressDialog = new ProgressDialog(MainActivity.this);
            progressDialog.setTitle("不带进度条的对话框");
            progressDialog.setMessage("正在加载");
            progressDialog.show();
        });

    }
```



```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical"
    android:gravity="center">
    
      <Button
        android:id="@+id/btn_simple_process_dialog"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="5dp"
        android:text="不带进度条的对话框"
        android:background="@color/white"
        android:textColor="#6CBAF8"
        android:textSize="15sp"/>

</LinearLayout>
```



![image-20231017180658710](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180658710.png)

### 3.2 带进度条的对话框

```java
 @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button processDialog = findViewById(R.id.btn_process_dialog);

        showProcessDialog(processDialog );
    }
    
     /**
     * 带进度条的对话框
     *
     * @param button processDialog
     */
    public void showProcessDialog(Button button) {
        button.setOnClickListener(v -> {
            ProgressDialog dialog = new ProgressDialog(MainActivity.this);

            dialog.setProgressStyle(ProgressDialog.STYLE_HORIZONTAL);
            dialog.setTitle("带进度条的对话框");
            dialog.setMessage("正在加载");
            dialog.setMax(200);
            dialog.show();
            new Thread(() -> {
                for (int i = 0; i <= 200; i++) {
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        throw new RuntimeException(e);
                    }
                    dialog.setProgress(i);
                }
            }).start();
        });
    }
```



```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical"
    android:gravity="center">
    
     <Button
        android:id="@+id/btn_process_dialog"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="5dp"
        android:text="带进度条的对话框"
        android:background="@color/white"
        android:textColor="#B69C4D"
        android:textSize="15sp"/>
    

</LinearLayout>
```



![image-20231017180707485](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180707485.png)

## 四、实战-支付对话框

```java
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
                        AlertDialog.Builder sucBuilder = new AlertDialog.Builder(MainActivity.this);
                        sucBuilder
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
```



```XML
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



![image-20231017180716977](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017180716977.png)

## 五、实战-个人中心

```java
private RelativeLayout rlOrder, rlAddress, rlLogout;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        rlOrder = findViewById(R.id.rl_order);
        rlAddress = findViewById(R.id.rl_address);
        rlLogout = findViewById(R.id.rl_logout);

        rlOrder.setOnClickListener(view -> {
            dialog("下一步将查询个人订单");
        });
        rlAddress.setOnClickListener(view -> {
            dialog("下一步将编辑个人地址");
        });
        rlLogout.setOnClickListener(view -> {
            dialog("下一步将退出登录");
        });
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
```

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

![image-20231017171328078](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017171328078.png)



## 六、列表控件

### 6.1 下拉列表 Spinner

```java
 private String[] boys = {"CBH", "SongWenJie", "WangWenZhao"};
    private String[] girls = {"CB", "CBQ"};
    private Spinner spB;
    private Spinner spG;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        spB = findViewById(R.id.sp_choice_b);
        spB.setAdapter(new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, boys));

        spG = findViewById(R.id.sp_choice_g);
        spG.setAdapter(new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, girls));

    }
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:gravity="center_vertical"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="请选择(girl)  "
            android:textSize="16sp" />

        <Spinner
            android:id="@+id/sp_choice_g"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />
    </LinearLayout>

    <View
        android:layout_width="match_parent"
        android:layout_height="100dp"
        android:background="@color/white"/>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:orientation="vertical">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="请选择(boy)  "
            android:textSize="16sp" />

        <Spinner
            android:id="@+id/sp_choice_b"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />
    </LinearLayout>


</LinearLayout>
```

![image-20231017171347184](https://yong-gan-niu-niu-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231017171347184.png)