# Lab5
实验五Intent

## Intent:
![](/screenshot/web.png)
![](/screenshot/mybrowser.png)

## 代码：
### Main.java
public class MainActivity extends AppCompatActivity implements View.OnClickListener{

    private static final String TAG = "MainActivity";
    private Button btn_submit;
    private EditText edit_url;
    private String urlHead="https://";
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        btn_submit= findViewById(R.id.btn_submit);
        edit_url= findViewById(R.id.edit_url);
        btn_submit.setOnClickListener(this);
    }

    @Override
    public void onClick(View view) {
        switch (view.getId()){
            case R.id.btn_submit:
                Intent intent=new Intent(Intent.ACTION_VIEW);
                intent.setData(Uri.parse(urlHead+edit_url.getText().toString()));
                startActivity(intent);
                break;
        }
    }
}

### main.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical" >
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textSize="25sp"
            android:id="@+id/edit_url"/>

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textSize="25sp"
            android:text="浏览"
            android:id="@+id/btn_submit"
            android:layout_marginTop="20dp"
            android:layout_marginLeft="100dp" />
    </LinearLayout>
</LinearLayout>

### MyBrowser.java
public class MyBrowser extends AppCompatActivity {

    private WebView webView;
    private String url;

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_my_browser);
        initView();
        setWebView();
    }

    private void initView() {
        webView=(WebView)findViewById(R.id.show);
        url=getIntent().getData().toString();
    }

    private void setWebView() {
        WebSettings webSettings=webView.getSettings();
        webSettings.setJavaScriptEnabled(true);
        webSettings.setSupportZoom(true);
        webView.loadUrl(url);
        webView.setWebViewClient(new WebViewClient(){
            @Override
            public boolean shouldOverrideUrlLoading(WebView view,String url) {
                webView.loadUrl(url);
                return true;
            }
        });
    }

}

### MyBrowser.xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MyBrowser">

    <WebView
        android:id="@+id/show"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

    </WebView>
</android.support.constraint.ConstraintLayout>
