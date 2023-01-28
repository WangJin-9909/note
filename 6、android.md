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



# 5、Activity

## 5.1Activity生命周期

![生命周期流程图](C:\02.code\note\img\20191112212436952.png)

Activity第一次启动，回调如下：onCreate -> onStart -> onResume

打开新Activity或按Home键：onPause->onStop

如果新的Activity的Theme为Dialog或者Translucent（透明）时不会调用onStop方法

再次回到Activity：onRestart->onStart->onResume

按Back键退出Activity：onPause->onStop->onDestroy

![1674867968976](C:\02.code\note\img\1674867968976.png)

## 5.2Activity任务栈及启动模式

栈：先进后出，进栈(push)和出栈(pop)，其特点是先进后出

查看Activity 栈的情况

查看系统栈内activity列表：am stack list

查看指定应用内activity栈的情况：dumpsys activity -p com.example.activitystack 筛选后：dumpsys activity -p com.example.activitystack | grep Run

am start-activity -n com.

android activity的四种启动方式
前言：一个项目中会包含多个activity(虽然现在已经出现有activity的应用)，系统中使用任务栈来存储这些activity，任务栈呢，是一种“后进先出”的栈结构。举个栗子：当我们多次启动同一个（没有设置启动方式–即默认的启动方式）的activity的时候，系统会创建多个实例依次进入栈中。当back返回的时候，每按一次，一个activity出栈。直至栈空为止。按照这种做法就会大大的消耗内存，白白浪费了。下面就将解析安卓的四种启动方式。如有错误，欢迎指正，此处仅供自己面试学习使用。

android任务栈：我们每次打开一个新的Activity或者退出当前Activity都会在一个称为任务栈的结构中添加或者减少一个Activity组件，一个任务栈包含了一个activity的集合。android通过ActivityRecord、TaskRecord、ActivityStack、ActivityStackSupervisor，ProcessRecord有序地管理每个activity。

一：Standard 标准模式
这是android的默认启动方式，即使不在AndroidManifest.xml里面设置launchMode，也是默认的这个模式。每次启动一个A activity都会创建一个A activity的实例入栈，无论A activity是否存在。
生命周期：onCreate；onStart；onResume都会被调用。
举个例子：任务栈中有A、B、C三个activity，此时C处于栈顶，<a>C的启动模式为Standard。若C跳转到 C；结果还会有一个C activity进入栈中，成为栈顶</a>。

二：SingleTop栈顶复用模式
此模式分为2中情况：（1）如果需要创建的activity已经位于栈顶，此时直接复用该栈顶activity，不再创建新的activity；（2）如果要创建的activity不处于栈顶，此时才会创建一个新的activity入栈，同Standard一样。
生命周期：第一种情况：onCreate 、onStart不会被系统调用，因为他没有什么改变，但是onNewIntent会被调用（activity被正常创建的时候不会调用这个方法）；第二种情况同Standard模式。
举个栗子：activity栈中有三个activity，分别是A、B、C。C处于栈顶，且为SingleTop模式。（1）情况1，C中加入点击事件，跳转到C中，此时的结果是复用栈顶的C。（2）情况2，C中加入点击事件跳转到A。结果是创建一个新的A 入栈，A成为栈顶。

三：SingleTask栈内复用模式
说明：如果创建的A activity已经处于栈中，此时不会创建新的Activity，而是会将A activity上面的其他activity摧毁，使得A成为栈顶。
生命周期：同SingleTop模式一样，只会回调一次onNewIntent方法。
举个栗子：此时有A、B、C三个activity，C位于栈顶，启动模式为SingleTask。（1）情况一，C中加入点击事件，跳转到C，此时直接复用栈顶的C Activity。（2）情况二，C跳到A ，会将A之上的所有activity销毁，使A成为 栈顶。

四：SingleInstance单实例模式
说明：全局单例模式，加强版的SingleTask模式。具有所有SingleTask的特性，除此之外，该模式的activity仅仅能单独位于一个任务栈中，这个经常应用于系统的应用中，如，锁屏，Launch等等，整个系统中仅仅有一个,用的不多
————————————————
版权声明：本文为CSDN博主「微光c」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_39178790/article/details/122472279

# 6、多线程、异步任务

Java多线程技术：

1、Thread

```
public static void test() {
    new Thread() {
        int i = 0;
        @Override
        public void run() {
            super.run();
            while (true){
                System.out.println("线程计数 " + (i++));
                try {
                    sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }.start();
}
```

2、实现Runnable接口

```
Runnable runnable = new Runnable() {
    int  i = 0;
    @Override
    public void run() {
        while(true){
            i++;
            System.out.println("线程计数 " + i);
            try {
                sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
};
Thread thread = new Thread(runnable);
thread.start();
```



3、Callable<>带返回值

```
Callable<String> callable = new Callable<String>() {
    int i = 0;
    @Override
    public String call() throws Exception {
        while(true){
            i++;
            System.out.println("线程计数:" + i);
            if(i >= 10){
                break;
            }
        }
        return "执行完成";
    }
};
FutureTask futureTask = new FutureTask(callable);
futureTask.run();
String result = (String)futureTask.get();
System.out.print("result = "+ result);
```

Callable和Runnable都是接口，都应该实现其方法然后作为Thread的构造参数后，通过Thread对象来操作线程

**Callable和Runnable的区别：**
① Callable有返回值，用泛型作为参数
② Callable可以抛出异常
③ Callable的方法是call()，Runnable的方法是run()

4、线程池















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