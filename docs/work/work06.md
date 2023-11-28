# 聊天

- 熟练使用相对布局
- Adapter 基本使用

## Adapter

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="horizontal"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:layout_gravity="center_vertical">
    <ImageView
            android:id="@+id/image_left"
            android:layout_width="35dp"
            android:scaleType="centerCrop"
            android:layout_height="35dp">
    </ImageView>
    <TextView
            android:id="@+id/title_left"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textSize="18dp"
            android:layout_marginLeft="15dp"/>


</LinearLayout>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="horizontal"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:gravity="right|center_vertical">
    <TextView
            android:id="@+id/title_right"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textSize="18dp"
            android:layout_marginRight="15dp"/>
    <ImageView
            android:id="@+id/image_right"
            android:layout_marginRight="1dp"
            android:scaleType="centerCrop"
            android:layout_width="35dp"
            android:layout_height="35dp">
    </ImageView>
</LinearLayout>
```

```java
/**
 * MessageAdapter
 *
 * @author Cola777jz
 * @date 2023/10/31 17:32
 * @since 1.0.0
 */
public class MessageAdapter extends BaseAdapter {
    private final List<MessageItem> data;
    private final Context context;

    public MessageAdapter(List<MessageItem> data,Context context){
        this.data=data;
        this.context=context;
    }
    @Override
    public int getCount() {
        return data.size();
    }

    @Override
    public Object getItem(int i) {
        return data.get(i);
    }

    @Override
    public long getItemId(int i) {
        return i;
    }

    @Override
    public View getView(int i, View view, ViewGroup viewGroup) {
        ViewHolder holder;
        MessageItem m =data.get(i);
        if(view==null){
            holder= new ViewHolder();
            if (m.getMag_type()==0){
                view= LayoutInflater.from(context).inflate(R.layout.item_left,null);
                holder.image=view.findViewById(R.id.image_left);
                holder.title=view.findViewById(R.id.title_left);
            }else{
                view= LayoutInflater.from(context).inflate(R.layout.item_right,null);
                holder.image=view.findViewById(R.id.image_right);
                holder.title=view.findViewById(R.id.title_right);
            }
            view.setTag(holder);
        }else{
            holder=(ViewHolder) view.getTag();
        }
        holder.image.setImageBitmap(m.getImage());
        holder.title.setText(m.getTitle());
        return view;
    }
    static class ViewHolder{
        ImageView image;
        TextView title;
    }
}

```

```java
/**
 * MessageItem
 *
 * @author Cola777jz
 * @date 2023/10/31 17:31
 * @since 1.0.0
 */
public class MessageItem {
    private Bitmap image;
    private String title;
    private int mag_type;//消息的类型

    public MessageItem(Bitmap image,String title,int mag_type){
        this.mag_type=mag_type;
        this.title=title;
        this.image=image;
    }

    public Bitmap getImage() {
        return image;
    }

