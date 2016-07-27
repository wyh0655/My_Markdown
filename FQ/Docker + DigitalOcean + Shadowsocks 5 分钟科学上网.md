# Docker + DigitalOcean + Shadowsocks 5 分钟科学上网

标签（空格分隔）： ss

---


> 本文内容来自 http://liujin.me/

5 分钟？就能科学上网？！！！！
有人肯定要说我标题党了，
如果你已经有一个 DigitalOcean(以下简称 DO) 账号或者 一个 VPS，
5 分钟已经算多了。
不信你自己掐表算，不废话，上教程。

PS:

> 因为这是给对服务器不熟悉的新手写的教程，像应该创建独立用户而不是使用 root 操作等涉及服务器安全的问题不在讨论范围内。有兴趣的可以自行 Google, 因为看完此文你已经能科学上网了。^^


> * Q: Shadowsocks 的安装已经足够简单了，为什么要用 Docker？

> * A: 再强调一次，写这个教程的时候，我的假想读者是对 OPS 所知甚少、对科学上网有强烈需求、又想自己折腾一番的初级电脑使用者。在一台全新的主机安装 SS？谁能保证安装过程不会出错？而 Docker 开箱即用，出错率更低。当然还有一个原因，我是强迫症，喜欢 Docker 没道理，也想让更多人认识 Docker.

###你需要准备

1. DO 账号
利益相关：DO 有一个 Referral Program，
用我的小尾巴注册 DO 会马上送你 10 刀，>  [我的小尾巴](https://www.digitalocean.com/?refcode=bd2a266d77af),
10 刀相当于可以免费使用 2 个月，当然你可以无视我。

2. Shadowsocks for OSX 客户端
本文以 Mac 平台客户端为例，SS 有各个平台的客户端 [传送门](https://shadowsocks.com/client.html)，具体使用不再赘述，请自行搜索。

更新：有朋友反映 Shadowsocks for OSX 给的下载链接不能访问，看来 Sourceforge 也被认证了，提供一个网盘链接给大家：[ShadowsocksX-2.6.3.dmg 百度网盘](http://pan.baidu.com/s/1kV6OoNt)

###服务端配置

#####创建一个 Droplet

![图一.png](https://ooo.0o0.ooo/2016/07/12/57847b148ec04.png)

![图二.png](https://ooo.0o0.ooo/2016/07/12/57847b14a3ad2.png)

#####安装 Shadowsocks

1. 首先先连上刚刚创建好的主机
2. 接下来安装 Shadowsocks (以下简称 SS)
现在就是见证 docker 的强大之处的时候了，安装 SS 你只需要：

```
docker pull oddrationale/docker-shadowsocks
```

完成后再输入

```
docker run -d -p 1984:1984 oddrationale/docker-shadowsocks -s 0.0.0.0 -p 1984 -k password -m rc4-md5
```

1984是端口号
password是密码
rc4-md5是数据传输加密方式
