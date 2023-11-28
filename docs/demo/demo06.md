# List 列表

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
            android:id="@+id/main_btn_spinner"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/spinner"
            android:background="@color/white"
            android:textColor="#A52C2C"
            android:textSize="15sp"/>

    <Button
            android:id="@+id/main_btn_listView"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/listView"
            android:background="@color/white"
            android:textColor="#9D25B1"
            android:textSize="15sp"/>

    <Button
            android:id="@+id/main_btn_gridview"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/gridview"
            android:background="@color/white"
            android:textColor="#E3316D"
            android:textSize="15sp"/>

    <Button
            android:id="@+id/main_btn_recyclerview"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="5dp"
            android:text="@string/recyclerview"
            android:background="@color/white"
            android:textColor="#6CBAF8"
            android:textSize="15sp"/>

</LinearLayout>
```

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button btn_spinner = findViewById(R.id.main_btn_spinner);
        Button btn_list_view = findViewById(R.id.main_btn_listView);
        Button btn_grid_view  = findViewById(R.id.main_btn_gridview);
        Button btn_recycle_view = findViewById(R.id.main_btn_recyclerview);

        btn_spinner.setOnClickListener(v -> {
            Intent intent = new Intent(MainActivity.this, SpinnerActivity.class);
            startActivity(intent);
        });

        btn_list_view.setOnClickListener(v -> {
            Intent intent = new Intent(MainActivity.this, ListActivity.class);
            startActivity(intent);
        });

        btn_grid_view.setOnClickListener(v -> {
            Intent intent = new Intent(MainActivity.this, GridActivity.class);
            startActivity(intent);
        });

        btn_recycle_view.setOnClickListener(v -> {
            Intent intent = new Intent(MainActivity.this, RecycleActivity.class);
            startActivity(intent);
        });
    }
}
```

## Adapter

### ListViewAdapter

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
 * ViewHolder
 *
 * @author Cola777jz
 * @date 2023/10/31 16:57
 * @since 1.0.0
 */
public class ListViewHolder {
    private TextView tvTitle;
    private TextView tvDepict;
    private ImageView iv;

    public ListViewHolder() {
    }

