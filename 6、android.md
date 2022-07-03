# 1、编译

## 1、api和implementation区别：

api和implementation两种依赖的不同点在于：它们**声明的依赖其他模块是否能使用**。

 api：当其他模块依赖于此模块时，此模块使用api声明的依赖包是可以被其他模块使用。

implementation：当其他模块依赖此模块时，此模块使用implementation声明的依赖包只限于模块内部使用，不允许其他模块使用。



注意：[api](https://so.csdn.net/so/search?q=api&spm=1001.2101.3001.7020)引用方式会导致exclude失效

## 2、查看依赖树



```java
 gradlew :app:dependencies --configuration compile //查看编译时依赖树
```

```
 gradlew :app:dependencies --configuration  implementation
```

## 3、依赖冲突

### 【1】重复的类

![1654572597902](C:\02.code\note\img\1654572597902.png)

Android studio 生成aar包，不把第三方jar打进去的两种方式

#### 一、第一种方式

1、新建一个mylibs文件夹（名字只要与工程里的libs不冲突就行），把不参与打包的jar包放进去

2、在gradle中添加依赖，依赖方式使用 compileOnly，compileOnly表示只参与编译，不参与打包

repositories{
    flatDir{
        dirs 'libs'
        dirs 'mylibs'
    }
}
dependencies {
    implementation fileTree(include: ['*.jar'], dir: 'libs')
    compileOnly files('mylibs/sdk.jar')
}

#### 二、第二种方式

1、把gradle中的dependencies下 implementation fileTree(include: ['*.jar'], dir: 'libs')  注销。

2、使用 compileOnly 添加jar包依赖，compileOnly表示只参与编译，不参与打包

dependencies {
    //implementation fileTree(include: ['*.jar'], dir: 'libs')
    compileOnly files('libs/sdk.jar')
}

使用这两种方式任何一种都可以实现不把sdk.jar打包进aar中。



# 2、Api整理

## 【1】JsonObject

JsonObject通常位于两个包内：com.google.code.gson和

### (1)com.google.code.gson

#### fromJson()

##### 1、将Json字符串转成对应的对象

```
 Gson gson = new Gson();
 Bean bean = gson.fromJson(response, Bean)
```



# 3、RxJava

![1654572597902](C:\02.code\note\img\944365-e0b47abda3544b32.png)



# 4、仓库配置

## 设置本地仓库

```
maven {
    url uri('D:\\gome_code\\repo')
}
```

## 设置阿里云仓库

```
maven { url 'https://maven.aliyun.com/repository/public' }
maven { url 'https://maven.aliyun.com/repository/google' }
maven { url 'https://maven.aliyun.com/repository/central' }
```

## 阿里云其它仓库：

https://developer.aliyun.com/mvn/guide

| 仓库名称         | 阿里云仓库地址                                       | 阿里云仓库地址(老版)                                         | 源地址                                   |
| :--------------- | :--------------------------------------------------- | :----------------------------------------------------------- | :--------------------------------------- |
| central          | https://maven.aliyun.com/repository/central          | https://maven.aliyun.com/nexus/content/repositories/central  | https://repo1.maven.org/maven2/          |
| jcenter          | https://maven.aliyun.com/repository/public           | https://maven.aliyun.com/nexus/content/repositories/jcenter  | http://jcenter.bintray.com/              |
| public           | https://maven.aliyun.com/repository/public           | https://maven.aliyun.com/nexus/content/groups/public         | central仓和jcenter仓的聚合仓             |
| google           | https://maven.aliyun.com/repository/google           | https://maven.aliyun.com/nexus/content/repositories/google   | https://maven.google.com/                |
| gradle-plugin    | https://maven.aliyun.com/repository/gradle-plugin    | https://maven.aliyun.com/nexus/content/repositories/gradle-plugin | https://plugins.gradle.org/m2/           |
| spring           | https://maven.aliyun.com/repository/spring           | https://maven.aliyun.com/nexus/content/repositories/spring   | http://repo.spring.io/libs-milestone/    |
| spring-plugin    | https://maven.aliyun.com/repository/spring-plugin    | https://maven.aliyun.com/nexus/content/repositories/spring-plugin | http://repo.spring.io/plugins-release/   |
| grails-core      | https://maven.aliyun.com/repository/grails-core      | https://maven.aliyun.com/nexus/content/repositories/grails-core | https://repo.grails.org/grails/core      |
| apache snapshots | https://maven.aliyun.com/repository/apache-snapshots | https://maven.aliyun.com/nexus/content/repositories/apache-snapshots | https://repository.apache.org/snapshots/ |





# adb命令

- 查看目录结构 ：`adb shell ls`
- 查看系统当前日期 ：`adb shell date`
- 查看系统 CPU 使用情况 ：`adb shell cat /proc/cpuinfo`
- 查看系统内存使用情况 ：`adb shell cat /proc/meminfo`
- 显示所有应用 ：`adb shell pm list packages`
- 显示系统自带应用 ：`adb shell pm list packages -s`
- 显示第 3 方应用 ：`adb shell pm list packages -3`
- 查看当前页面名：
  MAC: `adb shell "dumpsys window |grep mCurrentFocus"`
  Windows： `adb shell "dumpsys window |findstr mCurrentFocus"`
- 清除应用数据以及缓存：`adb shell pm clear <包名>`

- input输入事件：

  adb shell input  text https://static-sit1.gomemyf.com/gomeyika-process-sit5/addInfo?type=newUser&vendor=GMJR



# net:ERR_CLEARTEXT_NOT_PERMITTED错误解决办法

在AndroidManifest.xml文件中添加

```vbnet
android:usesCleartextTraffic="true"
```

就像这样：

```XML
<?xml version="1.0" encoding="utf-8"?>
<manifest ...>
    <uses-permission android:name="android.permission.INTERNET" />
    <application
       ...
        android:usesCleartextTraffic="true"
        ...>
        ...
    </application>
```



# FFMPEG

```
ffmpeg -i audio.m4s -i video.m4s -vcodec copy -acodec copy -y -strict experimental 目标.mp4
```

#













# 网页跳转回应用的实现原理

就Android平台而言，URI主要分三个部分：scheme, authority and path。其中authority又分为host和port。格式如下： 
scheme://host:port/path 
举个实际的例子： 
content://com.example.project:200/folder/subfolder/etc 
\---------/  \---------------------------/ \---/ \--------------------------/ 
scheme                 host               port        path 
                \--------------------------------/ 
                          authority    
-----------------------------------
©著作权归作者所有：来自51CTO博客作者编程小石头的原创作品，请联系作者获取转载授权，否则将追究法律责任
Android 从网页中跳转到APP,从微信打开自己的app并打开指定页面
https://blog.51cto.com/u_14368928/3310310