####sw最小宽度适配

* **使用方式**

1. 首先在values文件夹内自定义一个dimens文件，以该dimens.xml文件作为基准

2. 然后下载ScreenMatch插件，用来计算生成各个不同宽度的dimens文件

3. 使用时在项目目录下右击选择ScreenMatch,然后选择基于哪个module下的dimens文件作为基准，生成的dimens文件就放在哪个module下

* **代码中动态设置dp或sp**

   ```java
   /*注意
   * getDimension()方法并不是直接拿到dimens.xml文件中的dp或sp值
   * 而是將dimens.xml文件中的dp或sp值乘以屏幕密度（density）来换算成px值
   * 所以拿到该值后还需要换算成对应的dp或sp（除以屏幕密度）
   */
   
   
   /*获取sp值*/
   //获取对应资源文件下的sp值，getDimension()方法将其乘以屏幕密度变为px值
   float pxValue =getResources().getDimension(R.dimen.sp_15);	
   //将px值转化为sp值
   int spValue = ConvertUtils.px2sp(this,pxValue);
   
   
   
   /*获取dp值*/
   //获取对应资源文件下的dp值,getDimension()方法将其乘以屏幕密度变为px值
   float pxValue2=getResources().getDimension(R.dimen.dp_360);
   //将px值转化为dp值	
   int dpValue = ConvertUtils.px2dp(this,pxValue)；
   
   
   其中的ConvertUtils为自己编写的工具类
   
   public static int px2dp(Context context, final float pxValue) {
   	final float scale = context.getResources().getDisplayMetrics().density;
   	return (int) (pxValue / scale + 0.5f);
   }
   
   public static int sp2px(Context context, final float spValue) {
   	final float fontScale = 		       									context.getResources().getDisplayMetrics().scaledDensity;
   	return (int) (spValue * fontScale + 0.5f);
   }
   
   
   
   ```

* **实际密度和系统密度**

   安卓对界面元素进行缩放是根据系统密度而不是实际密度

   文字尺寸使用sp,这样当在系统设置里调节字号大小时，应用中文字也会变大变小

   | 分辨率|密度值|密度|
   |:----:|:----:|:----:|
   | 240×320 | 120 | ldpi |
   |320×480|160|mdpi|
   |480×800|240|hdpi|
   |720×1280|320|xhdpi|
   |1080×1920|480|xxhdpi|

* **dp与px的转化**

  dp和px的换算要以系统密度为准，例：720×1280系统密度为320，而320×480的系统密度为160,320/160=2，因为安卓中，系统密度以160dpi为基准屏幕，1dp=1px，所以720×1280中，1dp=2px;

  记住以下比例转化就很简单了
  |密度|ldpi|mdpi|hdpi|xhdpi|xxhdpi|
  |:--:|:--:|:--:|:--:|:--:|:--:|
  |分辨率|240×320|320×480|480×800|720×1280|1080×1920|
  |比例|3|4|6|8|12|
  ||0.75|1px|1.5|2|3|
  计算时以mdpi为基准，所以720×1280中1dp=2px

* **适配其他module**

  不需要多套dimens，只需要将app module中values文件夹下的dimens文件复制一份放入该module的values文件夹中即可。

  

  

  

  

  #### 参考文章

  [文章一](http://www.xueui.cn/experience/app-experience/ui-sedign-android.html)

  

  

   

   