    public void setImage(Bitmap image) {
        this.image = image;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public int getMag_type() {
        return mag_type;
    }

    public void setMag_type(int mag_type) {
        this.mag_type = mag_type;
    }
}

```

## Activity

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity"
        android:orientation="vertical"
        android:padding="30dp">

    <ListView
            android:id="@+id/listView"
            android:layout_weight="1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
    />
    <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="horizontal"
            android:layout_marginTop="10dp">
        <ImageView
                android:layout_width="45dp"
                android:layout_height="45dp"
                android:background="@drawable/voice"
                android:scaleType="centerCrop"
                android:layout_marginLeft="5dp"/>

        <EditText
                android:id="@+id/et_input"
                android:layout_width="wrap_content"
                android:layout_height="match_parent"
                android:layout_marginLeft="5dp"
                android:layout_weight="1"
        />
        <Button
                android:id="@+id/btn_send"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="发送"
                android:textColor="@android:color/black"
                android:textSize="18dp"
                android:layout_marginLeft="5dp"
                android:background="@drawable/rectangle_shape"
        />
    </LinearLayout>
</LinearLayout>
```

```java
public class MainActivity extends AppCompatActivity {

    private ListView listView;
    private List<MessageItem> data = new ArrayList<>();
    private MessageAdapter adapter;
    private EditText et_input;//输入的内容
    private Button btn_send;//发送信息

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        listView = findViewById(R.id.listView);
        et_input = findViewById(R.id.et_input);
        btn_send = findViewById(R.id.btn_send);

        initData();

        adapter = new MessageAdapter(data, MainActivity.this);
        listView.setAdapter(adapter);
        btn_send.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String string = et_input.getText().toString();
                MessageItem m = new MessageItem(BitmapFactory.decodeResource(getResources(), R.drawable.qq),
                        string, 0);
                data.add(m);
                listView.setSelection(data.size());

                MessageItem m2 = new MessageItem(BitmapFactory.decodeResource(getResources(), R.drawable.wchat),
                        string + "_Copy!", 1);
                data.add(m2);
                listView.setSelection(data.size() + 1);
                adapter.notifyDataSetChanged();
                et_input.setText("");
            }
        });
        registerForContextMenu(listView);

        listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> adapterView, View view, final int i, long l) {
                PopupMenu popupMenu = new PopupMenu(MainActivity.this, view);
                popupMenu.getMenuInflater().inflate(R.menu.popuo_menu, popupMenu.getMenu());
                popupMenu.show();
                popupMenu.setOnMenuItemClickListener(new PopupMenu.OnMenuItemClickListener() {
                    @Override
                    public boolean onMenuItemClick(MenuItem menuItem) {
                        final int position = i;
                        MessageItem m = null;
                        final int itemId = menuItem.getItemId();
                        if (itemId == R.id.popup_add) {
                            if (data.get(position).getMag_type() == 0) {
                                m = new MessageItem(BitmapFactory.decodeResource(getResources(), R.drawable.wchat), "WeChat", 1);
                            } else if (data.get(position).getMag_type() == 1) {
                                m = new MessageItem(BitmapFactory.decodeResource(getResources(), R.drawable.qq), "QQ", 0);
                            }
                            data.add(m);
                            listView.setSelection(data.size());
                            adapter.notifyDataSetChanged();
                        } else if (itemId == R.id.popup_delete) {
                            AlertDialog.Builder builder = new AlertDialog.Builder(MainActivity.this);

                            builder
                                    .setTitle("Are You Sure？")
                                    .setNegativeButton("NO", new DialogInterface.OnClickListener() {
                                        @Override
                                        public void onClick(DialogInterface dialogInterface, int i) {
                                            Toast.makeText(MainActivity.this, "Please Choose Again", Toast.LENGTH_SHORT).show();

                                        }
                                    })
                                    .setPositiveButton("Yes", new DialogInterface.OnClickListener() {
                                        @Override
                                        public void onClick(DialogInterface dialogInterface, int i) {
                                            data.remove(position);
                                            listView.setSelection(data.size());
                                            adapter.notifyDataSetChanged();
                                        }
                                    }).create().show();

                        } else if (itemId == R.id.popup_more) {
                            Toast.makeText(MainActivity.this, "MORE-POPUP", Toast.LENGTH_SHORT).show();
                        }
                        return false;
                    }
                });
            }
        });

    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.option_menu, menu);
        return super.onCreateOptionsMenu(menu);
    }

    @Override
    public boolean onOptionsItemSelected(@NonNull MenuItem item) {
        int itemId = item.getItemId();
        if (itemId == R.id.option_style) {
            Toast.makeText(MainActivity.this,
                    "这是字体大小菜单", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_10) {
            Toast.makeText(MainActivity.this,
                    "这是10号字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_20) {
            Toast.makeText(MainActivity.this,
                    "这是20号字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_30) {
            Toast.makeText(MainActivity.this,
                    "这是30号字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_color || itemId == R.id.option_red) {
            Toast.makeText(MainActivity.this,
                    "这是红色字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_blue) {
            Toast.makeText(MainActivity.this,
                    "这是蓝色字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_yellow) {
            Toast.makeText(MainActivity.this,
                    "这是黄色字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_gray) {
            Toast.makeText(MainActivity.this,
                    "这是灰色字", Toast.LENGTH_SHORT).show();
        } else if (itemId == R.id.option_normal) {
            Toast.makeText(MainActivity.this,
                    "这是普通菜单", Toast.LENGTH_SHORT).show();
        }
        return super.onOptionsItemSelected(item);
    }

    @Override
    public void onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo) {
        getMenuInflater().inflate(R.menu.context_menu, menu);
        super.onCreateContextMenu(menu, v, menuInfo);
    }

    @Override
    public boolean onContextItemSelected(@NonNull MenuItem item) {
        AdapterView.AdapterContextMenuInfo menuInfo =
                (AdapterView.AdapterContextMenuInfo) item.getMenuInfo();
        final int position = menuInfo.position;
        MessageItem m = null;

        int itemId = item.getItemId();
        if (itemId == R.id.context_add) {
            if (data.get(position).getMag_type() == 0) {
                m = new MessageItem(BitmapFactory.decodeResource(getResources(), R.drawable.wchat), "WeChat", 1);
            } else if (data.get(position).getMag_type() == 1) {
                m = new MessageItem(BitmapFactory.decodeResource(getResources(), R.drawable.qq), "QQ", 0);
            }
            data.add(m);
            listView.setSelection(data.size());
            adapter.notifyDataSetChanged();
        } else if (itemId == R.id.context_delete) {
            AlertDialog.Builder builder = new AlertDialog.Builder(MainActivity.this);

            builder
                    .setTitle("确定删除吗？")
                    .setNegativeButton("取消", new DialogInterface.OnClickListener() {
                        @Override
                        public void onClick(DialogInterface dialogInterface, int i) {
                            Toast.makeText(MainActivity.this, "请重新选择", Toast.LENGTH_SHORT).show();

                        }
                    })
                    .setPositiveButton("确定", new DialogInterface.OnClickListener() {
                        @Override
                        public void onClick(DialogInterface dialogInterface, int i) {
                            data.remove(position);
                            listView.setSelection(data.size());
                            adapter.notifyDataSetChanged();
                        }
                    }).create().show();
        } else if (itemId == R.id.context_more) {
            Toast.makeText(MainActivity.this, "MORE-CONTEXT", Toast.LENGTH_SHORT).show();
        }
        return super.onContextItemSelected(item);
    }

    private void initData() {
        MessageItem m1 = new MessageItem(BitmapFactory.decodeResource(getResources(),
                R.drawable.qq), "你好！去上课吗？", 0);
        data.add(m1);
        MessageItem m2 = new MessageItem(BitmapFactory.decodeResource(getResources(),
                R.drawable.wchat), "是啊，要一起吗", 1);
        data.add(m2);
        MessageItem m3 = new MessageItem(BitmapFactory.decodeResource(getResources(),
                R.drawable.qq), "好啊！", 0);
        data.add(m3);
        MessageItem m4 = new MessageItem(BitmapFactory.decodeResource(getResources(),
                R.drawable.wchat), "走吧！", 1);
        data.add(m4);
        MessageItem m5 = new MessageItem(BitmapFactory.decodeResource(getResources(),
                R.drawable.qq), "好！", 0);
        data.add(m5);

    }
}
```

