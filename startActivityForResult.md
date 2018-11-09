###requestCode请求码
![1541755306849](C:\Users\ADMINI~1\AppData\Local\Temp\1541755306849.png)
A活动中有两个按钮，两个按钮均用来打开活动B，此时返回来的数据如何判断是哪个按钮打开B而返回来的数据呢，这是通过请求码requestCode来标识请求来源。

###resultCode结果码
![1541756001239](C:\Users\ADMINI~1\AppData\Local\Temp\1541756001239.png)
A活动打开B活动和C活动，resultCode是用来区分是哪个活动返回来的数据。



```java
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    switch (requestCode){
        case 1:
            if(resultCode==RESULT_OK){
                tvSendContent.append("\n"+data.getStringExtra("data"));
            }
            break;
    }

}
```

[请求码结果码](https://blog.csdn.net/u010542873/article/details/51219352)

[详解博客](https://www.cnblogs.com/fuck1/p/5456337.html)