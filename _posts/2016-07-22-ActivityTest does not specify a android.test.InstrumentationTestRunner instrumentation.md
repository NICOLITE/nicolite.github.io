---
title: ActivityTest does not specify a android.test.InstrumentationTestRunner instrumentation or does not declare uses-library android.test.runner in its AndroidManifest.xml
date: 2016-07-22 03:10:55
categories:
- Android
tags: 
---
是权限配置问题，需要在AndroidManifest.xml 加上2条配置信息：  
```xml
<application>
     <uses-library android:name="android.test.runner" >
</application>
<instrumentation 
      android:name="android.test.InstrumentationTestRunner" 
      android:targetPackage="com.example.activitytest">
</instrumentation>
```