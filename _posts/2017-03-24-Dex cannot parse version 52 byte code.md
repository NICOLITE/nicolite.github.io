---
title: Error converting bytecode to dex: Cause: Dex cannot parse version 52 byte code.
date: 2017-03-24 12:36:05
categories:
- Android
tags: 
---
**错误**
```
Error:Error converting bytecode to dex:
Cause: Dex cannot parse version 52 byte code.
This is caused by library dependencies that have been compiled using Java 8 or above.
If you are using the 'java' gradle plugin in a library submodule add 
targetCompatibility = '1.7'
sourceCompatibility = '1.7'
to that submodule's build.gradle file.
```

**原因**
这是因为项目中使用了Java8导致的，很有可能是在引入的第三方库中。
**解决方法**
**第一种：删除Java8的语法**  
将使用了Java8语法地方修改，删除或者替换使用了Java8的第三方库。
**第二种：修改gradle文件**  
可以通过对gradle文件配置，而不需要修改源代码，但是这样做后无法使用Instant run
```groovy
apply plugin: 'com.android.application'

android {
    compileSdkVersion 25
    buildToolsVersion "25.0.2"
    defaultConfig {
        applicationId "cn.nicolite.rxjavatest"
        minSdkVersion 21
        targetSdkVersion 25
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"

//这是要加入的部分
        jackOptions {
            enabled true
        }
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }


//这是要加入的部分
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
    compile 'com.android.support:appcompat-v7:25.3.0'
    compile 'com.android.support.constraint:constraint-layout:1.0.2'
    testCompile 'junit:junit:4.12'
}
```