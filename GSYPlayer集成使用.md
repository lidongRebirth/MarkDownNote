### 集成中遇到的错误

**错误1：**[参考](https://blog.csdn.net/u014133119/article/details/81562552)

```java
Program type already present: android.support.v4.media.session.MediaControllerCompatApi21$PlaybackInfo, sources=[Unknown source file], tool name=Optional.of(D8)
```

**解决：**指没有依赖support v4包，在app的build.gradle中填入`implementation 'com.android.support:support-v4:28.0.0'`即可



**错误2：**在APP中使用`StandardGSYVideoPlayer`发现找不到，尽管module中已经依赖了，这个是主module引用不到依赖module里的依赖库问题[参考](https://blog.csdn.net/qq_32770809/article/details/80512582)

**解决：**这是因为AndroidStudio在3.0之后的版本，统一用`implementation`和`api`替换了`complie`，`androidTestApi`和`androidTestImplementation`替换了`androidTestCompile`,需要了解这些的不同

`implementation`声明的依赖包只限于模块内部使用，不允许其他模块使用

`api`声明的依赖包，模块依赖于此模块，此模块使用`api`声明的依赖包是可以被其他模块使用

**错误3：**集成过程中显示错误

`java.lang.RuntimeException: Manifest merger failed with multiple errors, see logs`

在Terminal控制台输入`gradlew processDebugManifest --stacktrace`后发现

```java
Error occurred during initialization of VM
Could not reserve enough space for 1572864KB object heap
```
解决：是不能给虚拟机分配足够的空间，在gradle.properties里，将原先的`org.gradle.jvmargs=-Xmx1536m`更改为`org.gradle.jvmargs=-Xmx512m`

更改后又显示：

```java
Execution failed for task ':app:processDebugManifest'.
> Manifest merger failed with multiple errors, see logs
```
解决：

在application标签中写入：

```
tools:replace="android:icon, android:label,android:theme"
```

更改后又显示：

```java
Manifest merger failed : uses-sdk:minSdkVersion 15 cannot be smaller than version 16 declared in library 
```

更改library和项目中的build.gradle中的`minSdkVersion 16`改为16即可。