    public ListViewHolder(TextView tvTitle, TextView tvDepict, ImageView iv) {
        this.tvTitle = tvTitle;
        this.tvDepict = tvDepict;
        this.iv = iv;
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

    public ImageView getIv() {
        return iv;
    }

    public void setIv(ImageView iv) {
        this.iv = iv;
    }
}
```

### OrderViewAdapter

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

    <TextView
            android:id="@+id/tx_goods_title"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_margin="8dp"
            android:text="云南天然干花束真花勿忘我家居客厅拜访超大花束"
            android:textSize="15sp"
            android:textStyle="bold"/>
    <TextView
            android:id="@+id/tx_order_status"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@id/tx_goods_title"
            android:layout_marginLeft="5dp"
            android:text="订单状态；已结算"/>

    <TextView
            android:id="@+id/tx_order_price"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentRight="true"
            android:layout_below="@id/tx_goods_title"
            android:layout_marginLeft="5dp"
            android:text="总价：80 元"/>

    <TextView
            android:id="@+id/tx_order_time"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@id/tx_order_status"
            android:layout_marginLeft="8dp"
            android:text="创建时间："/>



</RelativeLayout>
```

```java
/**
 * OrderViewHolder
 *
 * @author Cola777jz
 * @date 2023/10/31 17:19
 * @since 1.0.0
 */
public class OrderViewHolder {
    private TextView title;
    private TextView price;
    private TextView status;
    private TextView time;

    public TextView getTitle() {
        return title;
    }

    public void setTitle(TextView title) {
        this.title = title;
    }

    public TextView getPrice() {
        return price;
    }

    public void setPrice(TextView price) {
        this.price = price;
    }

    public TextView getStatus() {
        return status;
    }

    public void setStatus(TextView status) {
        this.status = status;
    }

    public TextView getTime() {
        return time;
    }

    public void setTime(TextView time) {
        this.time = time;
    }
}
```



## List

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

```xml
<?xml version="1.0" encoding="utf-8"?>
<ListView xmlns:android="http://schemas.android.com/apk/res/android"
          xmlns:tools="http://schemas.android.com/tools"
          android:id="@+id/listView"
          android:layout_width="match_parent"
          android:layout_height="match_parent"
          android:listSelector="#A9A9A9"
          tools:context=".MainActivity">

</ListView>
```

```java
/**
 * ListActivity
 *
 * @author Cola777jz
 * @date 2023/10/31 16:37
 * @since 1.0.0
 */
public class ListActivity extends AppCompatActivity {
    private int[] icons = {
            R.drawable.mcdd_01,
            R.drawable.mcdd_02,
            R.drawable.mcdd_03,
            R.drawable.mcdd_01,
            R.drawable.mcdd_02,
            R.drawable.mcdd_03,
            R.drawable.mcdd_01,
            R.drawable.mcdd_02,
            R.drawable.mcdd_03,
            R.drawable.mcdd_01,
            R.drawable.mcdd_02,
            R.drawable.mcdd_03,
            R.drawable.mcdd_04
    };

    private String[] titles = {
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

    private String[] depicts = {
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
        setContentView(R.layout.activity_list);

        ListView listView = findViewById(R.id.listView);
        listView.setAdapter(new CustomBaseAdapter());

        /**
         * 点击
         */
        listView.setOnItemClickListener((parent, view, position, id) -> {
            String text = "名称: " + titles[position] + "\n" + "描述: " + depicts[position];
            Toast.makeText(ListActivity.this, text, Toast.LENGTH_SHORT).show();
        });

        /**
         * 长按
         */
        listView.setOnItemLongClickListener((parent, view, position, id) -> {
            AlertDialog.Builder builder = new AlertDialog.Builder(ListActivity.this);
            AtomicReference<Boolean> flag = new AtomicReference<>(false);
            builder
                    .setMessage("确定要删除吗？")
                    .setPositiveButton("确定", (dialog, which) -> {
                        Toast.makeText(ListActivity.this, "您点击了 确定", Toast.LENGTH_SHORT).show();
                        flag.set(true);
                        Toast.makeText(ListActivity.this,"FLAG" + flag.get(),Toast.LENGTH_SHORT).show();
                    })
                    .setNegativeButton("取消", (dialog, which) -> {
                        Toast.makeText(ListActivity.this, "您点击了 取消", Toast.LENGTH_SHORT).show();
                        Toast.makeText(ListActivity.this,"FLAG" + flag.get(),Toast.LENGTH_SHORT).show();
                    })
                    .create().show();
            return flag.get();
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

        /**
         * 增强 listView （缓冲）
         * @param position The position of the item within the adapter's data set of the item whose view
         *        we want.
         * @param convertView The old view to reuse, if possible. Note: You should check that this view
         *        is non-null and of an appropriate type before using. If it is not possible to convert
         *        this view to display the correct data, this method can create a new view.
         *        Heterogeneous lists can specify their number of view types, so that this View is
         *        always of the right type (see {@link #getViewTypeCount()} and
         *        {@link #getItemViewType(int)}).
         * @param parent The parent that this view will eventually be attached to
         * @return convertView 缓冲对象
         */
        @Override
        public View getView(int position, View convertView, ViewGroup parent) {
            ListViewHolder viewHolder;
            if (convertView == null) {
                convertView = View.inflate(ListActivity.this, R.layout.list_item, null);
                viewHolder = new ListViewHolder(
                        convertView.findViewById(R.id.tv_title),
                        convertView.findViewById(R.id.tv_depict),
                        convertView.findViewById(R.id.iv)
                );
                convertView.setTag(viewHolder);
            } else {
                viewHolder = (ListViewHolder) convertView.getTag();
            }


            viewHolder.getIv().setBackgroundResource(icons[position]);
            viewHolder.getTvTitle().setText(titles[position]);
            viewHolder.getTvDepict().setText(depicts[position]);

            return convertView;
        }
    }
}
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128202002483.png" alt="image-20231128202002483" style="zoom:80%;" />

## GridList

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

</RelativeLayout>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<GridView xmlns:android="http://schemas.android.com/apk/res/android"
          xmlns:tools="http://schemas.android.com/tools"
          android:id="@+id/grid_view"
          android:layout_width="match_parent"
          android:layout_height="match_parent"
          android:listSelector="#A9A9A9"
          android:numColumns="4"
          android:verticalSpacing="3dp"
          tools:context=".GridActivity">



</GridView>
```

```java
{
    private GridView gridView;
    private List<Map<String, Object>> datas = new ArrayList<>();
    private int[] icons = {
            R.drawable.mcdd_01,
            R.drawable.mcdd_02,
            R.drawable.mcdd_03,
            R.drawable.mcdd_01,
            R.drawable.mcdd_02,
            R.drawable.mcdd_03,
            R.drawable.mcdd_01,
            R.drawable.mcdd_02,
            R.drawable.mcdd_03,
            R.drawable.mcdd_01,
            R.drawable.mcdd_02,
            R.drawable.mcdd_03,
            R.drawable.mcdd_04
    };

    private String[] titles = {
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
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_grid);
        initData();
        gridView = findViewById(R.id.grid_view);
        gridView.setAdapter(new SimpleAdapter(GridActivity.this,datas,R.layout.grid_item,new String[]{"icons","titles"},new int[]{R.id.iv,R.id.tv_title}));

        gridView.setOnItemClickListener((parent, view, position, id) -> {
            String text = "名称: " + titles[position];
            Toast.makeText(GridActivity.this, text, Toast.LENGTH_SHORT).show();
        });
    }
    void initData(){
        for (int i = 0; i < icons.length; i++) {
            Map<String, Object> item = new HashMap<>();
            item.put("icons", icons[i]);
            item.put("titles", titles[i]);
            datas.add(item);

        }
    }
}

```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128202037717.png" alt="image-20231128202037717" style="zoom:80%;" />

## SpinnerList

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
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
                android:text="@string/girl"
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
                android:text="@string/boy"
                android:textSize="16sp" />

