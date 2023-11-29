# 记事本

| 信息                                                         | 项目文档                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 姓名: **曹宝琪**<br />学号: **2309312102**<br />班级: **计算机专升本 2301 班**<br />专业:**计算机科学与技术** | Github:  https://github.com/CaoBaoQi/android-demo<br />文档: http://182.92.71.87:81/ |

## 介绍

> 功能方面: 
>
> - 使用 `CountDownTimer` 实现启动页以及倒计时 (3s) 和点击跳过功能
> - 自定义主题与多标签切换
> - 页面透明感实现(毛玻璃)
> - SQLite 数据管理
> - 多 Adapter 、menu 的使用
> - 用户登录、注册、记住我功能实现
> - 笔记模糊检索
> - `AlarmReceiver` 服务类实现通知
> - 日记、待办事项的添加修改删除
> - 多控件多布局使用
> - Intent 数据传递

### 启动页

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:fitsSystemWindows="true"
        android:background="@color/white"
        android:orientation="vertical"
        tools:context=".activity.SplashActivity">
    <androidx.cardview.widget.CardView
            android:layout_marginTop="56dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:cardElevation="0dp"
            android:backgroundTint="#DF7676"
            android:layout_margin="20dp"
            android:layout_alignParentEnd="true"
            app:cardCornerRadius="25dp">
        <TextView
                android:id="@+id/tv_second"
                android:layout_width="80dp"
                android:layout_height="50dp"
                android:textColor="@color/white"
                android:gravity="center"
                android:text="3s"
                android:textSize="16sp" />
    </androidx.cardview.widget.CardView>
    <androidx.cardview.widget.CardView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerInParent="true"
            app:cardCornerRadius="25dp">
        <ImageView
                android:layout_width="110dp"
                android:layout_height="110dp"
                android:src="@drawable/note" />

    </androidx.cardview.widget.CardView>
    <LinearLayout
            android:layout_marginTop="56dp"
            android:layout_centerHorizontal="true"
            android:layout_width="wrap_content"
            android:gravity="center"
            android:orientation="vertical"
            android:layout_height="wrap_content">
        <TextView
                android:layout_marginTop="175dp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:textSize="16sp"
                android:textStyle="bold"
                android:text="@string/cbq" />
        <TextView
                android:layout_marginTop="10dp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:textSize="16sp"
                android:textStyle="bold"
                android:text="@string/about_cbq" />
    </LinearLayout>
</RelativeLayout>
```

```java
/**
 * 启动页
 *
 * @author cbq
 * @date 2023/11/20 22:45
 * @since 1.0.0
 */
public class SplashActivity extends AppCompatActivity {

    private TextView tv_second;
    private CountDownTimer countDownTimer;
    private long timeLeftInMillis = 4000;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_splash);

        Toast.makeText(this, "点击时间即可跳过", Toast.LENGTH_SHORT).show();

        tv_second = findViewById(R.id.tv_second);
        tv_second.setOnClickListener(v -> {
            startActivity(new Intent(this, LoginActivity.class));
            finish();
        });

        startCountdown();
    }

    private void startCountdown() {
        countDownTimer = new CountDownTimer(timeLeftInMillis, 1000) {
            @Override
            public void onTick(long millisUntilFinished) {
                timeLeftInMillis = millisUntilFinished;
                int secondsRemaining = (int) (millisUntilFinished / 1000);
                tv_second.setText(secondsRemaining + " s");
            }

            @Override
            public void onFinish() {
                startActivity(new Intent(SplashActivity.this, LoginActivity.class));
                finish();
            }

        }.start();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        if (countDownTimer != null) {
            countDownTimer.cancel();
        }
    }
}
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231129203930590.png" alt="image-20231129203930590" style="zoom:50%;" />

### 自定义主题与多标签切换

```xml
<?xml version="1.0" encoding="utf-8"?><!-- MainActivity布局文件 -->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:fitsSystemWindows="true"
        android:orientation="vertical">
    <!-- 自定义顶部工具条 -->
    <androidx.appcompat.widget.Toolbar
            android:layout_width="match_parent"
            android:layout_height="?attr/actionBarSize"
            android:background="@color/light_grey">
        <!-- 笔记标签 -->
        <TextView
                android:id="@+id/note"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/note"
                android:layout_gravity="center"
                android:textSize="20sp"
                android:textColor="@color/black" />
        <!-- 待办标签 -->
        <TextView
                android:id="@+id/in_abeyance"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/in_abeyance"
                android:layout_gravity="center"
                android:layout_marginStart="62dp"
                android:textSize="20sp"
                android:textColor="@color/dark_grey" />
        <!-- 关于我 -->
        <TextView
                android:id="@+id/about_me"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/about_me"
                android:layout_gravity="center"
                android:layout_marginStart="62dp"
                android:textSize="20sp"
                android:textColor="@color/dark_grey" />

    </androidx.appcompat.widget.Toolbar>

    <!-- ViewPager2 用于盛放 Fragment -->
    <androidx.viewpager2.widget.ViewPager2
            android:id="@+id/mainViewPager2"
            android:layout_width="match_parent"
            android:layout_height="0dp"
            android:layout_weight="1"
            android:background="@color/light_grey" />
</LinearLayout>


```

```java
public class MainActivity extends AppCompatActivity implements View.OnClickListener {
    /**
     * ViewPager2
     */
    ViewPager2 viewPager;
    /**
     * 顶部 笔记 标签
     */
    TextView note;
    /**
     * 顶部 待办 标签
     */
    TextView in_abeyance;
    /**
     * 顶部 关于我 标签
     */
    TextView about_me;
    /**
     * 回收站按钮
     */
    ImageView recycle_bin;
    /**
     * 标志当前显示笔记页面或者待办页面
     * 0 为笔记 | 1 为待办
     */
    public static int status = 0;

    // 初始化
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        getWindow().setSoftInputMode(WindowManager.LayoutParams.SOFT_INPUT_ADJUST_PAN);
        super.onCreate(savedInstanceState);

        Window window = getWindow();
        window.clearFlags(WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS);
        window.addFlags(WindowManager.LayoutParams.FLAG_DRAWS_SYSTEM_BAR_BACKGROUNDS);
        window.setStatusBarColor(getResources().getColor(R.color.light_grey));
        window.getDecorView().setSystemUiVisibility(View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN | View.SYSTEM_UI_FLAG_LIGHT_STATUS_BAR);
        setContentView(R.layout.activity_main);

        note = findViewById(R.id.note);
        note.setOnClickListener(this);
        in_abeyance = findViewById(R.id.in_abeyance);
        in_abeyance.setOnClickListener(this);
        about_me = findViewById(R.id.about_me);

        initViewPager();
    }

    @Override
    protected void onResume() {
        super.onResume();

        viewPager.setCurrentItem(status);
    }

    @Override
    protected void onPause() {
        super.onPause();

        status = viewPager.getCurrentItem();
    }

    /**
     * 初始化 ViewPager2
     */
    private void initViewPager() {
        viewPager = findViewById(R.id.mainViewPager2);

        List<Fragment> fragmentList = new ArrayList<>();
        fragmentList.add(NoteFragment.newInstance());
        fragmentList.add(InAbeyanceFragment.newInstance());
        fragmentList.add(AboutMeFragment.newInstance());

        MyFragmentPagerAdapter myFragmentPagerAdapter =
                new MyFragmentPagerAdapter(getSupportFragmentManager(),
                        getLifecycle(), fragmentList);

        viewPager.setAdapter(myFragmentPagerAdapter);
        viewPager.registerOnPageChangeCallback(new ViewPager2.OnPageChangeCallback() {
            @SuppressLint("ResourceAsColor")
            @Override
            public void onPageSelected(int position) {
                super.onPageSelected(position);
                changeFragment(position);
            }
        });
    }

    /**
     * 切换 Fragment
     *
     * @param position position
     */
    @SuppressLint("NonConstantResourceId")
    private void changeFragment(int position) {
        if (position == R.id.note) {
            viewPager.setCurrentItem(0);
        } else if (position == R.id.in_abeyance) {
            viewPager.setCurrentItem(1);
        } else if (position == R.id.about_me) {
            viewPager.setCurrentItem(2);
        } else {
            selected(position);
        }
    }

    /**
     * 选中标签
     * @param position position
     */
    private void selected(int position) {
        switch (position) {
            case 0:
                note.setTextColor(note.getResources().getColor(R.color.black));
                in_abeyance.setTextColor(in_abeyance.getResources().getColor(R.color.dark_grey));
                about_me.setTextColor(about_me.getResources().getColor(R.color.dark_grey));
                break;
            case 1:
                in_abeyance.setTextColor(in_abeyance.getResources().getColor(R.color.black));
                note.setTextColor(note.getResources().getColor(R.color.dark_grey));
                about_me.setTextColor(about_me.getResources().getColor(R.color.dark_grey));
                break;
            case 2:
                about_me.setTextColor(about_me.getResources().getColor(R.color.black));
                note.setTextColor(note.getResources().getColor(R.color.dark_grey));
                in_abeyance.setTextColor(in_abeyance.getResources().getColor(R.color.dark_grey));
                break;
            default:
                Log.d("MainActivity", "selected: " + position);
                break;
        }
    }

    /**
     * onClick
     *
     * @param view The view that was clicked.
     */
    @Override
    public void onClick(View view) {
        changeFragment(view.getId());
    }
}
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231129204018399.png" alt="image-20231129204018399" style="zoom:50%;" />

### SQLite 数据管理

```java
/**
 *  数据库 DBHelper
 *
 * @author cbq
 * @date 2023/11/20 22:39
 * @since 1.0.0
 */
