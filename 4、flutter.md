1、查看flutter 版本  

flutter --version

2、显示所有log操作

flutter -v



在flutter中，所有的组件都是类，如Center组件就是Center类







组件：

Material组件：android风格的组件

Cupertino组件：iOS风格的组件

Text：文本、Image：图片、Icon：显示图标、Container：容器，类似于div、Row、Column：水平和垂直排列组件、Stack：Z轴方向的多组件、Scaffold：页面基本组件

## MaterialApp：

theme：配置主题，取值有ThemeData(primarycolor：Colors.yellow)

## ListView：

ListView通常替换Colum，当用户弹出键盘时候，ListView支持滚动，而Column不支持

## Column：

## Row:

mainAxisAlignment:设置主轴居中类型，取值为MainAxisAlignment类型,里面有枚举值

## Icon：

## IconButton：

## Text:

## TextField:   用于接收用户输入



obscureText：用户控制是否暗码显示内容



## Issue：

### 1、TextField

TextField不能直接放到Row里面，需要在外面套一层Expanded，否则会引起报错

![1651027242918](D:\02.work_in_guomei\img\1651027242918.png)





## InputDecoration：

 suffixIcon:尾缀图标























工程目录结果结构：

pubspec.yaml：项目的配置文件，包含项目名称、项目环境、依赖等，需要新的依赖库要放在此文件内说明





![1650421043513](C:\02.code\note\img\1650421043513.png)

{}表示可选参数，不在{}里面声明的参数为必选参数，{}里的到底是不是可选参数呢？？？