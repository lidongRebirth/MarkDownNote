[LeakCanary中文使用说明](https://www.liaohuqiu.net/cn/posts/leak-canary-read-me/)

[LeakCanary具体分析](https://www.jianshu.com/p/1e7e9b576391)

#### 使用介绍：

1. 导入依赖：

   ```java
   debugImplementation 'com.squareup.leakcanary:leakcanary-android:1.3'
   releaseImplementation 'com.squareup.leakcanary:leakcanary-android-no-op:1.3'
   ```

2. 在Application的onCreate()方法中直接调用`LeakCanary.install(this);`即可

3. 若要在Fragment中使用：

   在Application中

   ```java
   public class App extends Application {
       
       private RefWatcher refWatcher;
       
       public void onCreate() {
           refWatcher = LeakCanary.install(this);
       }
       
       public static RefWatcher getRefWatcher(Context context) {
           App app = (App) context.getApplicationContext();
       }
   }
   ```

   在Fragment中

   ```java
   public void onDestroy(){
       super.onDestroy();
       
       RefWatcher refWatcher = App.getRefWatcher(getActivity());
       refWatcher.watch(this);
   }
   ```

   