public class DBHelper extends SQLiteOpenHelper {
    /**
     * 数据库名称
     */
    private static final String DBNAME = "note_book.db";
    /**
     * 实例 instance
     */
    private static DBHelper instance;

    public static synchronized DBHelper getInstance(Context context) {
        if (instance == null) {
            instance = new DBHelper(context, DBNAME, null, 1);
        }
        return instance;
    }

    private DBHelper(@Nullable Context context, @Nullable String name, @Nullable SQLiteDatabase.CursorFactory factory, int version) {
        super(context, name, factory, version);
    }

    @Override
    public void onCreate(SQLiteDatabase sqLiteDatabase) {
        noteTable(sqLiteDatabase);
        inAbeyanceTable(sqLiteDatabase);
        accountTable(sqLiteDatabase);
    }

    @Override
    public void onUpgrade(SQLiteDatabase sqLiteDatabase, int i, int i1) {
    }


    /**
     * 创建 note 表并插入一条默认数据
     * @param sqLiteDatabase sqLiteDatabase
     */
    private static void noteTable(SQLiteDatabase sqLiteDatabase) {
        String sql = "CREATE TABLE note(" +
                "_id integer PRIMARY KEY AUTOINCREMENT," +
                "title text," +
                "content text," +
                "date_created text," +
                "date_updated text," +
                "recycle_status integer DEFAULT 0)";

        String insert_default_note = "INSERT INTO note " +
                "(title, content, date_created, date_updated)" +
                "VALUES" +
                "(\"About\", \"1.学校: 晋中学院 \n" +
                "2.专业: 计算机科学与技术 \n" +
                "3.班级: 计算机专升本 2301 班 \n" +
                "4.姓名: 曹宝琪 \n" +
                "5.学号: 2309312102 \n" +
                "6.江天一色 ~ \n" +
                "7.email: 1203952894@qq.com \"," +
                "\"11月20日 上午 11:11\",\"11月20日 上午 11:11\")";

        sqLiteDatabase.execSQL(sql);
        sqLiteDatabase.execSQL(insert_default_note);
    }

    /**
     * 创建 in_abeyance 表
     * @param sqLiteDatabase sqLiteDatabase
     */
    private static void inAbeyanceTable(SQLiteDatabase sqLiteDatabase) {
        String sql = "CREATE TABLE in_abeyance (" +
                "_id integer PRIMARY KEY AUTOINCREMENT," +
                "content text," +
                "date_remind text," +
                "status integer DEFAULT 0," +
                "date_created text)";

        sqLiteDatabase.execSQL(sql);
    }

    /**
     * 创建 账户 表
     * @param sqLiteDatabase sqLiteDatabase
     */
    private static void accountTable(SQLiteDatabase sqLiteDatabase) {
        String sql = "CREATE TABLE account (" +
                "_id integer PRIMARY KEY AUTOINCREMENT," +
                "username text," +
                "email text," +
                "password text)";

        String insert_default_account = "INSERT INTO account " +
                "(username, email, password)" +
                "VALUES" +
                "('CaoBaoQi', '1203952894@qq.com','123321')";

        sqLiteDatabase.execSQL(sql);
        sqLiteDatabase.execSQL(insert_default_account);
    }

}

```


#### Account 账户 DB


```java
/**
 * 账户 OP
 *
 * @author cbq
 * @date 2023/11/25 16:35
 * @since 1.0.0
 */
public class AccountDBOperator {

    /**
     * 注册用户
     * @param context context
     * @return count (0 失败 | 1 成功)
     */
    public static int register(Context context, Account account) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getWritableDatabase();

        ContentValues values = new ContentValues();

        values.put("username", account.getUsername());
        values.put("email", account.getEmail());
        values.put("password", account.getPassword());

        String nullColumnHack = "values(null,?,?,?)";

        int count = (int) database.insert("account", nullColumnHack, values);
        database.close();
        return count;
    }

    /**
     * 根据用户名或邮箱查找
     * @param context context
     * @param text 用户名或邮箱
     * @return Account
     */
    @SuppressLint("Range")
    public static Account findAccount(Context context, String text) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getWritableDatabase();
        Account account = null;

        String sql = "SELECT * FROM account WHERE username=? or email=?";
        String[] selectionArgs = {text, text};

        Cursor cursor = database.rawQuery(sql, selectionArgs);
        if (cursor.moveToNext()) {
            int user_id = cursor.getInt(cursor.getColumnIndex("_id"));
            String username = cursor.getString(cursor.getColumnIndex("username"));
            String email = cursor.getString(cursor.getColumnIndex("email"));
            String password = cursor.getString(cursor.getColumnIndex("password"));

            account = new Account(user_id, username, email, password);
        }
        cursor.close();
        database.close();
        return account;
    }
}
```


#### InAbeyance 待办事项 DB

```java
/**
 * 待办事项 OP
 *
 * @author cbq
 * @date 2023/11/25 16:04
 * @since 1.0.0
 */
public class InAbeyanceDBOperator {
    /**
     * 添加待办
     * @param context context
     * @param inAbeyance InAbeyance
     * @return _id
     */
    public static int add_in_abeyance(Context context, InAbeyance inAbeyance) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getWritableDatabase();

        String sql = "INSERT INTO in_abeyance " +
                "(content, date_remind, date_created)" +
                "VALUES" +
                "('" + inAbeyance.getContent() + "','" +
                inAbeyance.getDate_remind() + "','" +
                inAbeyance.getDate_created() +
                "')";

        database.execSQL(sql);
        String get_id = "SELECT last_insert_rowid() FROM in_abeyance";
        Cursor cursor = database.rawQuery(get_id, null);
        int _id = -1;
        if (cursor.moveToFirst()) {
            _id = cursor.getInt(0);
        }
        cursor.close();
        database.close();
        return _id;
    }

    /**
     * 获取全部待办信息
     * @param context context
     * @return List<InAbeyance>
     */
    public static List<InAbeyance> getInAbeyanceData(Context context) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getWritableDatabase();

        String sql = "SELECT * FROM in_abeyance " +
                "ORDER BY _id DESC";

        Cursor cursor = database.rawQuery(sql, null);
        List<InAbeyance> inAbeyanceList = new ArrayList<>();

        while (cursor.moveToNext()) {
            int _id = cursor.getInt(0);
            String content = cursor.getString(1);
            String date_remind = cursor.getString(2);
            int status = cursor.getInt(3);
            InAbeyance inAbeyance = new InAbeyance(_id, content, date_remind, status);
            inAbeyanceList.add(inAbeyance);
        }
        cursor.close();
        database.close();
        return inAbeyanceList;
    }

    /**
     * 根据关键字查询待办
     * @param context context
     * @param keyWord 关键字
     * @return List<InAbeyance>
     */
    public static List<InAbeyance> queryInAbeyanceData(Context context, String keyWord) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getReadableDatabase();

        String sql = "SELECT * FROM in_abeyance " +
                "WHERE content LIKE \"%" + keyWord + "%\"" +
                "ORDER BY _id DESC";

        Cursor cursor = database.rawQuery(sql, null);// 执行sql语句
        List<InAbeyance> inAbeyanceList = new ArrayList<>();

        while (cursor.moveToNext()) {
            int _id = cursor.getInt(0);
            String content = cursor.getString(1);
            String date_remind = cursor.getString(2);
            int status = cursor.getInt(3);
            InAbeyance inAbeyance = new InAbeyance(_id, content, date_remind, status);
            inAbeyanceList.add(inAbeyance);
        }
        cursor.close();
        database.close();
        return inAbeyanceList;
    }

    /**
     * 根据 id 删除待办
     * @param context context
     * @param _id _id
     */
    public static void deleteInAbeyance(Context context, int _id) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getWritableDatabase();

        String sql = "delete FROM in_abeyance WHERE " +
                "_id = " + _id;

        database.execSQL(sql);
        database.close();
    }

    /**
     * 修改待办状态
     * @param context context
     * @param _id _id
     */
    public static void changeInAbeyanceStatus(Context context, int _id) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getWritableDatabase();

        String sql = "UPDATE in_abeyance SET " +
                "status = 1 - status WHERE " +
                "_id = " + _id;

        database.execSQL(sql);
        database.close();
    }

    /**
     * 更新待办
     * @param context context
     * @param inAbeyance InAbeyance
     */
    public static void updateInAbeyance(Context context, InAbeyance inAbeyance) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getWritableDatabase();

        String sql = "UPDATE in_abeyance SET " +
                "content = '" + inAbeyance.getContent() + "'," +
                "date_remind = '" + inAbeyance.getDate_remind() + "'" +
                " WHERE " +
                "_id = " + inAbeyance.get_id();

        database.execSQL(sql);
        database.close();
    }
}
```


#### NoteBook 笔记 DB
```java
/**
 * 笔记 OP
 *
 * @author cbq
 * @date 2023/11/20 22:41
 * @since 1.0.0
 */
