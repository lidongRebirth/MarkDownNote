### [Retrofit官网](https://square.github.io/retrofit/#restadapter-configuration)

### 重点：

**1、注解QueryMap和Body的区别**

@QueryMap注解会把参数拼接到url后面，所以它适用于GET请求；
@Body会把参数放到请求体中，所以适用于POST请求。

如果你的项目是采用POST请求方式，不管是使用实体类还是使用HashMap最好采用@Body注解。虽然你使用QueryMap 可能也不会有什么问题（PS:这种共用的情况只适用于POST请求，GET请求不能使用@Body注解，否则会报错）





### 自己总结

所有的baseurl为`http://mock-api.com/2vKVbXK8.mock/ `

## Get请求

1. 普通的get









## Post请求

错误1：

```java
Unable to create @Body converter for class com.myfittinglife.app.retrofitsummarydemo.bean.PostDataBean (parameter #1)
```

解决：传输post需将实体转为json传过去





























### 相关文章

[文章一](https://blog.csdn.net/guohaosir/article/details/78942485)

[文章二](https://blog.csdn.net/u010507199/article/details/78354246)

[文章三](https://blog.csdn.net/wzl_show/article/details/76169501)

[文章四](https://blog.csdn.net/yhy123456q/article/details/78772373)

[文章五](https://blog.csdn.net/guohaosir/article/details/78942485)

[文章六](https://blog.csdn.net/xieluoxixi/article/details/80092582)



