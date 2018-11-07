##Android中所有的危险权限：

| 权限组名|权限名|
|:---:| :--: |
| CALENDAR     | READ_CALENDAR		WRITE_CALENDAR |
| CAMERA | CAMERA |
|CONTACTS|READ_CONTACTS		WRITE_CONTACTS		GET_ACCOUNTS|
|LOCATION|ACCESS_FINE_LOCATION		ACCESS_COARSE_LOCATION|
|MICROPHONE|RECORD_AUDIO|
|PHONE|READ_PHONE_STATE		CALL_PHONE		READ_CALL_LOG	 WRITE_CALL_LOG		ADD_VOICEMAIL		USE_SIP		PROCESS_OUTGOING_CALLS|
|SENSORS|BODY_SENSORS|
|SMS|SEND_SMS		RECEIVE_SMS		READ_SMS		RECEIVE_WAP_PUSH	RECEIVE_MMS|
|STORAGE|READ_EXTERNAL_STORAGE		WRITE_EXTERNAL_STORAGE|
##注意事项

**1、运行权限申请时使用的是权限名，用户一旦授权，则该权限所在权限组中的所有权限都会被授权**

**2、Android6.0以后，这些权限不仅<u>要保留原来的静态注册</u>，还需要进行额外的动态权限申请**

**3、代码的动态申请必须在Activity中，不能在Application中，因为Application中无法处理弹窗的需求**

## 动态权限申请

```java
/**
 * 检查和申请权限
 */
public void requestPermission(){
    //判断是否已经赋予权限
    if(ContextCompat.checkSelfPermission(this, Manifest.permission.READ_PHONE_STATE)
            != PackageManager.PERMISSION_GRANTED
        || ContextCompat.checkSelfPermission(this, Manifest.permission.WRITE_EXTERNAL_STORAGE)
            != PackageManager.PERMISSION_GRANTED
        || ContextCompat.checkSelfPermission(this, Manifest.permission.READ_EXTERNAL_STORAGE)
            != PackageManager.PERMISSION_GRANTED){

        //多个权限一起进行申请
        ActivityCompat.requestPermissions(this, new String[]{
                Manifest.permission.READ_PHONE_STATE,
                Manifest.permission.WRITE_EXTERNAL_STORAGE,
                Manifest.permission.READ_EXTERNAL_STORAGE
            }, 1);//RequestCode = 1，用于处理弹窗结果（可以自己随意写）
    }else{
        Log.d(TAG, "Has Permission: READ_PHONE_STATE");
        /*============================================
         * 如果已经具有权限，就直接走接下来的流程。
         * * 该方法根据自己的业务逻辑去实现。
         *===================================*/
        doNextWork();
    }
}
```

## 动态权限申请结果

```java
@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
    super.onRequestPermissionsResult(requestCode, permissions, grantResults);
    //requestCode 对应于`requestPermissions`的requestCode
    switch(requestCode){
        case 1:
            //获取到了权限（按顺序，对三个权限进行验证）
            if(grantResults.length > 2
                    && grantResults[0] == PackageManager.PERMISSION_GRANTED
                    && grantResults[1] == PackageManager.PERMISSION_GRANTED
                    && grantResults[2] == PackageManager.PERMISSION_GRANTED
                    ){
                doNextWork();
            }else{
                //没有获取到权限，直接退出app。不然也没办法继续使用。
                Toast.makeText(this, "App must has permission!", Toast.LENGTH_SHORT).show();
                finish();
            }
            break;
        default:
            break;
    }
}
```

## 自己在项目中实际的使用

```java
1、编写判断权限是否申请的函数（此处是写在工具类中，供使用，所以使用static）
例如：读写权限的申请
    public static boolean verifyReadAndWritePermissions(Activity activity) {
    // 先判断是否含有权限
        int writePermission = ActivityCompat.checkSelfPermission(activity,
                Manifest.permission.WRITE_EXTERNAL_STORAGE);
        int readPermission = ActivityCompat.checkSelfPermission(activity,
                Manifest.permission.READ_EXTERNAL_STORAGE);

        if (writePermission != PackageManager.PERMISSION_GRANTED
                || readPermission != PackageManager.PERMISSION_GRANTED) {
     //没有权限进行申请
            ActivityCompat.requestPermissions(activity, PERMISSIONS_READANDWRITE,
                    REQUEST_READANDWRITE);
            return false;
        }else {
            return true;
        }
    }
2、在Activity中调用
if(verifyReadAndWritePermissions){	//true，权限已申请
	//做下一步操作
	doNext();	
}else{
	//什么也不做，这样当再次使用某功能时还会进行权限的申请，直到申请到了权限才会做下一步操作
}
以上的操作省去了在onRequestPermissionsResult（）里的操作
```