public class NoteBookDBOperator {

    /**
     * 获取全部 Note 数据
     * @param context context
     * @param recycle_status 0 未回收 | 1 已回收
     * @return List<Note>
     */
    public static List<Note> getNotesData(Context context, int recycle_status) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getReadableDatabase();

        String sql = "SELECT * FROM note " +
                "WHERE recycle_status = " + recycle_status +
                " ORDER BY date_updated DESC";

        List<Note> notes = new ArrayList<>();

        Cursor cursor = database.rawQuery(sql, null);
        while (cursor.moveToNext()) {
            int _id = cursor.getInt(0);
            String title = cursor.getString(1);
            String content = cursor.getString(2);
            String date_created = cursor.getString(3);
            String date_updated = cursor.getString(4);
            notes.add(new Note(_id, title, content, date_created, date_updated));
        }
        cursor.close();
        database.close();
        return notes;
    }

    /**
     * 查询符合关键字的 Note 数据
     * @param context context
     * @param keyWord 关键字
     * @param recycle_status 0 未回收 | 1 已回收
     * @return List<Note>
     */
    public static List<Note> queryNotesData(Context context,String keyWord, int recycle_status) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getReadableDatabase();

        String sql = "SELECT * FROM note " +
                "WHERE (title LIKE \"%" + keyWord + "%\" " +
                "OR content LIKE \"%" + keyWord + "%\") " +
                "AND recycle_status = " + recycle_status +
                " ORDER BY date_updated DESC";

        List<Note> notes = new ArrayList<>();

        Cursor cursor = database.rawQuery(sql, null);
        while (cursor.moveToNext()) {
            int _id = cursor.getInt(0);
            String title = cursor.getString(1);
            String content = cursor.getString(2);
            String date_created = cursor.getString(3);
            String date_updated = cursor.getString(4);
            notes.add(new Note(_id, title, content, date_created, date_updated));
        }
        cursor.close();
        database.close();
        return notes;
    }

    /**
     * 添加一条笔记
     * @param context context
     * @param note Note
     */
    public static void addNote(Context context, Note note) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getWritableDatabase();

        String date = DateUtil.getCurrentTime();
        String sql = "INSERT INTO note" +
                "(title, content, date_created, date_updated)" +
                "VALUES" +
                "('" + note.getTitle() + "','" +
                note.getContent() + "','" +
                date + "','" + date + "')";

        database.execSQL(sql);
        database.close();
    }

    /**
     * 更新笔记
     * @param context 更新笔记
     * @param note Note
     */
    public static void updateNote(Context context, Note note) {
        DBHelper dbHelper = DBHelper.getInstance(context);

        SQLiteDatabase database = dbHelper.getWritableDatabase();
        String date = DateUtil.getCurrentTime();

        String sql = "UPDATE note " +
                "SET title = '" + note.getTitle() + "'," +
                "content = '" + note.getContent() + "'," +
                "date_updated = '" + date + "'" +
                "WHERE _id = " + note.get_id();

        database.execSQL(sql);
        database.close();
    }

    /**
     * 更改笔记状态
     * @param context context
     * @param _id _id
     */
    public static void changeNoteRecycleStatus(Context context, int _id) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getWritableDatabase();

        String sql = "UPDATE note " +
                "SET recycle_status = 1 - recycle_status " +
                "WHERE _id = " + _id;

        database.execSQL(sql);
        database.close();
    }

    /**
     * 根据 id 删除一条笔记
     * @param context context
     * @param _id _id
     */
    public static void deleteNote(Context context, int _id) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getWritableDatabase();

        String sql = "DELETE FROM note " +
                "WHERE _id = " + _id;

        database.execSQL(sql);
        database.close();
    }

}
```

### 多 Adapter 、menu 的使用

#### 笔记

```xml
<?xml version="1.0" encoding="utf-8"?><!-- 这是笔记编辑界面的布局文件 -->
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:fitsSystemWindows="true"
        tools:context=".activity.EditActivity">

    <!-- 顶部工具条 -->
    <androidx.appcompat.widget.Toolbar
            android:id="@+id/top_bar"
            android:layout_width="match_parent"
            android:layout_height="?attr/actionBarSize"
            android:background="@color/white">
        <!-- 返回按钮 -->
        <ImageView
                android:id="@+id/back"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:background="@drawable/ic_baseline_arrow_back_ios_24"
                android:layout_marginStart="25dp" />
        <!-- 完成按钮 -->
        <ImageView
                android:id="@+id/accomplish"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="end"
                android:layout_marginEnd="25dp"
                android:background="@drawable/ic_accomplish_24" />
    </androidx.appcompat.widget.Toolbar>

    <!-- 创建时间 -->
    <TextView
            android:id="@+id/date_created"
            android:layout_below="@id/top_bar"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginStart="30dp"
            android:layout_marginTop="10dp"
            android:layout_marginBottom="10dp"
            android:textSize="15sp"
            android:textColor="@color/dark_grey" />
    <!-- 一个隐藏文本框存放传入的id -->
    <TextView
            android:id="@+id/note_id"
            android:layout_width="0dp"
            android:layout_height="0dp" />
    <!-- 标题编辑框 -->
    <EditText
            android:id="@+id/note_title_edit"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="@string/note_title_edit"
            android:inputType="text"
            android:layout_below="@id/date_created"
            android:textSize="30sp"
            android:textStyle="bold"
            android:padding="5dp"
            android:layout_marginStart="25dp"
            android:textColor="@color/black"
            android:background="@color/white"
            android:imeOptions="actionNext" />

    <!-- 滚动条，使得滑动没有那么卡顿 -->
    <ScrollView
            android:id="@+id/content_scroll"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:fillViewport="true"
            android:layout_below="@id/note_title_edit">

        <!-- 内容编辑框 -->
        <EditText
                android:id="@+id/note_content_edit"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_marginStart="25dp"
                android:padding="5dp"
                android:background="@color/white"
                android:gravity="top"
                android:hint="@string/note_content_edit"
                android:inputType="textMultiLine"
                android:textColor="@color/black"
                android:textSize="22sp" />
    </ScrollView>
</RelativeLayout>

```

```java
/**
 * 笔记 Adapter
 *
 * @author cbq
 * @date 2023/11/20 22:50
 * @since 1.0.0
 */
public class NoteRecyclerViewAdapter extends RecyclerView.Adapter<NoteRecyclerViewAdapter.MyRecyclerViewHolder> {
    /**
     *  Note List
     */
    List<Note> notes;
    /**
     * context
     */
    Context context;
    /**
     * note item 单击事件监听器
     */
    OnItemClickListener onItemClickListener;

    public NoteRecyclerViewAdapter(List<Note> notes, Context context) {
        this.notes = notes;
        this.context = context;
    }

    @NonNull
    @Override
    public MyRecyclerViewHolder onCreateViewHolder(
            @NonNull ViewGroup parent, int viewType) {
        View itemView = View.inflate(context, R.layout.item_note, null);
        return new MyRecyclerViewHolder(itemView);
    }

    @Override
    public void onBindViewHolder(@NonNull MyRecyclerViewHolder holder,
                                 @SuppressLint("RecyclerView") int position) {
        String title = notes.get(position).getTitle();
        String content = notes.get(position).getContent();

        if (title.length() == 0) {
            holder.note_title.setVisibility(View.GONE);
        } else {
            holder.note_title.setVisibility(View.VISIBLE);
            holder.note_title.setText(title);
        }
        if (content.length() == 0) {
            holder.note_content.setVisibility(View.GONE);
        } else {
            holder.note_content.setVisibility(View.VISIBLE);
            holder.note_content.setText(content);
        }
        holder.note_date.setText(notes.get(position).getDate_updated());

        holder.itemView.setOnClickListener(view -> {
            if (onItemClickListener != null) {
                String title1 = notes.get(position).getTitle();
                String content1 = notes.get(position).getContent();
                String date_created = notes.get(position).getDate_created();
                String note_id = notes.get(position).get_id() + "";
                onItemClickListener.onItemClick(position, title1, content1, date_created, note_id);
            }
        });

        holder.itemView.setOnLongClickListener(view -> {
            recycleNote(position);
            return true;
        });
    }

    @Override
    public int getItemCount() {
        return notes.size();
    }

    /**
     * 回收一条笔记
     * @param position position
     */
    public void recycleNote(int position) {
        int _id = notes.get(position).get_id();

        NoteBookDBOperator.changeNoteRecycleStatus(context, _id);
        notifyItemRemoved(position);

        notes.remove(position);
        notifyItemRangeChanged(position, notes.size() - position);
        Toast.makeText(context, "移入回收站",Toast.LENGTH_SHORT).show();
    }

