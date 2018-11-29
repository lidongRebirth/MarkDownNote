###一、混合开发的一些文章

[WebSetting API](https://developer.mozilla.org/en-US/docs/WebAPI)

[Android中的WebView](http://androiddoc.qiniudn.com/reference/android/webkit/WebView.html)

[原生开发也需要知道的混合开发框](https://mp.weixin.qq.com/s/t45RhFonOKZPEXmQ0Rpj5w)

[谈谈App的混合开发](https://www.cnblogs.com/wlfcolin/p/6803133.html)

[Android中WebView的使用指南](https://mp.weixin.qq.com/s/mGT7VwHNeZHtVdFaP4IqXw)

[WebView截图的解决方案](https://mp.weixin.qq.com/s/k_lYhFQbn3n2cjloOexCUw)

[浅谈WebView的页面跳转1](https://mp.weixin.qq.com/s/4WP1mTmeWTU8nFO9Ex9vQQ)

[浅谈WebView的页面跳转2](https://mp.weixin.qq.com/s/4WP1mTmeWTU8nFO9Ex9vQ)

[webview内存泄漏解决方案](https://mp.weixin.qq.com/s/RJWiGQW_rbo9Ej9KdKRdTA)

**[WebView爬坑，看这篇就够了](https://mp.weixin.qq.com/s/HFUXbJwqp6hC7Bb8wR0Svw)**

[WebView使用漏洞](https://blog.csdn.net/carson_ho/article/details/64904635)

[WebView重定向导致的多次加载问题](https://blog.csdn.net/nifanggge/article/details/72814472)









[腾讯X5集成介绍](https://www.imooc.com/article/49311)

-----------------------------------------------------------------------------------------------------------------------------------------------------------

###二、[Websetting属性设置](https://blog.csdn.net/csdn_yang123/article/details/71709444)

[Android 中WebSettings文档](http://androiddoc.qiniudn.com/reference/android/webkit/WebSettings.html)

`setJavaScriptEnabled(true);`  		//支持js

`setPluginsEnabled(true);` 			 //支持插件

`webSettings.setRenderPriority(RenderPriority.HIGH);`  //提高渲染的优先级 

设置自适应屏幕，两者合用

`setUseWideViewPort(true); ` //将图片调整到适合webview的大小

`setLoadWithOverviewMode(true);` // 缩放至屏幕的大小



`setSupportZoom(true);`  //支持缩放，默认为true。是下面那个的前提。

`setBuiltInZoomControls(true);` //设置内置的缩放控件。

//若上面是false，则该WebView不可缩放，这个不管设置什么都不能缩放。
`setTextZoom(2);`							//设置文本的缩放倍数，默认为 100

`setDisplayZoomControls(false); `//隐藏原生的缩放控件 



 `setLayoutAlgorithm(LayoutAlgorithm.SINGLE_COLUMN); `//支持内容重新布局

共包含： 

`NORMAL, `

`SINGLE_COLUMN, `适应屏幕，内容将自动缩放

`NARROW_COLUMNS`适应内容大小



` supportMultipleWindows(); ` //多窗口 



**WebView的5种缓存模式：** 

```java
LOAD_NO_CACHE: 		不使用缓存，只从网络获取数据
LOAD_CACHE_ONLY:  	不使用网络，只读取本地缓存数据
LOAD_DEFAULT:  		根据cache-control决定是否从网络上取数据
LOAD_CACHE_NORMAL: API level 17中已经废弃, 从API level 11开始作用同LOAD_DEFAULT模式
LOAD_CACHE_ELSE_NETWORK，只要本地有，无论是否过期，或者no-cache，都使用缓存中的数据
```

`setCacheMode(WebSettings.LOAD_CACHE_ELSE_NETWORK);`  //关闭webview中缓存 

[缓存文章](https://www.jb51.net/article/116333.htm)

`webSetting.setAllowFileAccess(true);`       //设置可以访问文件

`setNeedInitialFocus(true);` //当webview调用requestFocus时为webview设置节点 

`setLoadsImagesAutomatically(true);`  //支持自动加载图片 

`setDefaultTextEncodingName("utf-8");`//设置编码格式 

`webSetting.setAppCacheMaxSize(Long.MAX_VALUE);`                                   //设置应用程序缓存内容的最大大小



-----------------------------------------------------------------------------------------------------------------------------------------------------------