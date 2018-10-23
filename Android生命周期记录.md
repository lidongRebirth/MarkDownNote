生命周期记录：

该测试应用共有`MainActivity`、`TwoActivity`、`OneFragment`、`TwoFragment`四个，两个碎片是呈现在`TwoActivity`中的一个`LinearLayout`布局中的

行为一：打开应用



```java
I/MainActivity_ceshi: onCreate: 
I/MainActivity_ceshi: onStart: 
I/MainActivity_ceshi: onResume: 
```

行为二：跳转至`TwoActivity`

```java
I/MainActivity_ceshi: onPause: 
I/TwoActivity_ceshi: onCreate: 
I/TwoActivity_ceshi: onStart: 
I/TwoActivity_ceshi: onResume: 
I/MainActivity_ceshi: onStop: 
```

行为三：`TwoActivity`中添加碎片`OneFragment`

```java
I/OneFragment_ceshi: onAttach: 
I/OneFragment_ceshi: onCreate: 
I/OneFragment_ceshi: onCreateView: 
I/OneFragment_ceshi: onActivityCreated: 
I/OneFragment_ceshi: onStart: 
I/OneFragment_ceshi: onResume: 
```

行为四：替换`OneFragment`为`TwoFragment`

```java
I/TwoFragment_ceshi: onAttach:
I/TwoFragment_ceshi: onCreate: 
I/OneFragment_ceshi: onPause: 
I/OneFragment_ceshi: onStop: 
I/OneFragment_ceshi: onDestroyView: 
I/OneFragment_ceshi: onDestroy: 
I/OneFragment_ceshi: onDetach: 
I/TwoFragment_ceshi: onCreateView: 
I/TwoFragment_ceshi: onActivityCreated: 
I/TwoFragment_ceshi: onStart: 
I/TwoFragment_ceshi: onResume: 
```

行为5：锁屏

```java
I/TwoFragment_ceshi: onPause: 
I/TwoActivity_ceshi: onPause: 
I/TwoFragment_ceshi: onStop: 
I/TwoActivity_ceshi: onStop: 
```

行为6：开锁

```java
I/TwoActivity_ceshi: onRestart: 
I/TwoFragment_ceshi: onStart: 
I/TwoActivity_ceshi: onStart: 
I/TwoActivity_ceshi: onResume: 
I/TwoFragment_ceshi: onResume: 
```

行为7：返回键到`MainActivity`

```java
I/TwoFragment_ceshi: onPause: 
I/TwoActivity_ceshi: onPause: 
I/MainActivity_ceshi: onRestart: 
I/MainActivity_ceshi: onStart: 
I/MainActivity_ceshi: onResume: 
I/TwoFragment_ceshi: onStop: 
I/TwoActivity_ceshi: onStop: 
I/TwoFragment_ceshi: onDestroyView: 
I/TwoFragment_ceshi: onDestroy: 
I/TwoFragment_ceshi: onDetach: 
I/TwoActivity_ceshi: onDestroy: 
```

行为8：点`home`键返回桌面

```java
I/MainActivity_ceshi: onPause: 
I/MainActivity_ceshi: onStop: 
```

行为9：清理任务杀掉应用

```java
I/MainActivity_ceshi: onDestroy: 
```

行为8（2）：返回键到桌面，（coolpad手机）此时任务已被杀掉，再进行9无反应

```java
I/MainActivity_ceshi: onPause: 
I/MainActivity_ceshi: onStop: 
I/MainActivity_ceshi:  onDestroy: 
```