    public void setOnItemClickListener(OnItemClickListener listener) {
        this.onItemClickListener = listener;
    }

    /**
     * ViewHolder
     */
    public static class MyRecyclerViewHolder extends RecyclerView.ViewHolder {
        /**
         * 笔记标题
         */
        final TextView note_title;
        /**
         * 笔记内容
         */
        final TextView note_content;
        /**
         * 笔记修改日期
         */
        final TextView note_date;

        public MyRecyclerViewHolder(@NonNull View itemView) {
            super(itemView);
            note_title = itemView.findViewById(R.id.note_title);
            note_content = itemView.findViewById(R.id.note_content);
            note_date = itemView.findViewById(R.id.note_date);
        }
    }

    public interface OnItemClickListener {
        void onItemClick(int position, String title, String content, String date_created, String note_id);
    }
}
```
```java
/**
 * 页面 Adapter
 *
 * @author cbq
 * @date 2023/11/20 22:49
 * @since 1.0.0
 */
public class MyFragmentPagerAdapter extends FragmentStateAdapter {
    /**
     * Fragment List
     */
    List<Fragment> fragmentList;

    public MyFragmentPagerAdapter(@NonNull FragmentManager fragmentManager,
                                  @NonNull Lifecycle lifecycle,
                                  List<Fragment> fragmentList) {
        super(fragmentManager, lifecycle);
        this.fragmentList = fragmentList;
    }
    @NonNull
    @Override
    public Fragment createFragment(int position) {
        return fragmentList.get(position);
    }

    @Override
    public int getItemCount() {
        return fragmentList.size();
    }
}
```

```java
/**
 * 编辑 EditActivity
 *
 * @author cbq
 * @date 2023/11/20 22:45
 * @since 1.0.0
 */
public class EditActivity extends AppCompatActivity {
    /**
     * 传来的数据
     */
    Bundle bundle;
    /**
     * 创建日期文本框
     */
    TextView date_created;
    /**
     * 一个隐藏的文本框用于标记 note 的 _id
     */
    TextView note_id;
    /**
     * 标题编辑框
     */
    EditText title;
    /**
     * 内容编辑框
     */
    EditText content;
    /**
     * 返回按钮
     */
    ImageView backButton;
    /**
     * 完成按钮
     */
    ImageView accomplishButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        Window window = getWindow();
        window.clearFlags(WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS);
        window.addFlags(WindowManager.LayoutParams.FLAG_DRAWS_SYSTEM_BAR_BACKGROUNDS);
        window.setStatusBarColor(getResources().getColor(R.color.white));
        window.getDecorView().setSystemUiVisibility(View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN | View.SYSTEM_UI_FLAG_LIGHT_STATUS_BAR);
        setContentView(R.layout.activity_edit);

        note_id = findViewById(R.id.note_id);
        title = findViewById(R.id.note_title_edit);
        content = findViewById(R.id.note_content_edit);
        backButton = findViewById(R.id.back);
        accomplishButton = findViewById(R.id.accomplish);

        backButton.setOnClickListener(view -> {
            MainActivity.status = 0;
            EditActivity.this.onBackPressed();
        });

        accomplishButton.setOnClickListener(view -> {
            String s_id = note_id.getText().toString();
            String title = EditActivity.this.title.getText().toString();
            String content = EditActivity.this.content.getText().toString();

            Note note;
            if ("".equals(s_id) && (!"".equals(title) || !"".equals(content))) {
                note = new Note(title, content);
                addNote(note);
            } else if (!"".equals(s_id) && (!"".equals(title) || !"".equals(content))) {
                int _id = Integer.parseInt(s_id);
                note = new Note(_id, title, content);
                updateNote(note);
            }

            EditActivity.this.onBackPressed();
        });

        bundle = getIntent().getExtras();

        if (bundle != null) {
            date_created = findViewById(R.id.date_created);
            title.setText(bundle.getString("note_title"));
            content.setText(bundle.getString("note_content"));
            note_id.setText(bundle.getString("note_id"));
            String tips = "创建于：" + bundle.getString("date_created");
            date_created.setText(tips);
            bundle.clear();
        }
    }

    /**
     * 添加一条笔记
     *
     * @param note Note
     */
    public void addNote(Note note) {
        NoteBookDBOperator.addNote(this, note);
        Toast.makeText(this, "添加成功", Toast.LENGTH_SHORT).show();
    }

    /**
     * 更新一条笔记
     *
     * @param note Note
     */
    public void updateNote(Note note) {
        NoteBookDBOperator.updateNote(this, note);
        Toast.makeText(this, "更新成功", Toast.LENGTH_SHORT).show();
    }
}
```
<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231129204133984.png" alt="image-20231129204133984" style="zoom:50%;" />

#### 待办事项

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="300dp"
        android:layout_height="70dp"
        tools:context=".activity.InAbeyanceDialogActivity"
        android:orientation="vertical">

    <TextView
            android:id="@+id/in_abeyance_id"
            android:layout_width="0dp"
            android:layout_height="0dp" />

    <EditText
            android:id="@+id/in_abeyance_edittext"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:inputType="text"
            android:background="@color/white"
            android:hint="输入待办内容"
            android:textSize="20dp" />

    <RelativeLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

        <LinearLayout
                android:id="@+id/set_remind"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:orientation="horizontal"
                android:background="@drawable/setting_remind_backgroung"
                android:layout_marginTop="10dp">

            <ImageView
                    android:id="@+id/setting_status"
                    android:layout_width="15dp"
                    android:layout_height="15dp"
                    android:src="@drawable/alarm"
                    android:layout_gravity="center_vertical" />

            <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="设置提醒"
                    android:textSize="15dp"
                    android:textColor="@color/black"
                    android:gravity="center_vertical" />
        </LinearLayout>

        <TextView
                android:id="@+id/date_remind_show"
                android:layout_toRightOf="@id/set_remind"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:textSize="15dp"
                android:layout_marginTop="10dp"
                android:paddingTop="4dp"
                android:paddingStart="8dp"
                android:textColor="@color/black" />

        <TextView
                android:id="@+id/input_accomplish"
                android:layout_alignParentEnd="true"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="完成"
                android:textColor="@color/mid_grey"
                android:textSize="15dp"
                android:paddingTop="14dp" />
    </RelativeLayout>
</LinearLayout>

```

