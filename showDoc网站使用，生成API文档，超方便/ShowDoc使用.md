###1. [网址](https://www.showdoc.cc/)

###2. 注意事项：目前目录最多三级，即：测试文档/测试代码/测试代码

###3. 使用：

   **方式一**

   步骤一：在代码中直接加入注解：

   ```java
       /**
        * showdoc
        * @catalog 测试文档/测试代码传入/代码更改
        * @title   普通post请求数据
        * @description 用户post接口
        * @method post
        * @url     portal/tender/info/detail
        * @param url 必选 接口地址
        * @param map 必选 string 传入参数
        * @return {"error_code":0,"data":{"uid":"1","username":"12154545","name":"吴系挂","groupid":2,"reg_time":"1436864169","last_login_time":"0"}}
        * @return_param groupid int 用户组id
        * @return_param name string 用户昵称
        * @remark 这里是备注信息
        * @number 199
        */
   ```

   步骤二：将脚本放入到此目录下，更改脚本的appid和appsecret，运行脚本即可。

**方法二**

步骤一：

新建文本文档，填入以下简单的类似java格式的内容：

```java
public class MainActivity extends AppCompatActivity {
    /**
     * showdoc
     * @catalog 测试文档/测试代码传入/代码更改
     * @title   普通post请求数据2
     * @description 用户post接口
     * @method post
     * @url     portal/tender/info/detail
     * @param url 必选 接口地址
     * @param map 必选 string 传入参数
     * @return {"error_code":0,"data":{"uid":"1","username":"12154545","name":"吴系挂","groupid":2,"reg_time":"1436864169","last_login_time":"0"}}
     * @return_param groupid int 用户组id
     * @return_param name string 用户昵称
     * @remark 这里是备注信息
     * @number 199
     */
    public void fun(){
    }
}
```

步骤二：同上运行脚本即可

**方法三：**

直接在网页上---新建页面---然后插入API接口模板，在模板内填入相应内容即可。



