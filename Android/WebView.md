1. Создаем пустой новый проект, добавляем строку в android->manifest->androidManifest.xml:

----------------------------------------------------------------------------------------------------------------

```<uses-permission android:name="android.permission.INTERNET"></uses-permission>```

----------------------------------------------------------------------------------------------------------------

В тело манифеста, но до application

2. Идем по пути android->res->layout->activity_main.xml, заменяем Hello world на:

----------------------------------------------------------------------------------------------------------------

```<WebView

android:id="@+id/webView"

android:layout_width="match_parent"

android:layout_height="match_parent"

/>```

----------------------------------------------------------------------------------------------------------------

3. Идем по пути android->java->com.webnet.NAME_PROJECT->MainActivity, все кроме первой строки заменяем:

----------------------------------------------------------------------------------------------------------------

```import androidx.appcompat.app.AppCompatActivity;

import android.app.Activity;

import android.os.Bundle;

import android.view.Window;

import android.view.WindowManager;

import android.webkit.WebResourceError;

import android.webkit.WebResourceRequest;

import android.webkit.WebView;

import android.webkit.WebViewClient;

import android.widget.Toast;

import android.annotation.TargetApi;

public class MainActivity extends AppCompatActivity {

WebView webView;

@Override

protected void onCreate(Bundle savedInstanceState) {

super.onCreate(savedInstanceState);

// задать fullscreen

this.getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN);

// задать No Title

getSupportActionBar().hide();

webView = new WebView(this);

webView.getSettings().setJavaScriptEnabled(true);

final Activity activity = this;

webView.setWebViewClient(new WebViewClient() {

@SuppressWarnings("deprecation")

@Override

public void onReceivedError(WebView view, int errorCode, String description, String failingUrl) {

Toast.makeText(activity, description, Toast.LENGTH_SHORT).show();

}

@TargetApi(android.os.Build.VERSION_CODES.M)

@Override

public void onReceivedError(WebView view, WebResourceRequest req, WebResourceError rerr) {

// Redirect to deprecated method, so you can use it in all SDK versions

onReceivedError(view, rerr.getErrorCode(), rerr.getDescription().toString(), req.getUrl().toString());

}

});

webView.loadUrl("https://zavod.store/index.html");

setContentView(webView);

}

}```

----------------------------------------------------------------------------------------------------------------

4. Последний шаг это подписать свой bundle перед публикацией