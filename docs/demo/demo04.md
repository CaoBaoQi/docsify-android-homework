# Dialog 弹窗

## 普通对话框

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
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
            android:text="@string/commonDialog"
            android:background="@color/white"
            android:textColor="#A52C2C"
            android:textSize="15sp"/>
</LinearLayout>
```

```java
 	/**
     * 普通对话框
     */
    private Button commonDialog;
commonDialog = findViewById(R.id.btn_common_dialog);
        showCommonDialog(commonDialog);

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
}

```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128200248633.png" alt="image-20231128200248633" style="zoom:80%;" />

## 单选对话框
```xml
    <Button
            android:id="@+id/btn_single_dialog"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/singleDialog"
            android:background="@color/white"
            android:textColor="#9D25B1"
            android:textSize="15sp"/>
```

```java
    /**
     * 单选对话框
     */
    private Button singleDialog;

        singleDialog = findViewById(R.id.btn_single_dialog);
        showSingleDialog(singleDialog);

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

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128200324263.png" alt="image-20231128200324263" style="zoom:80%;" />


## 多选对话框
```xml
    <Button
            android:id="@+id/btn_multiple_dialog"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/multipleDialog"
            android:background="@color/white"
            android:textColor="#E3316D"
            android:textSize="15sp"/>
```

```java
    /**
     * 多选对话框
     */
    private Button multipleDialog;
        multipleDialog = findViewById(R.id.btn_multiple_dialog);
        showMultipleDialog(multipleDialog);

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

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128200403403.png" alt="image-20231128200403403" style="zoom:80%;" />


## 不带进度条的对话框
```xml
    <Button
            android:id="@+id/btn_simple_process_dialog"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/simpleProcessDialog"
            android:background="@color/white"
            android:textColor="#6CBAF8"
            android:textSize="15sp"/>
```

```java
    /**
     * 不带进度条的对话框
     */
    private Button simpleProcessDialog;
        simpleProcessDialog = findViewById(R.id.btn_simple_process_dialog);
        showSimpleProcessDialog(simpleProcessDialog);

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

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128200509775.png" alt="image-20231128200509775" style="zoom:80%;" />


## 带进度条的对话框
```xml
    <Button
            android:id="@+id/btn_process_dialog"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/processDialog"
            android:background="@color/white"
            android:textColor="#B69C4D"
            android:textSize="15sp"/>
```

```java
    /**
     * 带进度条的对话框
     */
    private Button processDialog;
        processDialog = findViewById(R.id.btn_process_dialog);
        showProcessDialog(processDialog);

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
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128200454518.png" alt="image-20231128200454518" style="zoom:80%;" />
