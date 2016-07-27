# 以Debian系统为例安装Shadowsocks服务

标签（空格分隔）： VPN

---

测试用Linux版本为搬瓦工Debian8 x64 新装系统

先升级apt-get

```
sudo apt-get update
sudo apt-get upgrade
```

然后开始安装

```
apt-get install python-pip
pip install shadowsocks
```

这时Shadowsocks已经可以用了，但是我们为了提高科学上网的速度，还要添加一些配置。

---

转自GitHub

# net-speeder
net-speeder 在高延迟不稳定链路上优化单线程下载速度 

项目由https://code.google.com/p/net-speeder/  迁入


关注微信公众号了解最新开发进度/获取帮助/提出建议：

<img src="http://www.snooda.com/images/qrcode.jpg" />


A program to speed up single thread download upon long delay and unstable network

在高延迟不稳定链路上优化单线程下载速度

注1：开启了net-speeder的服务器上对外ping时看到的是4倍，实际网络上是2倍流量。另外两倍是内部dup出来的，不占用带宽。
另外，内部dup包并非是偷懒未判断。。。是为了更快触发快速重传的。
注2：net-speeder不依赖ttl的大小，ttl的大小跟流量无比例关系。不存在windows的ttl大，发包就多的情况。


安装步骤：

1：下载源码并解压

    wget https://github.com/snooda/net-speeder/archive/master.zip
    unzip master.zip

2：准备编译环境

debian/ubuntu：

    #安装libnet-dev：
    apt-get install libnet1-dev
    #安装libpcap-dev：
    apt-get install libpcap0.8-dev 

centos： 

    #下载epel：https://fedoraproject.org/wiki/EPEL/zh-cn 例：CentOS6 64位：
    wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
    #（如果是centos5，则在epel/5/下）
    #安装epel：
    rpm -ivh epel-release-6-8.noarch.rpm
    #然后即可使用yum安装：
    yum install libnet libpcap libnet-devel libpcap-devel

编译：

Linux Cooked interface使用编译（venetX，OpenVZ）：

    sh build.sh -DCOOKED

普通网卡使用编译（Xen，KVM，物理机）：

    sh build.sh

使用方法(需要root权限启动）：

    #参数：./net_speeder 网卡名 加速规则（bpf规则）
    #ovz用法(加速所有ip协议数据)： 
    ./net_speeder venet0 "ip" 

> 注意这里ip是一个变量，不要输入自己的IP，搬瓦工的网卡是venet0

---

接下来继续配置shadowsocks，我们使用配置文件进行配置，方法创建/etc/shadowsocks.json文件，填入如下内容：

```
{
    "server":"my_server_ip",
    "server_port":8000,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"mypassword",
    "timeout":300,
    "method":"rc4-md5"
}
```

加密方式推荐使用rc4-md5，因为 RC4 比 AES 速度快好几倍，如果用在路由器上会带来显著性能提升。旧的 RC4 加密之所以不安全是因为 Shadowsocks 在每个连接上重复使用 key，没有使用 IV。现在已经重新正确实现，可以放心使用。

---

运行shadowsocks 

```
ssserver -c /etc/shadowsocks.json -d start
```

如果要停止运行，将命令中的start改成stop。

---