```java
/**
 * 待办事项 InAbeyanceDialogActivity
 *
 * @author cbq
 * @date 2023/11/20 22:53
 * @since 1.0.0
 */
public class InAbeyanceDialogActivity extends AppCompatActivity {
    /**
     * 待办的 _id
     */
    TextView _id;
    /**
     * 代办的内容
     */
    EditText content;
    /**
     * 设置提醒按钮
     */
    LinearLayout set_remind;
    /**
     * 闹钟设置状态
     */
    ImageView setting_status;
    /**
     * 提醒日期
     */
    TextView date_remind;
    /**
     * 完成按钮
     */
    TextView accomplish;
    /**
     * 传入的数据
     */
    Bundle bundle;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_in_abeyance_dialog);

        _id = findViewById(R.id.in_abeyance_id);
        content = findViewById(R.id.in_abeyance_edittext);
        set_remind = findViewById(R.id.set_remind);

        set_remind.setOnClickListener(view -> {
            if (!"".equals(date_remind.getText().toString())) {
                setting_status.setSelected(true);
            }
            Calendar startTime = Calendar.getInstance();
            startTime.set(Calendar.SECOND, 0);
            Calendar endTime = Calendar.getInstance();
            endTime.set(2030, 12, 31, 23, 59);

            TimePickerView pickerView = new TimePickerView.Builder(
                    InAbeyanceDialogActivity.this,
                    (date, v) -> {
                        String time = DateUtil.getFormatTime(date);
                        setting_status.setSelected(true);
                        date_remind.setText(time);
                    })
                    .setType(new boolean[]{true, true, true, true, true, false})
                    .setCancelText("取消")
                    .setCancelColor(getResources().getColor(R.color.yellow))
                    .setSubmitText("确定")
                    .setSubmitColor(getResources().getColor(R.color.yellow))
                    .setTitleText("设置提醒日期")
                    .setTitleBgColor(getResources().getColor(R.color.white))
                    .isCyclic(true)
                    .setRangDate(startTime, endTime)
                    .isCenterLabel(false)
                    .setOutSideCancelable(true)
                    .build();
            pickerView.show();
        });
        setting_status = findViewById(R.id.setting_status);
        date_remind = findViewById(R.id.date_remind_show);
        accomplish = findViewById(R.id.input_accomplish);
        accomplish.setOnClickListener(view -> {
            String content_str = content.getText().toString();
            String date_remind_str = date_remind.getText().toString();
            String _id_str = _id.getText().toString();

            InAbeyance inAbeyance;

            if ("".equals(_id_str)) {
                String date_created_str = DateUtil.getCurrentTime();
                inAbeyance = new InAbeyance(content_str, date_remind_str, date_created_str);
                int _id = addInAbeyance(inAbeyance);
                if (!"".equals(date_remind_str)) {
                    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.S) {
                        AlarmUtil.setAlarm(getApplicationContext(),
                                DateUtil.getTimeMillis(date_remind_str),
                                _id, content_str);
                    }
                }
                Toast.makeText(getApplicationContext(), "添加成功", Toast.LENGTH_SHORT).show();
            } else {
                int _id_int = Integer.parseInt(_id_str);
                inAbeyance = new InAbeyance(_id_int, content_str,
                        date_remind_str);
                updateInAbeyance(inAbeyance);
                if (!"".equals(date_remind_str)) {
                    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.S) {
                        AlarmUtil.setAlarm(getApplicationContext(),
                                DateUtil.getTimeMillis(date_remind_str),
                                _id_int, content_str);
                    }
                }
                Toast.makeText(getApplicationContext(), "更新成功", Toast.LENGTH_SHORT).show();
            }
            MainActivity.status = 1;
            onBackPressed();
        });
        accomplish.setClickable(false);
        content.requestFocus();
        InputMethodManager imm = (InputMethodManager) getApplicationContext().getSystemService(Context.INPUT_METHOD_SERVICE);
        imm.toggleSoftInput(0, InputMethodManager.HIDE_NOT_ALWAYS);
        content.addTextChangedListener(new TextWatcher() {
            @Override
            public void beforeTextChanged(CharSequence charSequence, int i, int i1, int i2) {
            }

            @Override
            public void onTextChanged(CharSequence charSequence, int i, int i1, int i2) {
            }

            @Override
            public void afterTextChanged(Editable editable) {
                EditText editText = InAbeyanceDialogActivity.this.content;
                TextView textView = InAbeyanceDialogActivity.this.accomplish;
                String content = editText.getText().toString();
                if ("".equals(content)) {
                    textView.setTextColor(getResources().getColor(R.color.mid_grey));
                    textView.setClickable(false);
                } else {
                    textView.setTextColor(getResources().getColor(R.color.yellow));
                    textView.setClickable(true);
                }
            }
        });
        bundle = getIntent().getExtras();
        if (bundle != null) {
            _id.setText(bundle.getString("_id"));
            content.setText(bundle.getString("content"));
            content.setSelection(content.getText().length());
            if (!"".equals(bundle.getString("date_remind"))) {
                setting_status.setSelected(true);
                date_remind.setText(bundle.getString("date_remind"));
            }
        }
    }

    /**
     * 添加一条待办
     *
     * @param inAbeyance InAbeyance
     * @return _id
     */
    public int addInAbeyance(InAbeyance inAbeyance) {
        return InAbeyanceDBOperator.add_in_abeyance(getApplicationContext(), inAbeyance);
    }

    /**
     * 更新一条待办
     *
     * @param inAbeyance InAbeyance
     */
    public void updateInAbeyance(InAbeyance inAbeyance) {
        InAbeyanceDBOperator.updateInAbeyance(getApplicationContext(), inAbeyance);
    }
}

```

```java
/**
 * 待办事项 Adapter
 *
 * @author cbq
 * @date 2023/11/20 22:48
 * @since 1.0.0
 */
public class InAbeyanceRecyclerViewAdapter extends RecyclerView.Adapter<InAbeyanceRecyclerViewAdapter.ViewHolder> {
    /**
     * 待办数据
     */
    List<InAbeyance> inAbeyances;
    /**
     * context
     */
    Context context;
    /**
     *  InAbeyance item 单击事件监听接口
     */
    OnItemClickListener onItemClickListener;

    public InAbeyanceRecyclerViewAdapter(List<InAbeyance> inAbeyances, Context context) {
        this.inAbeyances = inAbeyances;
        this.context = context;
    }

    @NonNull
    @Override
    public ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View itemView = LayoutInflater.from(parent.getContext())
                .inflate(R.layout.item_in_abeyance, parent, false);
        return new ViewHolder(itemView);
    }

    @Override
    public void onBindViewHolder(@NonNull ViewHolder holder,
                                 @SuppressLint("RecyclerView") int position) {

        /*
        * 设置待办完成状态 (默认为不勾选)
        * status为 1 则代表已完成
        * */
        holder.accomplish_status
                .setSelected(inAbeyances.get(position).getStatus() == 1);
        
        holder.parent_of_accomplish_status.setOnClickListener(
                view -> {
                    updateInabeyanceStatus(position); // 更新完成状态
                });

        holder.in_abeyance_content.setText(inAbeyances.get(position).getContent());
        if (!"".equals(inAbeyances.get(position).getDate_remind())) {
            holder.hasRemind.setSelected(true);
            holder.date_remind.setText(inAbeyances.get(position).getDate_remind());
        } else {
            holder.hasRemind.setSelected(false);
            holder.date_remind.setText("");
        }

        holder.in_abeyance_main.setOnLongClickListener(view -> {
            deleteInAbeyance(position);
            return true;
        });

        holder.in_abeyance_main.setOnClickListener(view -> {
            InAbeyance inAbeyance = inAbeyances.get(position);
            onItemClickListener.OnItemClick(
                    position, inAbeyance.get_id() + "",
                    inAbeyance.getContent(), inAbeyance.getDate_remind());
        });
    }

    @Override
    public int getItemCount() {
        return inAbeyances.size();
    }

    /**
     * 这是继承自 RecyclerView.ViewHolder 的
     * 自定义的 ViewHolder
     * 也是 InAbeyanceAdapter 的内部类
     */
    public class ViewHolder extends RecyclerView.ViewHolder {
        /**
         * 待办完成状态选择框的容器
         */
        private final LinearLayout parent_of_accomplish_status;
        /**
         * 待办完成状态
         */
        private final ImageView accomplish_status;
        /**
         * 待办信息主要布局
         */
        private final LinearLayout in_abeyance_main;
        /**
         * 待办内容
         */
        private final TextView in_abeyance_content;
        /**
         * 待办是否有提醒
         */
        private final ImageView hasRemind;
        /**
         * 待办提醒日期
         */
        private final TextView date_remind;

        public ViewHolder(@NonNull View itemView) {
            super(itemView);
            parent_of_accomplish_status = itemView.findViewById(R.id.in_abeyance_status);
            accomplish_status = itemView.findViewById(R.id.in_abeyance_check_box);
            in_abeyance_main = itemView.findViewById(R.id.in_abeyance_main);
            in_abeyance_content = itemView.findViewById(R.id.in_abeyance_content);
            hasRemind = itemView.findViewById(R.id.in_abeyance_alarm);
            date_remind = itemView.findViewById(R.id.date_remind);
        }
    }

    /**
     * 更新待办的完成状态
     * @param position position
     */
    public void updateInabeyanceStatus(int position) {
        int _id = inAbeyances.get(position).get_id();

        inAbeyances.get(position).
                setStatus(1 - inAbeyances.get(position).getStatus());

        notifyItemChanged(position);
        InAbeyanceDBOperator.changeInAbeyanceStatus(context, _id);
    }

    /**
     * 删除一条待办
     * @param position position
     */
    public void deleteInAbeyance(int position) {
        int _id = inAbeyances.get(position).get_id();

        String date_remind = inAbeyances.get(position).getDate_remind();
        if (!"".equals(date_remind)) {
            AlarmUtil.cancelAlarm(context.getApplicationContext(), _id);
        }

        InAbeyanceDBOperator.deleteInAbeyance(context, _id);
        inAbeyances.remove(position);
        notifyItemRemoved(position);

        notifyItemRangeChanged(position, inAbeyances.size() - position);
        Toast.makeText(context, "删除成功", Toast.LENGTH_SHORT).show();
    }

    public void setOnItemClickListener(OnItemClickListener onItemClickListener) {
        this.onItemClickListener = onItemClickListener;
    }

    public interface OnItemClickListener {
        void OnItemClick(int position, String _id, String content, String date_remind);
    }
}
```



#### 回收站

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231129204244195.png" alt="image-20231129204244195" style="zoom:50%;" />

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".activity.RecycleBinActivity"
        android:fitsSystemWindows="true"
        android:orientation="vertical">
    <!-- 自定义顶部工具栏 -->
    <androidx.appcompat.widget.Toolbar
            android:layout_width="match_parent"
            android:layout_height="?attr/actionBarSize"
            android:background="@color/light_grey">

        <ImageView
                android:id="@+id/back_of_recycle_bin"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:src="@drawable/ic_baseline_arrow_back_ios_24"
                android:layout_gravity="start" />
        <!-- 标题 -->
        <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="回收站"
                android:textSize="20sp"
                android:textColor="@color/black"
                android:layout_gravity="center" />
    </androidx.appcompat.widget.Toolbar>

    <!-- 盛放搜索框和回收笔记 -->
    <RelativeLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:background="@color/light_grey"

            >

        <!-- 笔记搜索输入框 -->
        <EditText
                android:id="@+id/search_recycle_note_editText"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:background="@drawable/my_edittext"
                android:drawableStart="@drawable/ic_baseline_search_24"
                android:drawablePadding="15dp"
                android:layout_marginLeft="20dp"
                android:layout_marginRight="20dp"
                android:hint="@string/search_note"
                android:inputType="text"
                android:singleLine="true"
                android:imeOptions="actionSearch" />

        <!-- RecyclerView用于列出笔记条目信息 -->
        <androidx.recyclerview.widget.RecyclerView
                android:id="@+id/recycle_note_recyclerview"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_below="@id/search_recycle_note_editText"
                android:padding="12dp" />
    </RelativeLayout>
