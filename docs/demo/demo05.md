# Menu 菜单

## MainActivity

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        tools:context=".MainActivity">

    <Button
            android:id="@+id/main_btn_optional"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/menu_optional"
            android:background="@color/white"
            android:textColor="#A52C2C"
            android:textSize="15sp"/>

    <Button
            android:id="@+id/main_btn_context"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/menu_context"
            android:background="@color/white"
            android:textColor="#9D25B1"
            android:textSize="15sp"/>

    <Button
            android:id="@+id/main_btn_popup"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/menu_popup"
            android:background="@color/white"
            android:textColor="#E3316D"
            android:textSize="15sp"/>


</LinearLayout>
```

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button optional_bth = findViewById(R.id.main_btn_optional);
        Button context_bth = findViewById(R.id.main_btn_context);
        Button popup_bth = findViewById(R.id.main_btn_popup);

        optional_bth.setOnClickListener(v -> {
            Intent intent = new Intent(MainActivity.this, OptionalActivity.class);
            startActivity(intent);
        });
        context_bth.setOnClickListener(v -> {
            Intent intent = new Intent(MainActivity.this, ContextActivity.class);
            startActivity(intent);
        });
        popup_bth.setOnClickListener(v -> {
            Intent intent = new Intent(MainActivity.this, PopupActivity.class);
            startActivity(intent);
        });
    }


}
```

## 选项卡菜单

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
            android:id="@+id/option_style"
            android:title="@string/menu_optional_font_size">
        <menu>
            <item android:id="@+id/option_10"
                  android:title="@string/size_10"/>
            <item android:id="@+id/option_20"
                  android:title="@string/size_20"/>
            <item android:id="@+id/option_30"
                  android:title="@string/size_30"/>
        </menu>
    </item>

    <item
            android:id="@+id/option_color"
            android:title="@string/menu_optional_font_color">
        <menu>
            <item android:id="@+id/option_red"
                  android:title="@string/color_red"/>
            <item android:id="@+id/option_blue"
                  android:title="@string/color_blue"/>
            <item android:id="@+id/option_yellow"
                  android:title="@string/color_yellow"/>
            <item android:id="@+id/option_gray"
                  android:title="@string/color_gray"/>
        </menu>

    </item>

    <item
            android:id="@+id/option_normal"
            android:title="@string/menu_optional_normal">

    </item>

</menu>
```
```xml
<?xml version="1.0" encoding="utf-8"?>
<ListView
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".OptionalActivity">


</ListView>
```
```java
/**
 * OptionalActivity
 *
 * @author Cola777jz
 * @date 2023/10/31 19:04
 * @since 1.0.0
 */
