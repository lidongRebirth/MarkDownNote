1. 生成release版本，直接点击androidstudio左下角的Build Variants，选择release，且要有key store才行

2. 判断当前程序是debug还是release版本

   ```java
   在Application中写入：
   	private boolean isDebug = true;
       private static ProjectApp instance;
   
   	@Override
       public void onCreate() {
           instance =this;
       }
       public static synchronized ProjectApp getInstance() {
           return instance;
       }
       public  boolean isDebug() {
           try {
               ApplicationInfo info = getInstance().getApplicationInfo();
               return (info.flags & ApplicationInfo.FLAG_DEBUGGABLE) != 0;
           } catch (Exception e) {
               return false;
           }
       }
   在活动中直接调动：
   ProjectApp.getInstance().isDebug()
   
   
   ```

   





[参考文章](https://blog.csdn.net/u__f_o/article/details/78356439)