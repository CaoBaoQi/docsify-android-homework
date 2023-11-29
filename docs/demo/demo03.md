# Activity 活动

## MainActivity

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
            android:id="@+id/btn_login"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/login"
            android:background="@color/white"
            android:textColor="#A52C2C"
            android:textSize="15sp"/>

    <Button
            android:id="@+id/btn_register"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/register"
            android:background="@color/white"
            android:textColor="#9D25B1"
            android:textSize="15sp"/>

    <Button
            android:id="@+id/btn_user_center"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/user_center"
            android:background="@color/white"
            android:textColor="#E3316D"
            android:textSize="15sp"/>




</LinearLayout>
```

```java
/**
 * 启动
 *
 * @author cbq
 * @date 2023/11/1 16:46
 * @since 1.0.0
 */
public class MainActivity extends AppCompatActivity implements View.OnClickListener{

    /**
     * 登录
     */
    private Button btn_login;
    /**
     * 注册
     */
    private Button btn_register;
    /**
     * 用户中心
     */
    private Button btn_user_center;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btn_login = findViewById(R.id.btn_login);
        btn_register = findViewById(R.id.btn_register);
        btn_user_center = findViewById(R.id.btn_user_center);

        btn_login.setOnClickListener(this);
        btn_register.setOnClickListener(this);
        btn_user_center.setOnClickListener(this);
    }

    /**
     * Called when a view has been clicked.
     * @param v The view that was clicked.
     */
    @Override
    public void onClick(View v) {
        int id = v.getId();
        if (id == R.id.btn_login) {
            startActivity(new Intent(this, LoginActivity.class));
        } else if (id == R.id.btn_register) {
            startActivity(new Intent(this, RegisterActivity.class));
        } else if (id == R.id.btn_user_center) {
            startActivity(new Intent(this, UserCenterActivity.class));
        }
    }
}
```

## LoginActivity

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".activity.LoginActivity">

    <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Login"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

```java
/**
 * 登录
 *
 * @author cbq
 * @date 2023/11/1 16:46
 * @since 1.0.0
 */
public class LoginActivity extends AppCompatActivity {
    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);

        Toast.makeText(this, "登录 Activity", Toast.LENGTH_SHORT).show();
    }
}
```



## RegisterActivivy

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".activity.RegisterActivity">

    <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Register"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

```java
/**
 * 注册
 *
 * @author cbq
 * @date 2023/11/1 16:46
 * @since 1.0.0
 */
public class RegisterActivity extends AppCompatActivity {
    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_register);

        Toast.makeText(this, "注册 Activity", Toast.LENGTH_SHORT).show();

    }
}
```



## UserCenterActivity

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".activity.UserCenterActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="UserCenter"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

```java
/**
 * 用户中心
 *
 * @author cbq
 * @date 2023/11/1 16:56
 * @since 1.0.0
 */
public class UserCenterActivity extends AppCompatActivity {

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_user_center);

        Toast.makeText(this, "用户中心 Activity", Toast.LENGTH_SHORT).show();

    }
}
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128195625919.png" alt="image-20231128195625919" style="zoom:80%;" />