---
title: 通过Activity实现安卓Splash（启动画面）
date: 2016-10-03 14:55:44
categories:
- Android
tags: 
---
现在几乎每个应用都有启动画面，所以学习的时候肯定不能错过,这里已Android Studio为例，Eclipse的类似  
#### 1.首先将我们的图片复制到res->drawable下,我这里是splash.png  
![](/images/20161003-145544-1.png)

#### 2.然后在res->layout下新建一个名为splash的布局文件  
![](/images/20161003-145544-2.png)  

#### 布局文件的代码如下  

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent" android:layout_height="match_parent">
    <ImageView
        android:id="@+id/splash"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:src="@drawable/splash"
        android:scaleType="fitXY" />
    <TextView
        android:id="@+id/info"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/app_name"
        android:layout_centerInParent="true"
        android:layout_alignParentBottom="true"
        android:textSize="25sp" />
</RelativeLayout>
```

#### 在你的活动所在文件夹新建一个名为SplashActivity的类  
![](/images/20161003-145544-3.png)  

#### 类中的代码如下  

```java
public class SplashActivity extends Activity {
    private final int SPLASH_DISPLAY_LENGTH = 3000;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        requestWindowFeature(Window.FEATURE_NO_TITLE);
        setContentView(R.layout.splash);

        new Handler().postDelayed(new Runnable() {
            @Override
            public void run() {
                Intent mainIntent = new Intent(SplashActivity.this, ChooseAreaActivity.class);
                // ChooseAreaActivity.class是你启动完后台要启动的活动
                SplashActivity.this.startActivity(mainIntent);
                SplashActivity.this.finish();
            }
        }, SPLASH_DISPLAY_LENGTH);
    }
}
```

#### 到这里还不够，我们还得修改AndroidManifes.xml文件
```xml
 <activity
            android:theme="@android:style/Theme.Translucent.NoTitleBar.Fullscreen"
            <!-- 设置为无标题全屏显示，防止启动时白屏几秒 -->
            android:name="activity.SplashActivity">
            <!-- 将Splash活动设置为主活动，这样首先启动的就是splash界面了 -->
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity android:name="activity.ChooseAreaActivity"></activity>
        <!-- 注册启动splash后要启动的活动 -->
```

#### 效果如下  
![](/images/20161003-145544-4.png)