[总结文章](https://mp.weixin.qq.com/s/HFUXbJwqp6hC7Bb8wR0Svw)

**1、Webview打开一个页面，播放一段音乐，退出Activity时音乐还在后台播放**

   解决方案1：

   ```java
   //销毁Webview
   @Override
   protected void onDestroy() {
      if (mWebview != null) {
          mWebview.loadDataWithBaseURL(null, "", "text/html", "utf-8", null);
          mWebview.clearHistory();
          ((ViewGroup) mWebview.getParent()).removeView(mWebview);
          mWebview.destroy();
          mWebview = null;
      }
      super.onDestroy();
   }
   ```

   还有别问我为什么要移除，等你Error: WebView.destroy() called while still attached!之后你就知道了。 

   解决方案2：(实际使用并不能使用)

   ```java
   @Override
   protected void onPause() {
     h5_webview.onPause();
     h5_webview.pauseTimers();
     super.onPause();
   }
   @Override
   protected void onResume() {
     h5_webview.onResume();
     h5_webview.resumeTimers();
     super.onResume();
   }
   ```

**2、 用网页标题设置自己的标题栏**

   ```java
    nativeWeb.setWebChromeClient(new WebChromeClient(){
               @Override
               public void onReceivedTitle(WebView view, String title) {      //设置自己的标题栏
                   super.onReceivedTitle(view, title);
                   if(title!=null){
                       tvMiddle.setText(title);
                   }
               }
           });
   ```

**3、Android8.0的WebView回退失效**

[文章](https://blog.csdn.net/SilenceOO/article/details/80058487)

   ```java
   x5Web.setWebViewClient(new WebViewClient() {
   /**
   * 防止加载网页时调起系统浏览器
   */
   public boolean shouldOverrideUrlLoading(WebView view, String url) {     //8.0以后返回false才会重定向，并且无需调用loadUrl
      if(Build.VERSION.SDK_INT<26){
            view.loadUrl(url);
            Log.i(TAG, "shouldOverrideUrlLoading: 触发，为重定向地址，所以加载两次");
            Log.i(TAG, "shouldOverrideUrlLoading: 重定向的地址为："+url);
            return true;}
            return false;
   }
   ```

   Android 8.0开始WebView的shouldOverrideUrlLoading(WebView view, String url)返回值是false才会自动重定向，并且无需调用loadUrl，与8.0之前的效果刚好相反。 

**4、5.0以后解决WebView加载的链接为Https开头，但链接里的内容，如图片为http链接，图片会加载不出来**

```java
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {    //两者都可以    			 
   webSetting.setMixedContentMode(webSetting.getMixedContentMode()); 
   webSetting.setMixedContentMode(WebSettings.MIXED_CONTENT_ALWAYS_ALLOW);
}
```

参数说明：  

- MIXED_CONTENT_ALWAYS_ALLOW 允许从任何来源加载内容，即使起源是不安全的；

- MIXED_CONTENT_NEVER_ALLOW 不允许Https加载Http的内容，即不允许从安全的起源去加载一个不安全的资源；

- MIXED_CONTENT_COMPLTIBILITY_MODE 当涉及到混合式内容时，WebView会尝试去兼容最新Web浏览器的风格；

另外：在认证证书不被Android所接受的情况下，我们可以通过设置重写WebViewClient的onReceivedSslError方法在其中设置接受所有网站的证书来解决，具体代码如下： 

```java
webView.setWebViewClient(new WebViewClient() {
       @Override
       public void onReceivedSslError(WebView view,SslErrorHandler handler, SslError error) {
           //super.onReceivedSslError(view, handler, error);注意一定要去除这行代码，否则设置无效。
           // handler.cancel();// Android默认的处理方式
           handler.proceed();// 接受所有网站的证书
           // handleMessage(Message msg);// 进行其他处理
       }
});
```

**5、WebView调用手机系统相册来上传图片？？？？？？**

[文章一](https://blog.csdn.net/yuzhiqiang_1993/article/details/76228541)

[文章二](https://blog.csdn.net/yuzhiqiang_1993/article/details/74012067)

[文章三](https://blog.csdn.net/qq_35070105/article/details/75546374)

[文章四](https://blog.csdn.net/github_38516987/article/details/77988182)

[文章五](https://blog.csdn.net/taohai123/article/details/53302405)

[文章六](https://blog.csdn.net/qq_34829270/article/details/80207293)

[文章七](https://blog.csdn.net/qq_21138819/article/details/56676007)

**6、webview开启硬件加速导致问题(界面闪烁)**

解决：在过渡期前将webview的硬件加速临时关闭，过渡期后再开启
```java
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.HONEYCOMB) {       
    webview.setLayerType(View.LAYER_TYPE_SOFTWARE, null);   		//指定支持此视图层的类型
} 
webview.setLayerType(View.LAYER_TYPE_SOFTWARE ,null);

webview.setLayerType(View.LAYER_TYPE_HARDWARE, null) 
```

View layers 
所有的Android版本View都可以在非屏幕内存(off-screen buffers)上渲染，使用view的drawing cache或者Canvas.saveLayer().非屏幕内存或者layers有许多用处，在对复杂对View做动画或者做一些叠加复合效果时可以得到更好的性能。 
在Android3.0之后可以使用View.setLayerType()来控制如何使用layers。
LAYER_TYPE_NONE 默认行为，正常渲染，不会在off-screen buffer上备份
LAYER_TYPE_HARDWARE 如果应用开启了硬件加速view渲染在硬件上，否则与LAYER_TYPE_SOFTWARE行为一样
LAYER_TYPE_SOFTWARE 用软件渲染在一个bitmap上
使用硬件加速有更高的效率，如果产生兼容性问题，可以用setLayerType改变渲染方式。


**7、Android 4.0+中Edit字符重叠问题**