public class OptionalActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_menu_optional);

    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.menu_optional, menu);

        return super.onCreateOptionsMenu(menu);
    }

    @Override
    public boolean onOptionsItemSelected(@NonNull MenuItem item) {
        int itemId = item.getItemId();

        if (itemId == R.id.option_style) {
            Toast.makeText(this, "这是字体大小菜单", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_10) {
            Toast.makeText(this, "这是10号字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_20) {
            Toast.makeText(this, "这是20号字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_30) {
            Toast.makeText(this, "这是30号字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_color) {
            Toast.makeText(this, "这是字体颜色菜单", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_red) {
            Toast.makeText(this, "这是红色字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_blue) {
            Toast.makeText(this, "这是蓝色字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_yellow) {
            Toast.makeText(this, "这是黄色字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_gray) {
            Toast.makeText(this, "这是灰色字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_normal) {
            Toast.makeText(this, "OPTIONAL-NORMAL", Toast.LENGTH_SHORT).show();
        }

        return super.onOptionsItemSelected(item);
    }


}
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128200720469.png" alt="image-20231128200720469" style="zoom:80%;" />

## Adapter

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
                android:layout_width="match_parent"
                android:layout_height="match_parent">

    <ImageView
            android:id="@+id/iv"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="5dp"
            android:background="@drawable/mcdd_01"
            android:scaleType="centerCrop"/>

    <TextView
            android:id="@+id/tv_title"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_alignTop="@id/iv"
            android:layout_toEndOf="@id/iv"
            android:text="@string/name"
            android:textSize="18sp"
            android:textStyle="bold"/>

    <TextView
            android:id="@+id/tv_depict"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_below="@id/tv_title"
            android:layout_marginTop="10dp"
            android:layout_toEndOf="@id/iv"
            android:text="@string/description"
            android:textSize="16sp"/>



</RelativeLayout>
```

```java
/**
 * ListViewHolder
 *
 * @author Cola777jz
 * @date 2023/10/31 19:59
 * @since 1.0.0
 */
public class ListViewHolder {
    private TextView tvTitle;
    private TextView tvDepict;

    public ListViewHolder() {
    }

    public ListViewHolder(TextView tvTitle, TextView tvDepict) {
        this.tvTitle = tvTitle;
        this.tvDepict = tvDepict;
    }

    public TextView getTvTitle() {
        return tvTitle;
    }

    public void setTvTitle(TextView tvTitle) {
        this.tvTitle = tvTitle;
    }

    public TextView getTvDepict() {
        return tvDepict;
    }

    public void setTvDepict(TextView tvDepict) {
        this.tvDepict = tvDepict;
    }
}

```



## 上下文菜单

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
            android:id="@+id/context_add"
            android:title="@string/context_add"/>
    <item
            android:id="@+id/context_delete"
            android:title="@string/context_delete"/>
    <item
            android:id="@+id/context_more"
            android:title="@string/context_more"/>
</menu>
```
```xml
<?xml version="1.0" encoding="utf-8"?>
<ListView
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".ContextActivity">


</ListView>
```
```java
/**
 * ContextActivity
 *
 * @author Cola777jz
 * @date 2023/10/31 19:04
 * @since 1.0.0
 */
public class ContextActivity extends AppCompatActivity {

    private final String[] titles = {
            "错愕",
            "霍霍",
            "画画",
            "错愕",
            "霍霍",
            "画画",
            "错愕",
            "霍霍",
            "画画",
            "错愕",
            "霍霍",
            "画画",
            "送花"
    };

    private final String[] depicts = {
            "错愕的抹茶",
            "霍霍的抹茶",
            "画画的抹茶",
            "错愕的抹茶",
            "霍霍的抹茶",
            "画画的抹茶",
            "错愕的抹茶",
            "霍霍的抹茶",
            "画画的抹茶",
            "错愕的抹茶",
            "霍霍的抹茶",
            "画画的抹茶",
            "Mom to Flower"
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_menu_context);

        ListView listView = findViewById(R.id.listView);
        listView.setAdapter(new CustomBaseAdapter());

        listView.setOnItemClickListener((parent, view, position, id) -> {
            String text = "名称: " + titles[position] + "\n" + "描述: " + depicts[position];
            Toast.makeText(ContextActivity.this, text, Toast.LENGTH_SHORT).show();
        });

        registerForContextMenu(listView);

    }

    @Override
    public void onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo) {
        getMenuInflater().inflate(R.menu.menu_context, menu);
        super.onCreateContextMenu(menu, v, menuInfo);
    }


    @Override
    public boolean onContextItemSelected(@NonNull MenuItem item) {
        AdapterView.AdapterContextMenuInfo menuInfo =
                (AdapterView.AdapterContextMenuInfo) item.getMenuInfo();
        final int position = menuInfo.position;
        int itemId = item.getItemId();

        if (itemId == R.id.context_add) {
            Toast.makeText(this, " " + titles[position], Toast.LENGTH_SHORT).show();
            Toast.makeText(this, "context_add", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.context_delete) {
            Toast.makeText(this, " " + depicts[position], Toast.LENGTH_SHORT).show();
            Toast.makeText(this, "context_delete", Toast.LENGTH_SHORT).show();

        } else if (itemId == R.id.context_more) {
            Toast.makeText(this, "context_more", Toast.LENGTH_SHORT).show();
        }

        return super.onContextItemSelected(item);
    }

    /**
     * 自定义 Adapter
     */
    private class CustomBaseAdapter extends BaseAdapter {
        @Override
        public int getCount() {
            return titles.length;
        }

        @Override
        public Object getItem(int position) {
            return titles[position];
        }

        @Override
        public long getItemId(int position) {
            return position;
        }

        @Override
        public View getView(int position, View convertView, ViewGroup parent) {
            ListViewHolder viewHolder;
            if (convertView == null) {
                convertView = View.inflate(ContextActivity.this, R.layout.list_item, null);
                viewHolder = new ListViewHolder(
                        convertView.findViewById(R.id.tv_title),
                        convertView.findViewById(R.id.tv_depict)
                );
                convertView.setTag(viewHolder);
            } else {
                viewHolder = (ListViewHolder) convertView.getTag();
            }


            viewHolder.getTvTitle().setText(titles[position]);
            viewHolder.getTvDepict().setText(depicts[position]);

            return convertView;
        }
    }
}

```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128200807515.png" alt="image-20231128200807515" style="zoom:80%;" />

## 弹出菜单

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
            android:id="@+id/popup_add"
            android:title="@string/popup_add"/>
    <item
            android:id="@+id/popup_delete"
            android:title="@string/popup_delete"/>
    <item
            android:id="@+id/popup_more"
            android:title="@string/popup_more"/>
</menu>
```
```xml
<?xml version="1.0" encoding="utf-8"?>
<ListView
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".PopupActivity">


</ListView>
```
```java
/**
 * PopupActivity
 *
 * @author Cola777jz
 * @date 2023/10/31 19:04
 * @since 1.0.0
 */
public class PopupActivity extends AppCompatActivity {
    private final String[] titles = {
            "错愕",
            "霍霍",
            "画画",
            "错愕",
            "霍霍",
            "画画",
            "错愕",
            "霍霍",
            "画画",
            "错愕",
            "霍霍",
            "画画",
            "送花"
    };

    private final String[] depicts = {
            "错愕的抹茶",
            "霍霍的抹茶",
            "画画的抹茶",
            "错愕的抹茶",
            "霍霍的抹茶",
            "画画的抹茶",
            "错愕的抹茶",
            "霍霍的抹茶",
            "画画的抹茶",
            "错愕的抹茶",
            "霍霍的抹茶",
            "画画的抹茶",
            "Mom to Flower"
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_menu_popup);

        ListView listView = findViewById(R.id.listView);
        listView.setAdapter(new PopupActivity.CustomBaseAdapter());

        listView.setOnItemClickListener((parent, view, position, id) -> {
            PopupMenu popupMenu = new PopupMenu(PopupActivity.this, view);
            popupMenu.getMenuInflater().inflate(R.menu.menu_popup, popupMenu.getMenu());
            popupMenu.show();

            popupMenu.setOnMenuItemClickListener(item -> {
                int itemId = item.getItemId();
                if (itemId == R.id.popup_add) {
                    Toast.makeText(PopupActivity.this, " " + titles[position], Toast.LENGTH_SHORT).show();
                    Toast.makeText(PopupActivity.this, "popup_add", Toast.LENGTH_SHORT).show();
                } else if (itemId == R.id.popup_delete) {
                    Toast.makeText(PopupActivity.this, " " + depicts[position], Toast.LENGTH_SHORT).show();
                    Toast.makeText(PopupActivity.this, "popup_delete", Toast.LENGTH_SHORT).show();

                } else if (itemId == R.id.popup_more) {
                    Toast.makeText(PopupActivity.this, "popup_more", Toast.LENGTH_SHORT).show();
                }
                return false;
            });
        });
    }

    /**
     * 自定义 Adapter
     */
    private class CustomBaseAdapter extends BaseAdapter {
        @Override
        public int getCount() {
            return titles.length;
        }

        @Override
        public Object getItem(int position) {
            return titles[position];
        }

        @Override
        public long getItemId(int position) {
            return position;
        }

        @Override
        public View getView(int position, View convertView, ViewGroup parent) {
            ListViewHolder viewHolder;
            if (convertView == null) {
                convertView = View.inflate(PopupActivity.this, R.layout.list_item, null);
                viewHolder = new ListViewHolder(
                        convertView.findViewById(R.id.tv_title),
                        convertView.findViewById(R.id.tv_depict)
                );
                convertView.setTag(viewHolder);
            } else {
                viewHolder = (ListViewHolder) convertView.getTag();
            }


            viewHolder.getTvTitle().setText(titles[position]);
            viewHolder.getTvDepict().setText(depicts[position]);

            return convertView;
        }
    }
}

```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128200851729.png" alt="image-20231128200851729" style="zoom:80%;" />
