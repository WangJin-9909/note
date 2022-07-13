1、ubuntu上安装mysql

```shell
sudo apt-get upgrade
sudo apt-get install mysql-server
```

2、在ubunt下使用默认密码登录到mysql

![1657016908132](C:\02.code\note\img\1657016908132.png)

3、配置mysql可以在外部访问，即通过远程得方式

![1657016980956](C:\02.code\note\img\1657016980956.png)

![1657017001772](C:\02.code\note\img\1657017001772.png)

```
  GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '密码'WITH GRANT OPTION;     //任何远程主机都可以访问数据库  
  FLUSH PRIVILEGES;    //需要输入次命令使修改生效  
 
```

 4、使用select host, user from user;查看用户表，若root用户显示host为localhost 则需要授权 root 用户的所有权限并设置远程访问，即步骤3

![1657017522988](C:\02.code\note\img\1657017522988.png)

5、service mysql restart重启MySQL服务