        <Spinner
                android:id="@+id/sp_choice_b"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content" />
    </LinearLayout>


</LinearLayout>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
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
                android:text="@string/girl"
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
                android:text="@string/boy"
                android:textSize="16sp" />

        <Spinner
                android:id="@+id/sp_choice_b"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content" />
    </LinearLayout>


</LinearLayout>
```

```java
/**
 * SpinnerActivity
 *
 * @author Cola777jz
 * @date 2023/10/31 16:38
 * @since 1.0.0
 */
public class SpinnerActivity extends AppCompatActivity {
    private String[] boys = {"cbqH", "SongWenJie", "WangWenZhao"};
    private String[] girls = {"cbq", "cbqQ"};
    private Spinner spB;
    private Spinner spG;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_spinner);

        spB = findViewById(R.id.sp_choice_b);
        spB.setAdapter(new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, boys));

        spG = findViewById(R.id.sp_choice_g);
        spG.setAdapter(new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, girls));
    }
}
```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128202122174.png" alt="image-20231128202122174" style="zoom:80%;" />

## RecyclerList

```xml
<?xml version="1.0" encoding="utf-8"?>
<ListView xmlns:android="http://schemas.android.com/apk/res/android"
          xmlns:tools="http://schemas.android.com/tools"
          android:id="@+id/listView"
          android:layout_width="match_parent"
          android:layout_height="match_parent"
          android:listSelector="#A9A9A9"
          tools:context=".RecycleActivity">

</ListView>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

    <TextView
            android:id="@+id/tx_goods_title"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_margin="8dp"
            android:text="云南天然干花束真花勿忘我家居客厅拜访超大花束"
            android:textSize="15sp"
            android:textStyle="bold"/>
    <TextView
            android:id="@+id/tx_order_status"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@id/tx_goods_title"
            android:layout_marginLeft="5dp"
            android:text="订单状态；已结算"/>

    <TextView
            android:id="@+id/tx_order_price"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentRight="true"
            android:layout_below="@id/tx_goods_title"
            android:layout_marginLeft="5dp"
            android:text="总价：80 元"/>

    <TextView
            android:id="@+id/tx_order_time"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@id/tx_order_status"
            android:layout_marginLeft="8dp"
            android:text="创建时间："/>



</RelativeLayout>
```

```java
/**
 * RecycleActivity
 *
 * @author Cola777jz
 * @date 2023/10/31 16:38
 * @since 1.0.0
 */
public class RecycleActivity extends AppCompatActivity {
    private static final int ORDER_COUNT = 30;
    private List<OrderItem> orderList;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_recycle);

        orderList = new ArrayList<>();
        initOrderItemList(orderList);

        ListView listView = findViewById(R.id.listView);

        OrderAdapter adapter = new OrderAdapter(orderList, RecycleActivity.this);

        listView.setAdapter(adapter);
        listView.setOnItemClickListener((parent, view, position, id) ->
                Toast.makeText(RecycleActivity.this, "" + orderList.get(position), Toast.LENGTH_SHORT).show());
        listView.setOnItemLongClickListener((parent, view, position, id) -> {
            AlertDialog.Builder builder = new AlertDialog.Builder(RecycleActivity.this);

            builder
                    .setMessage("确定删除吗？")
                    .setPositiveButton("确定", (dialog, which) -> {
                        orderList.remove(position);
                        adapter.notifyDataSetChanged();
                    })
                    .setNegativeButton("取消", (dialog, which) -> Toast.makeText(RecycleActivity.this, "您取消了删除", Toast.LENGTH_SHORT).show()).create().show();
            return true;
        });
    }

    /**
     * 初始化数据
     * @param orderList orderList
     */
    void initOrderItemList(List<OrderItem> orderList) {
        Random random = new Random();
        for (int i = 0; i < ORDER_COUNT; i++) {
            OrderItem item = new OrderItem(
                    "title_" + random.nextInt(100),
                    random.nextDouble() + random.nextInt(50),
                    random.nextBoolean()
            );
            orderList.add(item);
        }
    }
}

```

<img src="https://jz-cbq-1311841992.cos.ap-beijing.myqcloud.com/images/image-20231128202202589.png" alt="image-20231128202202589" style="zoom:80%;" />