# 从零开始配置Apache+MySQL+PHP（Windows版）

标签（空格分隔）： PHP

---

[TOC]

---

###说明

以前总是用一键安装包来搭建开发环境，总觉得还不够深入，这次通过阅读安装包内的英文说明文档使用官方安装包单独进行安装，算是加深理解吧。如果有时间再去配置一下linux系统的开发环境

如果是刚刚入门，不想太麻烦的请直接搜索 wamp/xampp/appserv

---

平台：win10 64位

---



---
###准备

####Apache的下载
进入apache官网  https://httpd.apache.org/

![1.jpg](https://ooo.0o0.ooo/2016/03/18/56ecc87c242fb.jpg)

找到Apache httpd 2.4.18 Released 

点击download 进入下载选项

![2.jpg](https://ooo.0o0.ooo/2016/03/18/56ecc87c3c5e7.jpg)

选择 Files for Microsoft Windows

![3.jpg](https://ooo.0o0.ooo/2016/03/18/56ecc87c3ddcf.jpg)

这个大意是说apache本身不提供已编译的安装包，只提供源码，如果你自己无法编译，可以选择下面这些官方推荐的第三方提供编译的网站。
其中后两个是有名的wamp以及xampp集成环境，如果只想下载apache可以选择前三个网站，这里我们第一个ApacheHaus为例。

![4.jpg](https://ooo.0o0.ooo/2016/03/18/56ecc87c3dab2.jpg)

我们选择 Apache 2.4.18 x64 with Open SSL

下载下来的是一个压缩包。把它移动到你想放置的地方，我把它放在C:\wamp目录下

####MySQL的下载

进入 MySQL官网 http://www.mysql.com/

![5.jpg](https://ooo.0o0.ooo/2016/03/19/56ece2a63fcf5.jpg)

点击Downloads

![6.jpg](https://ooo.0o0.ooo/2016/03/19/56ece2a641a05.jpg)

选择windows

![7.jpg](https://ooo.0o0.ooo/2016/03/19/56ece3543fccd.jpg)

下载完整版安装包，后面安装时顺便安装MySQL的可视化管理程序

![8.jpg](https://ooo.0o0.ooo/2016/03/19/56ece3df2ce0f.jpg)

####PHP的下载

进入PHP官网 http://php.net/

（小插曲： 在这篇文章完成的时候，想再回去看看php官方的文档，结果发现官网挂了，不知道什么时候会修好。。。3月21日）

![QQ截图20160321001854.jpg](https://ooo.0o0.ooo/2016/03/20/56eecf2437a31.jpg)

点击Download

![QQ截图20160321001921.jpg](https://ooo.0o0.ooo/2016/03/20/56eecf2426463.jpg)

选择Windows Download

![QQ截图20160321002031.jpg](https://ooo.0o0.ooo/2016/03/20/56eecf242cbd4.jpg)

选择 Thread Safe （根据个人需求选择，选择线程安全，后面会解释为什么）

依据请看
http://blog.csdn.net/kongdeqian1988/article/details/7919828

---

###安装

####Apache的安装

1. 首先你点电脑中应该安装了 Visual C++ 2008 Redistributable Package
2. 测试Apache： 进入Apache的bin目录，shift+右键选择在此处打开命令窗口，输入httpd看是否有错误提示，如果没有错误提示，打开浏览器，在地址栏输入`localhost`，将会看到Apache的介绍页面，此页面实际位置在Apache目录htdocs的目录下。
> 这里可能会出现一个报错，`ServerRoot must be a valid directory`，这是因为conf目录下的httpd.conf文件中的Apache地址与实际地址不同造成的，可以修改httpd.conf文件中第38和39行
第38行是定义的一个地址变量，后面就可以引用了
`
Define SRVROOT "实际安装地址"
ServerRoot "${SRVROOT}"
`
3. 如果以上没问题就可以将Apache安装为后台服务了。命令为：
```
httpd -k install
```
启动Apache服务
```
httpd -k start
```
其他命令
```
Stop Apache	 	httpd -k stop
Restart Apache	httpd -k restart
Uninstall Apache Service	httpd -k uninstall
Test Config Syntax	httpd -t
Version Details	httpd -V
Command Line Options List	httpd -h
```

附极客学院 关于Apache配置的课程 http://www.jikexueyuan.com/course/1224_1.html

####MySQL的安装

打开MySQL的安装包

按照下面的选择进行安装
MySQLserver就是MySQL的服务器
MySQL Workbench 是MySQL的可视化操作管理程序
MySQL Notifier 提供系统通知栏的图标显示

![9.jpg](https://ooo.0o0.ooo/2016/03/20/56ee2efa4148c.jpg)

一直点下一步就好了

![10.jpg](https://ooo.0o0.ooo/2016/03/20/56ee859b4f551.jpg)

在设置MySQL密码是输入密码作为数据库管理员的密码

安装好之后打开MySQL workbench 的界面是这样的

![11.jpg](https://ooo.0o0.ooo/2016/03/20/56ee866acf7bf.jpg)

点击箭头所指位置即可查看数据库

关于数据的增删查改请看极客学院 http://www.jikexueyuan.com/course/627_6.html

至此MySQL已经安装完成

####PHP的安装

 
> And as you'll soon learn, the preferred method for installing PHP is to keep all PHP related files in one directory and have this directory available to your systems PATH.
You may choose a different location but do not have spaces in the path (like C:\Program Files\PHP) as some web servers will crash if you do.

PHP的安装文档中提到，将PHP的目录添加到系统环境变量PATH中，将会更加方便的安装以及升级，另外，PHP的安装目录中不应该出现空格，否则会出现错误。

PHP的安装很简单，只需要将PHP安装包解压到想放置的目录即可，我放在了 C:/wamp/php/ 目录下

PHP文件夹里有两个PHP的配置文件 ，php.ini-development & php.ini-production，作为开发者使用 php.ini-development 就可以了，当然能够自己配置会更好。

将php.ini-development文件重命名为 php.ini 并移动到C:/Windows目录下
原因是安装包默认设置把配置文件放在此目录下，而我们又没办法更改，至少我不会改，我因为没有将配置文件放在此目录下，找了一个下午原因。

php.ini，将extension_dir="./" 改成 extension_dir="安装目录/ext";

去掉以下三行的分号:extension=php_mbstring.dll ,extension=php_gd2.dll,extension=php_mysql.dll。

查找date.timezone，去分号，改成date.timezone=PRC。

PHP已经安装好了

---

###连接

####Apache与PHP的连接

打开apache的配置文件httpd.conf,在DirectoryIndex index.html前加一空格后添加index.php。

查找# LoadModule foo_module modules/mod_foo.so，在此添加一行

```
LoadModule php7_module "C:/wamp/php/php7apache2_4.dll"
```

查找AddType application/x-gzip .gz .tgz,加一行

```
AddType application/x-httpd-php .php
```

文件最后加上

```
<IfModule php7_module>
	PHPIniDir ‪C:/wamp/php/php.ini
</IfModule>
```

> 测试，将下面代码复制到新建文本文档中，保存为index.php，放在 Apache 的 htdocs 目录下，打开浏览器输入localhost，回车，此时应该能看到PHP的详细信息

```php
<?php
    phpinfo();
?>
```

####PHP与MySQL的连接

PHP 的配置文件为 php.ini 也就是刚刚我们放到C:/Windows目录下的文件。
大多数扩展功能我们都是通过修改php.ini文件来实现的

数据库的扩展也是通过修改php.ini实现的
找到下图所示部分，去掉一些分号
![QQ截图20160321165307.jpg](https://ooo.0o0.ooo/2016/03/21/56efb7932c31e.jpg)
其中gd2是图形库
mysqli和mysql是数据库
其他的作用暂不清楚。

现在如果测试没有问题，就应该是配置好了PHP&MySQL的开发环境

---

####PHPMyAdmin的安装

有时候MySQL workbench 用起来太大才小用了，这时候用PHPMyAdmin就比较方便了，这是一个通过网页来控制MySQL的一个程序

官网 https://www.phpmyadmin.net/

从官网下载 PHPMyAdmin 直接解压到 Apache/htdocs目录下，将文件夹名称改为phpMyAdmin，这样就可以通过访问
http://localhost/phpMyAdmin来操作数据库了。

---

以上是我花了近两天时间读说明文档，利用谷歌等搜索引擎来科学的配置PHP开发环境的过程。前面花了大量时间来找官方的安装包是为了给强迫症患者准备的（比如我。。。）。

如有错误，欢迎指正。

























































