---
title: \@Field parameters can only be used with form encoding
date: 2017-08-11 10:40:23
categories:
- Android
tags: 
---
今天使用Retrofit使用Post请求获取Token时遇到了下面的错误：
```
java.lang.IllegalArgumentException: @Field parameters can only be used with form encoding. (parameter #1)
for method MessageAPI.getToken
at retrofit2.ServiceMethod$Builder.methodError(ServiceMethod.java:752)
at retrofit2.ServiceMethod$Builder.methodError(ServiceMethod.java:743)
at retrofit2.ServiceMethod$Builder.parameterError(ServiceMethod.java:761)
at retrofit2.ServiceMethod$Builder.parseParameterAnnotation(ServiceMethod.java:533)
at retrofit2.ServiceMethod$Builder.parseParameter(ServiceMethod.java:336)
at retrofit2.ServiceMethod$Builder.build(ServiceMethod.java:204)
at retrofit2.Retrofit.loadServiceMethod(Retrofit.java:170)
at retrofit2.Retrofit$1.invoke(Retrofit.java:147)
at java.lang.reflect.Proxy.invoke(Proxy.java:393)
at $Proxy6.getToken(Unknown Source)
```
##原因
```
@Field parameters can only be used with form encoding. (parameter #1)
```
从这句话可以看出是因为对方服务器，只支持x-www-form-urlencoded不支持form-data所致，reftrofit2默认的post请求用的就是form-data
##解决方法
```java
 @FormUrlEncoded  //加上这个就可以了
    @POST("https://xxx.com/getToken")
    Observable getToken(@Field("userid") String userId);
```