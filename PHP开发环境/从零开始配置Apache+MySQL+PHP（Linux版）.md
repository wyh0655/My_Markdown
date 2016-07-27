# 从零开始配置Apache+MySQL+PHP（Linux版）

标签（空格分隔）： PHP

---

> 假设你新安装的 CentOS 7 系统，从头开始配置环境。

[TOC]

---

###First of All

增加权限：目的是在非root用户下能够使用sudo命令

```
su root
visudo

在下面这一行添加
root ALL=(ALL)    ALL

用户名 ALL=(ALL)   ALL
```

update：升级系统

```
sudo yum update 

yum　info updates

yum -y update
升级所有包，改变软件设置和系统设置,系统版本内核都升级

yum -y upgrade
升级所有包，不改变软件设置和系统设置，系统版本升级，内核不改变

-y ：当安装过程提示选择全部为"yes"
```

Xshell有个好处是传输文件只需要拖进去就行了。
所以这里我习惯用Xshell传输文件
用rz、sz命令在Xshell传输文件

```
yum install lrzsz -y
```

解压zip软件

```
yum install zip unzip  
```

编译器GCC

```
yum install gcc gcc-c++
```

安装zlib

```
yum install zlib-devel
```

安装vim

```
yum install vim
```

---

###Apache的安装

需要的安装包
httpd、apr、apr-util、pcre

```
tar xzf httpd-2.4.18.tar.gz
tar xzf apr-1.5.2.tar.gz
tar xzf apr-util-1.5.4.tar.gz
unzip pcre-8.38.zip
```

```
cd pcre-8.38
./configure && make && make install

```

```
cp -r /lamp/apr-1.5.2 /lamp/httpd-2.4.18/srclib/apr
cp -r /lamp/apr-util-1.5.4 /lamp/httpd-2.4.18/srclib/apr-util
cd httpd-2.4.18
./configure --prefix=/usr/local/apache2/ --sysconfdir=/usr/local/apache2/etc/ --with-included-apr --enable-so --enable-deflate=shared --enable-expires=shared --enable-rewrite=shared
make
make install
```

解释

```
--prefix=/usr/local/apache2/：指定Apache软件安装的位置
--sysconfdir=/usr/local/apache2/etc/：指定Apache服务器的配置文件存放位置
--with-included-apr：为了增加编译效率，是C里面的东西，可以不用去管它
--enable-so：apache可以包含和支持一些动态模块（linux的模块是以so结尾的）
--enable-deflate=shared：支持网页压缩模块，与网站加速有关
--enable-expires=shared：支持 HTTP 控制模块，与网站加速有关
--enable-rewrite=shared：支持 URL 重写模块
```

安装好之后启动时会报一个错

```
[root@localhost httpd-2.4.18]# /usr/local/apache2/bin/apachectl start
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using localhost.localdomain. Set the 'ServerName' directive globally to suppress this message
```

进入apache的配置文件目录，然后编辑apache配置文件:
```
cd /usr/local/apache2/etc
vim httpd.conf
```
将里面的#ServerName www.example.com:80注释去掉保存退出即可。

现在重启apache，就不会出现这个警告了：
```
/usr/local/apache2/bin/apachectl restart
```
查看apache服务是否启动：ps -ef |grep httpd （可能有些人会问：为什么是httpd而不是apache，因为apache的进程名称就叫httpd，而不是叫apache）

先清空centos操作系统的防火墙策略：
```
iptables -F 
```
然后再通过实体机浏览器输入地址访问：http://虚拟机ip地址（我这里是：http://192.168.0.17），若显示“It works”即表明Apache正常工作。

> 恭喜你，你的apache安装成功啦！去喝杯茶庆祝一下吧！！！

---

###MySQL的安装

接下来我们继续

需要的安装包
mysql、boost、

MySQL要装 cmake

```
yum install cmake
tar xzf ncurses-6.0.tar.gz
tar xzf mysql-boost-5.7.12.tar.gz
tar xzf boost_1_60_0.tar.gz
tar -zxf bison-3.0.tar.gz
```

源码装boost库,这个问题会很多，自己去Google吧

```
cd boost_1_60_0
./bootstrap.sh
./b2 install
```

安装ncurses

```
cd ncurses-6.0
./configure --with-shared --without-debug --without-ada
make
make install
```

安装bison

```
yum install m4
cd bison-3.0
./configure
make
make install
```



```
rm -rf CmakeCache.txt
```

```
yum group install "Development tools"
```

