# XX-Net

标签（空格分隔）： XX-Net GoAgent

---
XX-Net  
=================
翻墙工具套件
* GAE proxy, 稳定、易用、快速   
* Web界面，人性化交互  


## 下载(Download)：
测试版(Test)：
https://codeload.github.com/XX-net/XX-Net/zip/2.9.0

稳定版(Stable)：
https://codeload.github.com/XX-net/XX-Net/zip/2.8.9

懒人集成浏览器版（Easy Browser Bundle）:
https://github.com/yeahwu/firefox-xx



## 链接

| 目录 |        |
| --------  | :----  |
|使用方法：|https://github.com/XX-net/XX-Net/wiki/使用方法 |
|更新历史：|https://github.com/XX-net/XX-Net/wiki/更新历史 |
|问题报告: |https://github.com/XX-net/XX-Net/issues |
|讨论群:  |https://groups.google.com/forum/#!forum/xx-net |


---

网上给的说明过于简单,我来演示一遍

![图1.jpg](https://ooo.0o0.ooo/2016/02/23/56cc4bff87909.jpg)

这是下载后解压后的文件夹

> 双击start.bat启动程序 

然后到任务栏找 XX-NET 图标 ,单击一下 ,弹出一个网页来 ,这就是 XX-NET 的 Web 管理界面.如果你只是偶尔翻墙查查资料,这就够了 ,但是你想看 youtube 视频 ,还需要一系列的部署 .

---

### 前期准备
#### 注册 Google 帐号 

请填入手机号，为后面使用appengine做准备
https://accounts.google.com/SignUp

#### 绑定手机号码

https://security.google.com/settings/phone?pli=1
没有绑定手机号码，是不能注册appengine服务的

#### 启用弱安全应用


> 关于两步验证的设置,请移步
http://jingyan.baidu.com/article/ac6a9a5e611b4c2b653eac3e.html

https://www.google.com/settings/security/lesssecureapps
对于多数用户而言，你只需要启用弱安全应用，就可以上传appid

注：如果你已经启用2步登录验证，那么不需要启用弱安全应用，而是设置应用专用密码： https://security.google.com/settings/security/apppasswords
设备选"其他"，随便起个名词，比如GoAgent，点"生成"后，会出来一串密码。 以后就拿这个密码来上传appid部署服务端

---

### 申请appid

1、打开 https://console.developers.google.com/ ，你会看到下图的界面

![图2.png](https://ooo.0o0.ooo/2016/02/23/56cc4ffbc91ba.png)

2、点击该界面中的“Create a project”按钮，会看到如下的界面

![图3.png](https://ooo.0o0.ooo/2016/02/23/56cc4fe7e43bd.png)

1 填入你希望的appid
下面的appid会显示实际给你的appid，建议字母后面加上3-4个数字
2 点选不要发邮件
3 点同意
4 提交

---

### 设置部署权限

如果你没有启用2步登录验证，请启用弱安全应用
https://www.google.com/settings/security/lesssecureapps

如果你已经启用2步登录验证，请设置应用专用密码：
打开 https://security.google.com/settings/security/apppasswords ，并且按照下图操作：


![图4.png](https://ooo.0o0.ooo/2016/02/23/56cc4fde51116.png)

![图5.png](https://ooo.0o0.ooo/2016/02/23/56cc4ff1bc499.png)

![图6.png](https://ooo.0o0.ooo/2016/02/23/56cc4fdd98b2b.png)

![图7.png](https://ooo.0o0.ooo/2016/02/23/56cc4ff56c622.png)

---

### 上传服务端

提示：在部署之前，APPID是无法使用的，不要将他们填入到XX-Net的配置中。
1、打开http://127.0.0.1:8085/?module=goagent&menu=deploy ，按下图说明操作： 

![图8.png](https://ooo.0o0.ooo/2016/02/23/56cc4fde87aae.png)


![图9.png](https://ooo.0o0.ooo/2016/02/23/56cc50000f78c.png)

2、如果你成功做到这一步，那么恭喜你，你即将修成正果，只差最后一步。 打开http://127.0.0.1:8085/?module=goagent&menu=config ，然后老样子看图即可。 

![图10.png](https://ooo.0o0.ooo/2016/02/23/56cc4fdd53b6f.png)

3、当你点击“保存并重启”的那一刻，你就脱离了苦海，视频畅饮，没有任何限制

---

### 一些说明

1、每个GAE应用每天限额流量1G，每个帐号限制12个
2、appid只影响流量，不影响速度

---

如果你想研究更深 :

---

## 如何帮助项目
https://github.com/XX-net/XX-Net/wiki/How-to-contribute


## 集成XX-Net的项目
* ChromeGAE  
  http://www.ccav1.com/chromegae  
  集成Google Chrome和XX-Net的自动翻墙浏览器  
  维护人：Yanu  

* 集成火狐和XX-Net  
  https://github.com/yeahwu/firefox-xx  

* plusburg  
  https://github.com/Plusburg/Plusburg  
  集成XX-Net的启动光盘镜像  

* appifed-xx-net  
  https://github.com/binarydist/appified-xx-net  
  Mac OS X 环境下，变成一个标准的Mac应用  
  
* ComodoDragonPortable:   
  https://github.com/mikedchavez1010/ComodoDragonPortable  
  为XX-Net和Lantern定制的便携浏览器  
  仅支持Windows，心系安全  