</LinearLayout>
```

```java
/**
 * 回收站 RecycleBinActivity
 *
 * @author cbq
 * @date 2023/11/20 22:55
 * @since 1.0.0
 */
public class RecycleBinActivity extends AppCompatActivity {
    /**
     * 存放回收的笔记数据 Note List
     */
    List<Note> notes;
    /**
     * 返回按钮
     */
    ImageView back;
    /**
     * 回收笔记搜索框
     */
    EditText recycle_note_search;
    /**
     * recyclerView
     */
    RecyclerView recyclerView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        Window window = getWindow();
        window.clearFlags(WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS);
        window.addFlags(WindowManager.LayoutParams.FLAG_DRAWS_SYSTEM_BAR_BACKGROUNDS);
        window.setStatusBarColor(getResources().getColor(R.color.light_grey));
        window.getDecorView().setSystemUiVisibility(View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN | View.SYSTEM_UI_FLAG_LIGHT_STATUS_BAR);
        setContentView(R.layout.activity_recycle_bin);
        back = findViewById(R.id.back_of_recycle_bin);

        back.setOnClickListener(view -> RecycleBinActivity.this.onBackPressed());

        recycle_note_search = findViewById(R.id.search_recycle_note_editText);
        recycle_note_search.addTextChangedListener(new TextWatcher() {
            @Override
            public void beforeTextChanged(CharSequence charSequence, int i, int i1, int i2) {
            }

            @Override
            public void onTextChanged(CharSequence charSequence, int i, int i1, int i2) {
            }

            @Override
            public void afterTextChanged(Editable editable) {
                String keyWord = RecycleBinActivity.this
                        .recycle_note_search.getText().toString();
                notes = findNotesByKeyWord(keyWord);
                bindData();
            }
        });
        notes = getAllNotes();
        bindData();
    }

    public void bindData() {
        recyclerView = findViewById(R.id.recycle_note_recyclerview);
        StaggeredGridLayoutManager layoutManager =
                new StaggeredGridLayoutManager(2, LinearLayout.VERTICAL);
        recyclerView.setLayoutManager(layoutManager);
        RecycledNoteRecyclerViewAdapter adapter =
                new RecycledNoteRecyclerViewAdapter(notes, this);
        recyclerView.setAdapter(adapter);
    }

    /**
     * 查询全部已被回收的数据
     *
     * @return List<Note>
     */
    public List<Note> getAllNotes() {
        return NoteBookDBOperator.getNotesData(this, 1);
    }

    /**
     * 按照关键字查询已被回收的笔记
     *
     * @param keyWord 关键字
     * @return List<Note>
     */
    public List<Note> findNotesByKeyWord(String keyWord) {
        return NoteBookDBOperator.queryNotesData(this, keyWord, 1);
    }
}
```

```java
/**
 * 回收笔记 Adapter
 *
 * @author cbq
 * @date 2023/11/20 22:50
 * @since 1.0.0
 */
public class RecycledNoteRecyclerViewAdapter extends
        RecyclerView.Adapter<NoteRecyclerViewAdapter.MyRecyclerViewHolder> {

    /**
     * 存放已被回收的笔记
     */
    List<Note> notes;
    /**
     * context
     */
    Context context;

    public RecycledNoteRecyclerViewAdapter(List<Note> notes, Context context) {
        this.notes = notes;
        this.context = context;
    }

    @NonNull
    @Override
    public NoteRecyclerViewAdapter.MyRecyclerViewHolder
    onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View itemView = View.inflate(context, R.layout.item_note, null);
        return new NoteRecyclerViewAdapter.MyRecyclerViewHolder(itemView);
    }

    @Override
    public void onBindViewHolder(
            @NonNull NoteRecyclerViewAdapter.MyRecyclerViewHolder holder,
            @SuppressLint("RecyclerView") int position) {

        String title = notes.get(position).getTitle();
        String content = notes.get(position).getContent();

        if (title.length() == 0) {
            holder.note_title.setVisibility(View.GONE);
        } else {
            holder.note_title.setVisibility(View.VISIBLE);
            holder.note_title.setText(title);
        }
        if (content.length() == 0) {
            holder.note_content.setVisibility(View.GONE);
        } else {
            holder.note_content.setVisibility(View.VISIBLE);
            holder.note_content.setText(content);
        }
        holder.note_date.setText(notes.get(position).getDate_updated());

        holder.itemView.setOnClickListener(view -> restoreNote(position));

        holder.itemView.setOnLongClickListener(view -> {
            deleteNote(position);
            return true;
        });
    }

    @Override
    public int getItemCount() {
        return notes.size();
    }

    /**
     * 还原一条笔记
     * @param position position
     */
    public void restoreNote(int position) {
        int _id = notes.get(position).get_id();

        NoteBookDBOperator.changeNoteRecycleStatus(context, _id);

        notifyItemRemoved(position);
        notes.remove(position);

        notifyItemRangeChanged(position, notes.size() - position);
        Toast.makeText(context, "恢复成功", Toast.LENGTH_SHORT).show();
    }

    /**
     * 删除一条笔记
     * @param position position
     */
    public void deleteNote(int position) {
        int _id = notes.get(position).get_id();

        NoteBookDBOperator.deleteNote(context, _id);

        notifyItemRemoved(position);
        notes.remove(position);

        notifyItemRangeChanged(position, notes.size() - position);
        Toast.makeText(context, "删除成功", Toast.LENGTH_SHORT).show();
    }
}

```


### 用户登录、注册、记住我功能实现

#### 登录
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.appcompat.widget.LinearLayoutCompat
        android:background="#f9f4dc"
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        tools:ignore="ContentDescription"
        tools:context=".activity.LoginActivity">

    <androidx.appcompat.widget.Toolbar
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            app:title="@string/app_name"
            android:background="@color/teal_200"
            app:subtitleTextColor="@color/white"/>

    <TextView
            android:layout_marginTop="15dp"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textStyle="bold"
            android:textSize="20sp"
            android:text="@string/login"
            android:textColor="@color/black"
            android:gravity="center"/>

    <androidx.appcompat.widget.LinearLayoutCompat
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical"
            android:layout_margin="26dp">

        <androidx.appcompat.widget.LinearLayoutCompat
                android:layout_width="match_parent"
                android:background="@drawable/edit_backfround"
                android:paddingLeft="10dp"
                android:paddingRight="10dp"
                android:layout_height="50dp">

            <ImageView
                    android:scaleType="fitCenter"
                    android:layout_width="30dp"
                    android:layout_height="30dp"
                    android:layout_gravity="center_vertical"
                    android:src="@drawable/username"/>

            <EditText
                    android:id="@+id/login_activity_et_username"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:layout_marginStart="10dp"
                    android:hint="@string/input_name"
                    android:textSize="14sp"
                    android:text="@string/default_name"
                    android:background="@null" android:autofillHints="" android:inputType="textEmailAddress|text"/>


        </androidx.appcompat.widget.LinearLayoutCompat>

        <androidx.appcompat.widget.LinearLayoutCompat
                android:layout_marginTop="10dp"
                android:layout_width="match_parent"
                android:background="@drawable/edit_backfround"
                android:paddingLeft="10dp"
                android:paddingRight="10dp"
                android:layout_height="50dp">

            <ImageView
                    android:layout_width="30dp"
                    android:layout_height="30dp"
                    android:layout_gravity="center_vertical"
                    android:src="@drawable/password"/>

            <EditText
                    android:id="@+id/login_activity_et_pwd"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:layout_marginStart="10dp"
                    android:hint="@string/input_pwd"
                    android:text="@string/default_pwd"
                    android:textSize="14sp"
                    android:background="@null" android:autofillHints="" android:inputType="textPassword"/>


        </androidx.appcompat.widget.LinearLayoutCompat>

        <RelativeLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content">

            <CheckBox
                    android:id="@+id/login_activity_cb_save_pwd"
                    android:layout_width="wrap_content"
                    android:text="@string/save_pwd"
                    android:textColor="@color/teal_200"
                    android:layout_centerVertical="true"
                    android:layout_height="wrap_content"/>

            <TextView
                    android:id="@+id/login_activity_tx_register"
                    android:layout_marginTop="10dp"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_centerVertical="true"
                    android:layout_alignParentEnd="true"
                    android:layout_gravity="right"
                    android:textColor="@color/teal_200"
                    android:text="@string/not_register" tools:ignore="RelativeOverlap,RtlHardcoded"/>
        </RelativeLayout>

        <Button
                android:id="@+id/login_activity_btn_login"
                android:layout_marginTop="20dp"
                android:layout_width="match_parent"
                android:text="@string/login"
                android:layout_height="50dp"/>


    </androidx.appcompat.widget.LinearLayoutCompat>

</androidx.appcompat.widget.LinearLayoutCompat>
```