在安装包之前我们首先查看http php  mysql是否安装 rpm -qa |grep -E “http |php|mysql”若安装过了，则需要卸载  yum remove httpd 且删除/etc下的httpd目录及所有内容


```
检查kernel版本指令是 uname –r

详细版本
cat /proc/version

cat /etc/*-release

CentOS Linux release 7.2.1511 (Core) 
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"

CentOS Linux release 7.2.1511 (Core) 
CentOS Linux release 7.2.1511 (Core) 


标准档案（可被修改）
cat /etc/issue 

查看所有硬件的型号
dmidecode | more

查看memory info
cat /proc/meminfo | more

查看CPU info
cat /proc/cpuinfo

查看磁盘信息
df -lh

```

```
更新系统时间
ntpdate time.windows.com;/sbin/hwclock -w

更新下载源
sudo yum clean all
sudo yum makecache
sudo yum update

clean all 清除缓存
makecache 建立一个缓存，以后用install安装软件时就在缓存中搜索，提高了速度。
```



### Apache服务器的安装与部署

Apache的服务httpd查询与卸载

```
# rpm -qa |grep httpd
# rpm -e --nodeps httpd*
# for name in `rpm -qa httpd*`;do rpm -e --nodeps $name;done
```
注意：如果服务器默认安装了httpd，如果要编译安装，那要使用上述命令将httpd服务器删除
```
# rpm -qa |grep httpd     # 查询服务器的是否安装了httpd
# rpm -e --nodeps httpd*  #
```
卸载有过httpd的服务，上面没有安装，所以出现error
第四行代码：将查询和卸载合二为一

Apache服务http安装包和验证包下载
通过 `wget`命令下载
例：


```
安装包
# wget -O httpd.tar.gz http://www-us.apache.org/dist//httpd/httpd-2.4.18.tar.gz
验证文件
# wget -O httpd.tar.gz.asc https://www.apache.org/dist/httpd/httpd-2.4.18.tar.gz.asc
# wget -O httpd.tar.gz.md5 https://www.apache.org/dist/httpd/httpd-2.4.18.tar.gz.md5
# wget -O httpd.tar.gz.sha1 https://www.apache.org/dist/httpd/httpd-2.4.18.tar.gz.sha1

```

如果在生产环境，那么我们必须将我们下载的安装包进行检测，看看是否被修改。这是一个安全的常识，官网提供了三种验证方式，推荐的是下面这种验证方式。

```
[root@localhost opt]# gpg --verify httpd.tar.gz.asc httpd.tar.gz
gpg: directory `/root/.gnupg' created
gpg: new configuration file `/root/.gnupg/gpg.conf' created
gpg: WARNING: options in `/root/.gnupg/gpg.conf' are not yet active during this run
gpg: keyring `/root/.gnupg/pubring.gpg' created
gpg: Signature made Tue 08 Dec 2015 12:32:07 PM PST using RSA key ID 791485A8
gpg: Can't check signature: No public key
[root@localhost opt]# gpg --verify httpd.tar.gz.asc httpd.tar.gz
gpg: Signature made Tue 08 Dec 2015 12:32:07 PM PST using RSA key ID 791485A8
gpg: Can't check signature: No public key

// 原因：We don't have the release manager's public key ( 791485A8 ) in our local system. You now need to retrieve the public key from a key server. One popular server is pgpkeys.mit.edu (which has a web interface ). The public key servers are linked together, so you should be able to connect to any key server.

理论上应该通过mit能查到，但是，，，显示代理错误，看来这个方法行不通
gpg --keyserver pgpkeys.mit.edu --recv-key 791485A8
gpg: requesting key 791485A8 from HKP keyserver pgpkeys.mit.edu
gpg: trustdb created
gpg: key 791485A8: public key "Jim Jagielski <jim@apache.org>"
imported
gpg: Total number processed: 1
gpg:           imported: 1
```
现在无法继续验证下去了，如果以后有需求，到Apache官网查看验证说明
https://httpd.apache.org/dev/verification.html

---


-------------------


绑定域名（如果没有域名可以跳过）：

```
#cd /etc/httpd/conf.d/
```

我们cat一下README里面的内容，大概的意思是所有以".conf"结尾的文件将被服务所处理，所以我们设置一个网站域名文件在这里来实现绑定域名配置。

模版配置文件在httpd的主配置文件末尾，我们用以下命令来复制一个(注意复制后的文件名一定要是".conf")：

