[摘录文章](https://www.jianshu.com/p/464fa025229e)	   超详细超赞的，一定要看这个系列的文章！！！

### 1、集成

```java
implementation 'io.reactivex.rxjava2:rxjava:2.2.3'
implementation 'io.reactivex.rxjava2:rxandroid:2.1.0'
```
### 2、名称记录

|   名称    |   解释   |
| :-------: | :------: |
| Observable | 被观察者 |
|Observer|观察者|
|Emitter|发射器|
|Disposable|用完及丢弃，切到上下游，导致下游接收不到事件，但上游会继续发送剩余的事件|

###3、方法：

|持有类|  方法名  | 解释 |
|:--:| :------: | :--: |
|ObservableEmitter| onNext() |      |
|ObservableEmitter|onComplete()||
|ObservableEmitter|onError()||
|Disposable|dispose()|使用后下游不再接受事件，但上游会继续发送剩余的事件|
|Observable|subscribe()||
|Observable|subscribeOn()|上游发送事件的线程|
|Observable|observeOn()|下游接受事件的线程|
|Observable|filter()|过滤器|
|Observable|sample(2，TimeUnit.SECONDS)|每隔指定的时间从上游发一个事件给下游|
||||
||||
||||
||||
|Consumer|accept()|表示下游只关心onNext()事件|
||||
||||
||||
||||
||||
||||




**subscribe()多个重载的方法**

```java
public final Disposable subscribe() {}
public final Disposable subscribe(Consumer<? super T> onNext) {}
public final Disposable subscribe(Consumer<? super T> onNext, Consumer<? super Throwable> onError) {}
public final Disposable subscribe(Consumer<? super T> onNext, Consumer<? super Throwable> onError, Action onComplete) {}
public final Disposable subscribe(Consumer<? super T> onNext, Consumer<? super Throwable> onError, Action onComplete, Consumer<? super Disposable> onSubscribe) {}
public final void subscribe(Observer<? super T> observer) {}
```

* 不带任何参数的`subscribe()` 表示下游不关心任何事件,你上游尽管发你的数据去吧, 老子可不管你发什么 

* 带有一个`Consumer`参数的方法表示下游只关心onNext事件, 其他的事件我假装没看见, 因此我们如果只需要onNext事件可以这么写:

  ```java
  Observable.create(new ObservableOnSubscribe<Integer>() {
              @Override
              public void subscribe(ObservableEmitter<Integer> emitter) throws Exception {
                  Log.d(TAG, "emit 1");
                  emitter.onNext(1);
                  Log.d(TAG, "emit 2");
                  emitter.onNext(2);
                  Log.d(TAG, "emit 3");
                  emitter.onNext(3);
                  Log.d(TAG, "emit complete");
                  emitter.onComplete();
                  Log.d(TAG, "emit 4");
                  emitter.onNext(4);
              }
          }).subscribe(new Consumer<Integer>() {
              @Override
              public void accept(Integer integer) throws Exception {
                  Log.d(TAG, "onNext: " + integer);
              }
          });
  ```

  

 

 

 

 

###4、要点

* 上游可以发送无限个`onNext()`, 下游也可以接收无限个`onNext()` 

* 当上游发送了一个`onComplete()`后, 上游`onComplete()`之后的事件将会**继续**发送, 而下游收到`onComplete()`事件之后将**不再继续**接收事件 

* 当上游发送了一个`onError()`后, 上游`onError()`之后的事件将**继续**发送, 而下游收到`onError()`事件之后将**不再继续**接收事件 

* 上游可以不发送`onComplete()`或`onError()` 

* 最为关键的是`onComplete()`和`onError()`必须唯一并且互斥, 即不能发多个`onComplete()`, 也不能发多个`onError()`, 也不能先发一个`onComplete()`, 然后再发一个`onError()`, 反之亦然

> 注: 关于onComplete和onError唯一并且互斥这一点,  是需要自行在代码中进行控制, 如果你的代码逻辑中违背了这个规则, **并不一定会导致程序崩溃. ** 比如发送多个onComplete是可以正常运行的, 依然是收到第一个onComplete就不再接收了, 但若是发送多个onError, 则收到第二个onError事件会导致程序会崩溃

* `subscribeOn()`多次调用只有一次有效，`observeOn()`多次指定下游线程，每调用一次`observeOn`下游线程就会切换一次

**RxJava内置的线程选项**

* Schedulers.io() 代表io操作的线程, 通常用于网络,读写文件等io密集型的操作
* Schedulers.computation() 代表CPU计算密集型的操作, 例如需要大量计算的操作
* Schedulers.newThread() 代表一个常规的新线程
* AndroidSchedulers.mainThread() 代表Android的主线程
###5、Zip函数

**使用场景：**一个界面需要展示用户的一些信息，而这些信息分别要从两个服务器接口中获取，只有当两个都获取到了只有才能进行展示，此时用Zip就可以。

* 组合过程分别从两根水管各取一个事件来组合，并且一个事件只能取一次，组合顺序严格按照事件发送的顺序

* 下游收到事件数量和上游中发送事件最少的水管事件数量相同。

* 只有当最短的上游水管执行onComplete()后下游的水管才会执行onComplete()，否则不会执行onComplete()
###6、Backpressure

**使用场景：**其实就是为了控制流量，防止上游发送过快而下游处理过慢导致内存泄漏

* 当上下游位于同一线程时，为**同步**的订阅关系，上游每发送一个事件必须等到下游接受处理完成之后才能发送下一个事件，所以上游无限发，下游处理慢也不会导致内存泄漏

* 当上下游位于不同线程中时，为**异步**的订阅关系，上游发送不需要等待下游接收，而是通过“水缸”，上游放，下游从里面取，所以上游过快下游过慢就会出现OOM
  解决（OOM）办法：

* 从数量上进行治理，减少发送到水缸里的事件

  加filter()过滤器，只通过一部分事件，缺点：丢失部分事件

* 从速度上进行治理，减缓事件发送到水缸的速度

  在emitter.onNext()事件后加入sleep()，使其发送事件速度变慢
###7、Flowable

  

  
