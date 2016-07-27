# PhpStorm 配置在浏览器中打开文件

标签（空格分隔）： PHP

---

关于PhpStorm的中文资料比较少,需要花好长时间去了解PhpStorm

刚开始使用PhpStorm时有可能遇到这个问题,以下面的网页为例

![1.png](https://ooo.0o0.ooo/2016/02/20/56c80f5e0ef6c.png)

从PhpStorm中直接打开浏览器会发现打开了`http://localhost:35771/www/index.html`,这样情况下,当你用POST方法提交一个表单时,在后端并不能接收到数据

![2.png](https://ooo.0o0.ooo/2016/02/20/56c8114e6a7ae.png)

而通过wamp直接在浏览器中输入localhost在提交表单却能够获得数据

下面写一下我的解决办法:

点击File-Settings-Deployment 。点+按钮增加服务器


![3.png](https://ooo.0o0.ooo/2016/02/20/56c812c363648.png)
![4.png](https://ooo.0o0.ooo/2016/02/20/56c812c468cac.png)
![5.png](https://ooo.0o0.ooo/2016/02/20/56c812c4862d2.png)

OK,现在打开通过PhpStorm打开浏览器再试试,就可以了























