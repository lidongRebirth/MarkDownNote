**错误1：**`file origin does not match viewer's`不支持跨域访问

解决：修改viewer.js文件,将不允许跨域的代码注释掉

```java
//不允许跨域
if (origin !== viewerOrigin && protocol !== 'blob:') {
		throw new Error('file origin does not match viewer\'s');
}
```

[关于跨域的知识](https://www.cnblogs.com/chenshishuo/p/4919224.html)



**使用：**

1、下载[pdf.js](http://mozilla.github.io/pdf.js/getting_started/)相关的文件

2、将下载的文件中欧冠的build和web文件夹放置到assets资源文件夹内新建的pdfjs文件夹中

3、活动页面内放置一个webview控件，加载pdf网上文件时直接

`webview.loadUrl("file:///android_asset/pdfjs/web/viewer.html?file="+pdfUrl)`即可。



