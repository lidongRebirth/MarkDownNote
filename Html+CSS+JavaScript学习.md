# HTML



# CSS



# JavaScript

HTML DOM（文档对象模型），通过HTML DOM可访问 JavaScript HTML 文档的所有元素。 

**1、查找HTML元素**

1. 通过id		

   `var x=document.getElementById("id"); `

2. 通过标签名

   查找 id="main" 的元素，然后查找 id="main" 元素中的**所有** <p> 元素： 

   `var x=document.getElementById("main"); `

    `var y=x.getElementsByTagName("p"); `

3. 通过类名

   `var x=document.getElementsByClassName("intro"); `

**2、改变HTML**

1. 直接向 HTML 输出流写内容 

   `document.write(Date()); `

2. 改变HTML内容

   `document.getElementById(id).innerHTML=新的 HTML `

3. 改变HTML属性

   `document.getElementById(id).attribute=新属性值 `

   attribute为属性，例如：`document.getElementById("image").src="landscape.jpg"; `

**3、改变CSS**

1. 改变HTML样式

   `document.getElementById(id).style.property=新样式 `

   此处的property为相应的样式，可以为color、fontFamily、fontSize

   例：

   `document.getElementById("p2").style.color="blue"; `改变字体颜色

   `document.getElementById("p2").style.fontFamily="Arial"; `改变文本字体系列、这个字体变小了

   `document.getElementById("p2").style.fontSize="larger"; `字体变大

2. 使用事件（通过触发事件来执行代码）

   `<button type="button" onclick="document.getElementById('id1').style.color='red'">点我</button>`

**4、HTML DOM事件**  

1. 对事件做出反应

   当点击某元素，向该HTML事件属性添加JavaScript代码

   `<h1 onclick="this.innerHTML='Ooops!'">点击文本!</h1> `

   方式二：定义方法供其调用

   ```javascript
   <!DOCTYPE html>
   <html>
   <head>
   <script>
   function changetext(id)
   {
       id.innerHTML="Ooops!";
   }
   </script>
   </head>
   <body>
   <h1 onclick="changetext(this)">点击文本!</h1>
   </body>
   </html>
   ```

   2、使用HTML DOM来分配事件

   例：向button元素分类onClick()事件

   ```javascript
   <script>
   document.getElementById("myBtn").onclick=function(){displayDate()};
   </script>
   ```

   3、onload和onunload事件

   会在用户进入或离开页面时被触发

   onload 事件可用于检测访问者的浏览器类型和浏览器版本，并基于这些信息来加载网页的正确版本。

   onload 和 onunload 事件可用于处理 cookie。

   `<body onload="checkCookies()"> `

   4、onchange事件

   例：当用户改变输入字段的内容时，会调用 upperCase() 函数。 

   `<input type="text" id="fname" onchange="upperCase()"> `

   5、onmouseover 和 onmouseout 事件

   在用户的鼠标移至 HTML 元素上方或移出元素时触发函数。 

   ```javascript
   <div onmouseover="mOver(this)" onmouseout="mOut(this)" style="background-color:#D94A38;width:120px;height:20px;padding:40px;">Mouse Over Me</div>
   <script>
   function mOver(obj){
   	obj.innerHTML="Thank You"
   }
   function mOut(obj){
   	obj.innerHTML="Mouse Over Me"
   }
   ```

   7、onmousedown、onmouseup以及onclick事件

   

   

   

   







