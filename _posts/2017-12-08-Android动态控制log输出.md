---
title: Android动态控制log输出
date: 2017-12-08 16:24:26
categories:
- Android
tags: 
---
开发阶段我们通常需要通过打印log来进行代码调试，确认数据等  但是当发布正式版的时候，我们又希望不将log打印出来，难道把代码一条一条的删除吗？万一以后还要用到呢，这时候就需要配置log打印类了，debug时打印，打包正式版时不打印。 

### 首先在你的app目录下的gradle脚本对应位置中添加如下代码

```groovy
    buildTypes {
    
        release {
            buildConfigField("boolean", "LOG_DEBUG", "false")
        }

        debug {
            buildConfigField("boolean", "LOG_DEBUG", "true")
            }
    }
``` 
### 添加完成后，rebuild一下项目，这时候在你的BuildConfig类中就会自动生成对应的代码  

```java
//这个类上自动生成的
public final class BuildConfig {
  public static final boolean DEBUG = Boolean.parseBoolean("true");
  public static final String APPLICATION_ID = "cn.nicolite.huthelper";
  public static final String BUILD_TYPE = "debug";
  public static final String FLAVOR = "kuan";
  public static final int VERSION_CODE = 22556;
  public static final String VERSION_NAME = "1.0";
  // Fields from build type: debug
  public static final boolean LOG_DEBUG = true;
  //这就是我们在脚本中配置的，debug模式时时true，正式版时时false
}
```

### 接下来就是配置我们的log输出类了

```java
//虽然可以直接使用BuildConfig.DEBUG，但是由于这个常量由我们无法更改，由编译器控制，所以还是选择自己配置
/**
 * Created by nicolite on 17-6-24.
 * 用来控制Log输出
 */

public class LogUtils {

    private static final int VERBOSE = 1;
    private static  final int DEBUG = 2;
    private static final int INFO = 3;
    private static final int WARN = 4;
    private static final int  ERROR = 5;
    private static final int NOTHING = 6;
    private static final int LEVEL = VERBOSE; //将LEVEL设置为NOTHING就不会输出任何日志

    public static void v(String tag, String msg) {
        if (BuildConfig.LOG_DEBUG && LEVEL <= VERBOSE) {
            Log.v(tag, msg);
        }
    }

    public static void d(String tag, String msg) {
        if (BuildConfig.LOG_DEBUG && LEVEL <= DEBUG) {
            Log.d(tag, msg);
        }
    }

    public static void i(String tag, String msg) {
        if (BuildConfig.LOG_DEBUG && LEVEL <= INFO) {
            Log.i(tag, msg);
        }
    }

    public static void w(String tag, String msg) {
        if (BuildConfig.LOG_DEBUG && LEVEL <= WARN) {
            Log.w(tag, msg);
        }
    }

    public static void e(String tag, String msg) {
        if (BuildConfig.LOG_DEBUG && LEVEL <= ERROR) {
            Log.e(tag, msg);
        }
    }

    public static void v(String tag, String msg, Throwable throwable) {
        if (BuildConfig.LOG_DEBUG && LEVEL <= VERBOSE) {
            Log.v(tag, msg, throwable);
        }
    }

    public static void d(String tag, String msg, Throwable throwable) {
        if (BuildConfig.LOG_DEBUG && LEVEL <= DEBUG) {
            Log.d(tag, msg, throwable);
        }
    }

    public static void i(String tag, String msg, Throwable throwable) {
        if (BuildConfig.LOG_DEBUG && LEVEL <= INFO) {
            Log.i(tag, msg, throwable);
        }
    }

    public static void w(String tag, String msg, Throwable throwable) {
        if (BuildConfig.LOG_DEBUG && LEVEL <= WARN) {
            Log.w(tag, msg, throwable);
        }
    }

    public static void e(String tag, String msg, Throwable throwable) {
        if (BuildConfig.LOG_DEBUG && LEVEL <= ERROR) {
            Log.e(tag, msg, throwable);
        }
    }
}

```