```java
/**
 * 登录
 */
public class LoginActivity extends AppCompatActivity {

    private static final String CHANNEL_ID = "公共通知";
    /**
     * 用户名、密码 输入框
     */
    private EditText et_username, et_pwd;
    /**
     * sp （用于存储已登录用户的信息）
     */
    private SharedPreferences shared;
    /**
     * 是否登录
     */
    private boolean is_login;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);

        TextView tx_register = findViewById(R.id.login_activity_tx_register);
        Button btn_login = findViewById(R.id.login_activity_btn_login);
        CheckBox cb_save_pwd = findViewById(R.id.login_activity_cb_save_pwd);

        shared = getSharedPreferences("user", MODE_PRIVATE);
        et_username = findViewById(R.id.login_activity_et_username);
        et_pwd = findViewById(R.id.login_activity_et_pwd);
        is_login = shared.getBoolean("is_login", false);

        if (is_login) {
            String username = shared.getString("username", "CaoBaoQi");
            String pwd = shared.getString("pwd", "123321");
            et_username.setText(username);
            et_pwd.setText(pwd);
            cb_save_pwd.setChecked(true);
        }

        tx_register.setOnClickListener(v -> startActivity(new Intent(LoginActivity.this, RegisterActivity.class)));
        btn_login.setOnClickListener(this::validateForm);
        cb_save_pwd.setOnCheckedChangeListener((buttonView, isChecked) -> is_login = isChecked);
    }

    /**
     * 校验登录表单
     *
     * @param v view
     */
    private void validateForm(View v) {
        String username = et_username.getText().toString();
        String pwd = et_pwd.getText().toString();

        if (TextUtils.isEmpty(username) && TextUtils.isEmpty(pwd)) {
            Toast.makeText(this, "请输入用户名或密码", Toast.LENGTH_SHORT).show();
        } else {
            Account account = AccountDBOperator.findAccount(getApplicationContext(), username);
            if (!(account == null)) {
                if ((username.equals(account.getUsername()) || username.equals(account.getEmail())) && pwd.equals(account.getPassword())) {
                    SharedPreferences.Editor editor = shared.edit();
                    editor.putBoolean("is_login", is_login);
                    editor.putString("username", username);
                    editor.putString("pwd", pwd);
                    editor.apply();

                    Account.setLoginedAccount(account);

                    Toast.makeText(this, "登录成功,欢迎您 " + account.getUsername(), Toast.LENGTH_SHORT).show();
                    startActivity(new Intent(LoginActivity.this, MainActivity.class));

                    {
                        CharSequence name = getString(R.string.channel_name);
                        String description = getString(R.string.channel_description);
                        int importance = NotificationManager.IMPORTANCE_HIGH;
                        NotificationChannel channel = new NotificationChannel(CHANNEL_ID, name, importance);
                        channel.setDescription(description);
                        // Register the channel with the system; you can't change the importance
                        // or other notification behaviors after this
                        NotificationManager notificationManager = getSystemService(NotificationManager.class);
                        notificationManager.createNotificationChannel(channel);
                    }

                    NotificationCompat.Builder builder = new NotificationCompat.Builder(this, CHANNEL_ID)
                            .setSmallIcon(R.drawable.avatar)
                            .setAutoCancel(true)
                            .setContentTitle("登录成功")
                            .setContentText("欢迎您 " + account.getUsername())
                            .setPriority(NotificationCompat.PRIORITY_MAX);

                    NotificationManagerCompat notificationManager = NotificationManagerCompat.from(this);
                    if (ActivityCompat.checkSelfPermission(this, Manifest.permission.POST_NOTIFICATIONS) != PackageManager.PERMISSION_GRANTED) {
                        Toast.makeText(this, "请开启通知权限", Toast.LENGTH_SHORT).show();
                        return;
                    }
                    notificationManager.notify(1, builder.build());


                } else {
                    Toast.makeText(this, "用户名或密码错误", Toast.LENGTH_SHORT).show();
                }
            } else {
                Toast.makeText(this, "未注册", Toast.LENGTH_SHORT).show();
            }
        }
    }
}
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231129204340742.png" alt="image-20231129204340742" style="zoom:50%;" />

#### 注册

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.appcompat.widget.LinearLayoutCompat
        android:background="#f9f4dc"
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent" xmlns:app="http://schemas.android.com/apk/res-auto"
        android:orientation="vertical"
        tools:ignore="ContentDescription"
        tools:context=".activity.RegisterActivity">

    <androidx.appcompat.widget.Toolbar
            android:id="@+id/register_activity_toolbar"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            app:title="@string/register"
            app:navigationIcon="@drawable/ic_baseline_arrow_back_ios_24"
            android:background="@color/teal_200"
            app:subtitleTextColor="@color/white"/>

    <TextView
            android:layout_marginTop="15dp"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textStyle="bold"
            android:textSize="20sp"
            android:text="@string/register"
            android:textColor="@color/black"
            android:gravity="center"/>

    <androidx.appcompat.widget.LinearLayoutCompat
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical"
            android:layout_margin="26dp">

        <androidx.appcompat.widget.LinearLayoutCompat
                android:layout_width="match_parent"
                android:background="@drawable/edit_backfround"
                android:paddingLeft="10dp"
                android:paddingRight="10dp"
                android:layout_height="50dp">

            <ImageView
                    android:layout_width="30dp"
                    android:layout_height="30dp"
                    android:layout_gravity="center_vertical"
                    android:src="@drawable/username"/>

            <EditText
                    android:id="@+id/register_activity_et_username"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:layout_marginStart="10dp"
                    android:hint="@string/input_name"
                    android:textSize="14sp"
                    android:background="@null" android:autofillHints="" android:inputType="textAutoComplete"/>


        </androidx.appcompat.widget.LinearLayoutCompat>
        <androidx.appcompat.widget.LinearLayoutCompat
                android:layout_marginTop="10dp"
                android:layout_width="match_parent"
                android:background="@drawable/edit_backfround"
                android:orientation="horizontal"
                android:paddingLeft="10dp"
                android:paddingRight="10dp"
                android:layout_height="50dp">

            <ImageView
                    android:layout_width="30dp"
                    android:layout_height="30dp"
                    android:layout_gravity="center_vertical"
                    android:src="@drawable/email"/>

            <EditText
                    android:id="@+id/register_activity_et_email"
                    android:layout_height="match_parent"
                    android:layout_width="match_parent"
                    android:layout_marginStart="10dp"
                    android:hint="@string/input_email"
                    android:textSize="14sp"
                    android:background="@null" android:autofillHints="" android:inputType="textEmailAddress"
                    tools:ignore="TextFields"/>

        </androidx.appcompat.widget.LinearLayoutCompat>
        <androidx.appcompat.widget.LinearLayoutCompat
                android:layout_marginTop="10dp"
                android:layout_width="match_parent"
                android:background="@drawable/edit_backfround"
                android:paddingLeft="10dp"
                android:paddingRight="10dp"
                android:layout_height="50dp">

            <ImageView
                    android:layout_width="30dp"
                    android:layout_height="30dp"
                    android:layout_gravity="center_vertical"
                    android:src="@drawable/password"/>

            <EditText
                    android:id="@+id/register_activity_et_pwd"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:layout_marginStart="10dp"
                    android:hint="@string/input_pwd"
                    android:textSize="14sp"
                    android:background="@null" android:autofillHints="" android:inputType="textPassword"/>


        </androidx.appcompat.widget.LinearLayoutCompat>

        <androidx.appcompat.widget.LinearLayoutCompat
                android:layout_marginTop="10dp"
                android:layout_width="match_parent"
                android:background="@drawable/edit_backfround"
                android:paddingLeft="10dp"
                android:paddingRight="10dp"
                android:layout_height="50dp">

            <ImageView
                    android:layout_width="30dp"
                    android:layout_height="30dp"
                    android:layout_gravity="center_vertical"
                    android:src="@drawable/password"/>

            <EditText
                    android:id="@+id/register_activity_et_pwd_twice"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:layout_marginStart="10dp"
                    android:hint="@string/input_pwd_twice"
                    android:textSize="14sp"
                    android:background="@null" android:autofillHints="" android:inputType="textPassword"/>


        </androidx.appcompat.widget.LinearLayoutCompat>


        <Button
                android:id="@+id/register_activity_btn_register"
                android:layout_marginTop="20dp"
                android:layout_width="match_parent"
                android:text="@string/register"
                android:layout_height="50dp"/>
    </androidx.appcompat.widget.LinearLayoutCompat>


</androidx.appcompat.widget.LinearLayoutCompat>
```