```
#tail -n 7 /etc/httpd/conf/httpd.conf >www.none.la.conf
#vim www.none.la.conf
```

这里我以域名作为文件名，为了方便以后修改能找到,中间部分是做301跳转，把不带www的域名跳转到带www的域名上。

安装配置完成，启动httpd服务

```
#service httpd start
```
![1.png](https://ooo.0o0.ooo/2016/03/25/56f57c3ea67f7.png)


输入服务器域名或者IP查看是否陈功
1.如果不能打开请检查是否iptables没有开放80端口访问权限，可以先停止iptables服务，看是否这个原因造成。

```
#service iptables stop
```

2.如果确定是iptables造成不能访问，编辑iptables来开放访问：

```
#vim /etc/sysconfig/iptables
```

加入以下内容到iptables里面(如下图)：

```
-A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT
```
![2.png](https://ooo.0o0.ooo/2016/03/25/56f57c3eb14fe.png)
重启iptables服务，看看是否配置正确

```
#service iptables restart
```

二、安装Mysql
1.安装mysql

```
#yum -y install mysql-server
```

安装完成，启动mysql服务:

```
#service mysqld start
```

启动的时候会有一些提示信息，提示修改root用户密码等。

2.配置mysql超级用户root的密码：

```
#usr/bin/mysqladmin -u root password '123456'
```

修改密码之后使用命令测试是否正确：

```
#mysql -u root -p123456
```

正常登录表示修改成功，否则再次按上面修改即可。

可以使用命令mysql --help查看帮助，默认配置文件为以下位置的一个：

```
/etc/mysql/my.cnf 或者 /etc/my.cnf 或者~/.my.cnf
```

3.设置默认数据库编码，用root用户登录mysql，输入status查看默认设置状态：

```
mysql>status;
Server characterset:    utf8
Db     characterset:    utf8
Client characterset:    latin1
Conn.  characterset:    latin1
```

修改为所有为utf8编码：

```
#vim /etc/my.cnf
```

在[mysqld]块之后添加：character-set-server=utf8
在[mysql]块之后添加：default-character-set=utf8
如果[mysql]可以自行在最后添加，再添加字符编码语句。

然后再次登录mysql，查看状态，是否全部显示为utf8编码。

4.开启mysql远程链接：
加入以下内容到iptables里面，重启iptables服务：

```
-A INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT
```

用mysql超级用户创建一个普通用户来远程链接数据库（建议不要用root本身来远程链接数据库，不安全）：

```
mysql> grant all privileges on database.* to user@"%"identified by "123456" with grant option;
```


上面紫色部分的字体分别代表是：数据库名、用户名、密码，请修改为你自己的内容。用数据库工具链接测试是否链接上。



三、安装PHP

```
#yum -y install php
```

安装完成php之后，重启httpd服务，在网站根目录下面写一个php文件测试。

```
#vim /var/www/html/index.php
```


我们使用输出php配置信息来测试,在index.php输入以下内容:

```
<？php
phpinfo();
？>
```
安装PHP相关模块：

```
yum install php-mysql php-gd php-imap php-ldap php-odbc php-pear php-xml php-xmlrpc
```

重启httpd服务，查看输出页面信息，如果以上模块信息都有，说明配置成功！

四、服务随开机启动
查看当前启动项的情况

```
#chkconfig --list
```


把httpd和mysqld在开机时启动使用如下命令即可

```
#chkconfig httpd on
#chkconfig mysqld on
```

再次使用chkconfig --list 查看这连个服务的状态（其他服务需要开机启动也是这样操作）

完结。


```
#rpm -ql mysql-server
/etc/logrotate.d/mysqld
/etc/rc.d/init.d/mysqld
/usr/bin/innochecksum
/usr/bin/myisam_ftdump
/usr/bin/myisamchk
/usr/bin/myisamlog
/usr/bin/myisampack
/usr/bin/mysql_convert_table_format
/usr/bin/mysql_fix_extensions
/usr/bin/mysql_fix_privilege_tables
/usr/bin/mysql_install_db
/usr/bin/mysql_secure_installation
/usr/bin/mysql_setpermission
/usr/bin/mysql_tzinfo_to_sql
/usr/bin/mysql_upgrade
/usr/bin/mysql_zap
/usr/bin/mysqlbug
/usr/bin/mysqld_multi
/usr/bin/mysqld_safe
/usr/bin/mysqldumpslow
/usr/bin/mysqlhotcopy
/usr/bin/mysqltest
/usr/bin/perror
/usr/bin/replace
/usr/bin/resolve_stack_dump
/usr/bin/resolveip
/usr/lib/mysql/plugin
/usr/lib/mysql/plugin/ha_archive.so
/usr/lib/mysql/plugin/ha_archive.so.0
/usr/lib/mysql/plugin/ha_archive.so.0.0.0
/usr/lib/mysql/plugin/ha_blackhole.so
/usr/lib/mysql/plugin/ha_blackhole.so.0
/usr/lib/mysql/plugin/ha_blackhole.so.0.0.0
/usr/lib/mysql/plugin/ha_example.so
/usr/lib/mysql/plugin/ha_example.so.0
/usr/lib/mysql/plugin/ha_example.so.0.0.0
/usr/lib/mysql/plugin/ha_federated.so
/usr/lib/mysql/plugin/ha_federated.so.0
/usr/lib/mysql/plugin/ha_federated.so.0.0.0
/usr/lib/mysql/plugin/ha_innodb_plugin.so
/usr/lib/mysql/plugin/ha_innodb_plugin.so.0
/usr/lib/mysql/plugin/ha_innodb_plugin.so.0.0.0
/usr/libexec/mysqld
/usr/libexec/mysqlmanager
/usr/share/doc/mysql-server-5.1.73
/usr/share/doc/mysql-server-5.1.73/my-huge.cnf
/usr/share/doc/mysql-server-5.1.73/my-innodb-heavy-4G.cnf
/usr/share/doc/mysql-server-5.1.73/my-large.cnf
/usr/share/doc/mysql-server-5.1.73/my-medium.cnf
/usr/share/doc/mysql-server-5.1.73/my-small.cnf
/usr/share/man/man1/innochecksum.1.gz
/usr/share/man/man1/msql2mysql.1.gz
/usr/share/man/man1/myisam_ftdump.1.gz
/usr/share/man/man1/myisamchk.1.gz
/usr/share/man/man1/myisamlog.1.gz
/usr/share/man/man1/myisampack.1.gz
/usr/share/man/man1/mysql.server.1.gz
/usr/share/man/man1/mysql_convert_table_format.1.gz
/usr/share/man/man1/mysql_fix_extensions.1.gz
/usr/share/man/man1/mysql_fix_privilege_tables.1.gz
/usr/share/man/man1/mysql_install_db.1.gz
/usr/share/man/man1/mysql_secure_installation.1.gz
/usr/share/man/man1/mysql_setpermission.1.gz
/usr/share/man/man1/mysql_tzinfo_to_sql.1.gz
/usr/share/man/man1/mysql_upgrade.1.gz
/usr/share/man/man1/mysql_zap.1.gz
/usr/share/man/man1/mysqlbinlog.1.gz
/usr/share/man/man1/mysqlbug.1.gz
/usr/share/man/man1/mysqlcheck.1.gz
/usr/share/man/man1/mysqld_multi.1.gz
/usr/share/man/man1/mysqld_safe.1.gz
/usr/share/man/man1/mysqldumpslow.1.gz
/usr/share/man/man1/mysqlhotcopy.1.gz
/usr/share/man/man1/mysqlimport.1.gz
/usr/share/man/man1/mysqlman.1.gz
/usr/share/man/man1/mysqltest.1.gz
/usr/share/man/man1/perror.1.gz
/usr/share/man/man1/replace.1.gz
/usr/share/man/man1/resolve_stack_dump.1.gz
/usr/share/man/man1/resolveip.1.gz
/usr/share/man/man8/mysqld.8.gz
/usr/share/man/man8/mysqlmanager.8.gz
/usr/share/mysql/config.huge.ini
/usr/share/mysql/config.medium.ini
/usr/share/mysql/config.small.ini
/usr/share/mysql/errmsg.txt
/usr/share/mysql/fill_help_tables.sql
/usr/share/mysql/my-huge.cnf
/usr/share/mysql/my-innodb-heavy-4G.cnf
/usr/share/mysql/my-large.cnf
/usr/share/mysql/my-medium.cnf
/usr/share/mysql/my-small.cnf
/usr/share/mysql/mysql_fix_privilege_tables.sql
/usr/share/mysql/mysql_system_tables.sql
/usr/share/mysql/mysql_system_tables_data.sql
/usr/share/mysql/mysql_test_data_timezone.sql
/var/lib/mysql
/var/log/mysqld.log
/var/run/mysqld
```