```java
/**
 * 注册
 */
public class RegisterActivity extends AppCompatActivity {

    private EditText et_username, et_email, et_pwd;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_register);

        et_username = findViewById(R.id.register_activity_et_username);
        et_email = findViewById(R.id.register_activity_et_email);
        et_pwd = findViewById(R.id.register_activity_et_pwd);

        // 返回按钮事件
        findViewById(R.id.register_activity_toolbar).setOnClickListener(v -> finish());

        Button btn_register = findViewById(R.id.register_activity_btn_register);
        btn_register.setOnClickListener(this::validateForm);
    }

    /**
     * 校验注册表单
     *
     * @param v view
     */
    private void validateForm(View v) {
        String username = et_username.getText().toString();
        String email = et_email.getText().toString();
        String pwd = et_pwd.getText().toString();
        Account account = new Account();

        if (TextUtils.isEmpty(username) && TextUtils.isEmpty(pwd)) {
            Toast.makeText(this, "请输入用户名或密码", Toast.LENGTH_SHORT).show();
        } else {
            account.setUsername(username);
            account.setEmail(email);
            account.setPassword(pwd);
            int count = AccountDBOperator.register(getApplicationContext(),account);
            if (count > 0) {
                Toast.makeText(this, "注册成功请登录", Toast.LENGTH_SHORT).show();
                finish();
            }
        }
    }
}
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231129204506960.png" alt="image-20231129204506960" style="zoom:50%;" />

#### 记住我

```java
    /**
     * sp （用于存储已登录用户的信息）
     */
    private SharedPreferences shared;
    /**
     * 是否登录
     */
    private boolean is_login;
 shared = getSharedPreferences("user", MODE_PRIVATE);
        et_username = findViewById(R.id.login_activity_et_username);
        et_pwd = findViewById(R.id.login_activity_et_pwd);
        is_login = shared.getBoolean("is_login", false);

        if (is_login) {
            String username = shared.getString("username", "CaoBaoQi");
            String pwd = shared.getString("pwd", "123321");
            et_username.setText(username);
            et_pwd.setText(pwd);
            cb_save_pwd.setChecked(true);
        }
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231129204657123.png" alt="image-20231129204657123" style="zoom:50%;" />

### 模糊检索

```java
 /**
     * 查询符合关键字的 Note 数据
     * @param context context
     * @param keyWord 关键字
     * @param recycle_status 0 未回收 | 1 已回收
     * @return List<Note>
     */
    public static List<Note> queryNotesData(Context context,String keyWord, int recycle_status) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getReadableDatabase();

        String sql = "SELECT * FROM note " +
                "WHERE (title LIKE \"%" + keyWord + "%\" " +
                "OR content LIKE \"%" + keyWord + "%\") " +
                "AND recycle_status = " + recycle_status +
                " ORDER BY date_updated DESC";

        List<Note> notes = new ArrayList<>();

        Cursor cursor = database.rawQuery(sql, null);
        while (cursor.moveToNext()) {
            int _id = cursor.getInt(0);
            String title = cursor.getString(1);
            String content = cursor.getString(2);
            String date_created = cursor.getString(3);
            String date_updated = cursor.getString(4);
            notes.add(new Note(_id, title, content, date_created, date_updated));
        }
        cursor.close();
        database.close();
        return notes;
    }
```

```java
   /**
     * 根据关键字查询待办
     * @param context context
     * @param keyWord 关键字
     * @return List<InAbeyance>
     */
    public static List<InAbeyance> queryInAbeyanceData(Context context, String keyWord) {
        DBHelper dbHelper = DBHelper.getInstance(context);
        SQLiteDatabase database = dbHelper.getReadableDatabase();

        String sql = "SELECT * FROM in_abeyance " +
                "WHERE content LIKE \"%" + keyWord + "%\"" +
                "ORDER BY _id DESC";

        Cursor cursor = database.rawQuery(sql, null);// 执行sql语句
        List<InAbeyance> inAbeyanceList = new ArrayList<>();

        while (cursor.moveToNext()) {
            int _id = cursor.getInt(0);
            String content = cursor.getString(1);
            String date_remind = cursor.getString(2);
            int status = cursor.getInt(3);
            InAbeyance inAbeyance = new InAbeyance(_id, content, date_remind, status);
            inAbeyanceList.add(inAbeyance);
        }
        cursor.close();
        database.close();
        return inAbeyanceList;
    }

```
![image-20231129204742502](https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231129204742502.png)

### 服务类实现通知

```java
/**
 * 闹钟工具类
 *
 * @author cbq
 * @date 2023/11/20 22:38
 * @since 1.0.0
 */
public class AlarmUtil {
    /**
     * 设置闹钟
     * @param context context
     * @param remindTime remindTime
     * @param _id _id
     * @param content content
     */
    @RequiresApi(api = Build.VERSION_CODES.S)
    public static void setAlarm(Context context, long remindTime,int _id, String content) {
        AlarmManager alarmManager = (AlarmManager)
                context.getSystemService(Context.ALARM_SERVICE);

        Intent intent = new Intent(context, AlarmReceiver.class);
        Bundle bundle = new Bundle();
        bundle.putString("content", content);
        intent.putExtras(bundle);

        PendingIntent sender = PendingIntent.getBroadcast(
                context, _id, intent, PendingIntent.FLAG_IMMUTABLE);

        /*
         * 注册闹钟
         * RTC_WAKEUP：指定当系统调用 System.currentTimeMillis() 方法返回的值 与 triggerAtTime 相等时
         * 启动 operation 所对应的设备（在指定的时刻，发送广播，并唤醒设备）
         */
        alarmManager.set(AlarmManager.RTC_WAKEUP, remindTime, sender);
    }

    /**
     * 取消闹钟
     * @param context context
     * @param _id _id
     */
    public static void cancelAlarm(Context context, int _id) {
        Intent intent = new Intent(context, AlarmReceiver.class);

        PendingIntent pendingIntent = PendingIntent.getBroadcast(
                context, _id, intent, PendingIntent.FLAG_IMMUTABLE);

        AlarmManager alarmManager = (AlarmManager)
                context.getSystemService(Context.ALARM_SERVICE);
        alarmManager.cancel(pendingIntent);
    }
}
```

```java
/**
 * 日期工具类
 *
 * @author cbq
 * @date 2023/11/20 22:39
 * @since 1.0.0
 */
public class DateUtil {
    /**
     * 获取当前日期
     * @return 日期字符串
     */
    public static String getCurrentTime() {
        @SuppressLint("SimpleDateFormat") DateFormat dateFormat
                = new SimpleDateFormat("MM月dd日 aa HH:mm");
        return dateFormat.format(new Date());
    }

    /**
     * 传入一个 Date 类型对象,
     * @param date date
     * @return 转换后的字符串
     */
    public static String getFormatTime(Date date) {
        @SuppressLint("SimpleDateFormat") SimpleDateFormat simpleDateFormat
                = new SimpleDateFormat("MM 月 dd 日 aa HH:mm");
        return simpleDateFormat.format(date);
    }

    /**
     * 将 util 包下 Date 类型日期时间转换为对应的绝对时间(long 类型的毫秒数)
     * @param dateTime dateTime
     * @return 对应的绝对时间(long 类型的毫秒数)
     */
    public static long getTimeMillis(String dateTime) {
        @SuppressLint("SimpleDateFormat") DateFormat dateFormat
                = new SimpleDateFormat("MM月dd日 aa HH:mm");
        try {
            Date date = dateFormat.parse(dateTime);
            if (date != null){
                date.setYear(Calendar.getInstance().get(Calendar.YEAR) - 1900);
                return date.getTime();
            }
        } catch (ParseException e) {
            Log.e("DateUtil->", "getTimeMillis: " + "捕获异常");
        }
        return System.currentTimeMillis() + 5000;
    }
}
```

```java
/**
 * AlarmReceiver 广播接收器
 *
 * @author cbq
 * @date 2023/11/20 22:35
 * @since 1.0.0
 */
public class AlarmReceiver extends BroadcastReceiver {

    @RequiresApi(api = Build.VERSION_CODES.S)
    @Override
    public void onReceive(Context context, Intent intent) {
        NotificationManager notificationManager = (NotificationManager)
                context.getSystemService(Context.NOTIFICATION_SERVICE);

        PendingIntent pendingIntent = PendingIntent.getActivity(
                context, 0, new Intent(context, MainActivity.class), PendingIntent.FLAG_IMMUTABLE);

        Notification notification;
        Bundle bundle = intent.getExtras();

        NotificationChannel notificationChannel = new NotificationChannel(
                "TODOAlarm", "待办提醒",
                NotificationManager.IMPORTANCE_HIGH);

        notificationManager.createNotificationChannel(notificationChannel);

        if (bundle != null) {
            notification = new Notification.Builder(context, "TODOAlarm")
                    .setSmallIcon(R.drawable.ic_baseline_alarm_24)
                    .setTicker("待办提醒")
                    .setContentTitle("待办事项提醒")
                    .setContentText(bundle.getString("content"))
                    .setContentIntent(pendingIntent)
                    .setAutoCancel(true)
                    .build();
            notificationManager.notify(3, notification);
        } else {
            Toast.makeText(context, "内部错误" + " | AlarmReceiver(onReceive)", Toast.LENGTH_SHORT).show();
        }
    }
}
```

