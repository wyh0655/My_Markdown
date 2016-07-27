# 快速配置 Sublime Text

标签（空格分隔）： Sublime C/C++ 

---

> 注:文中的程序安装包也可以从我的百度云链接进行下载
链接: http://pan.baidu.com/s/1i3SXL1F 密码: rht4

---
##安装

首先进入[Sublime官网](http://www.sublimetext.com/)下载 `portable` 版本的 sublime .

`portable` 版本的 sublime 是免安装的,直接解压即可.

---
##注册

Sublime Text是一个收费闭源软件.然而还是有人弄到了他的注册码.在这里提供四组注册码.

Sublime text 3(Build 3103) license key shared by [Mrxn Blog](http://www.mrxn.net) Feel free to enjoy them ^_^.

随机复制下面的几四个注册码 粘贴到sublime text 3(Build 3103)注册框 就可以了！

第一个--first licence key :

```
Michael Barnes
Single User License
EA7E-821385
8A353C41 872A0D5C DF9B2950 AFF6F667
C458EA6D 8EA3C286 98D1D650 131A97AB
AA919AEC EF20E143 B361B1E7 4C8B7F04
B085E65E 2F5F5360 8489D422 FB8FC1AA
93F6323C FD7F7544 3F39C318 D95E6480
FCCC7561 8A4A1741 68FA4223 ADCEDE07
200C25BE DBBC4855 C4CFB774 C5EC138C
0FEC1CEF D9DCECEC D3A5DAD1 01316C36
```

第二个--second licence key :
```
Nicolas Hennion
Single User License
EA7E-866075
8A01AA83 1D668D24 4484AEBC 3B04512C
827B0DE5 69E9B07A A39ACCC0 F95F5410
729D5639 4C37CECB B2522FB3 8D37FDC1
72899363 BBA441AC A5F47F08 6CD3B3FE
CEFB3783 B2E1BA96 71AAF7B4 AFB61B1D
0CC513E7 52FF2333 9F726D2C CDE53B4A
810C0D4F E1F419A3 CDA0832B 8440565A
35BF00F6 4CA9F869 ED10E245 469C233E
```

第三个--third licence key :
```
Anthony Sansone
Single User License
EA7E-878563
28B9A648 42B99D8A F2E3E9E0 16DE076E
E218B3DC F3606379 C33C1526 E8B58964
B2CB3F63 BDF901BE D31424D2 082891B5
F7058694 55FA46D8 EFC11878 0868F093
B17CAFE7 63A78881 86B78E38 0F146238
BAE22DBB D4EC71A1 0EC2E701 C7F9C648
5CF29CA3 1CB14285 19A46991 E9A98676
14FD4777 2D8A0AB6 A444EE0D CA009B54
```

第四个--fourth licence key :
```
Alexey Plutalov
Single User License
EA7E-860776
3DC19CC1 134CDF23 504DC871 2DE5CE55
585DC8A6 253BB0D9 637C87A2 D8D0BA85
AAE574AD BA7D6DA9 2B9773F2 324C5DEF
17830A4E FBCF9D1D 182406E9 F883EA87
E585BBA1 2538C270 E2E857C2 194283CA
7234FF9E D0392F93 1D16E021 F1914917
63909E12 203C0169 3F08FFC8 86D06EA8
73DDAEF0 AC559F30 A6A67947 B60104C6
```

---

##安装Package Control

Sublime Text支持大量插件，如何找到并管理这些插件就成了一个问题，Package Control正是为了解决这个问题而出现的，利用它我们可以很方便的浏览、安装和卸载Sublime Text中的插件。

> * 使用`Ctrl + ~ `打开Sublime Text控制台。
> * 将下面的代码粘贴到控制台里：

Sublime Text 3
```
import urllib.request,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```
Sublime Text 2
```
import urllib2,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
```
> * 等待Package Control安装完成。之后使用`Ctrl + Shift + P`打开命令板，输入PC应出现Package Control

成功安装Package Control之后，我们就可以方便的安装使用Sublime Text的各种插件

---

##配置C/C++开发环境




---
###导读

`sublime text 3`提供了构建功能，它的构建系统`（Build systems）`可以运行一段外部命令，还可以捕获输出并显示。
要在`sublime text 3`中实现`c`或`c++`代码的编译和运行，在本质上说也是调用外部的命令，`windows`中也可以理解为执行一段`cmd`命令。
目前`c/c++`编译器最流行的就是`gcc`和`g++`，本文将先介绍`gcc`和`g++`的基本命令格式，然后介绍`win7 64bit`下 `Sublime Text 3 build 3103`版本中`build`配置文件的编写。

---
###关于gcc和g++
---

安装编译器是后面所有工作的基础，如果没有编译器，后面的一切都无从谈起。在`windows`下使用`gcc`和`g++`，是通过安装`MinGW`实现的。


####安装MinGW

`MinGW`是`Minimalist GNU on Windows`的首字母缩写，安装后就可以使用很多的`GNU`工具。`GNU（GNU’s Not Unix）`是`linux`中的一个著名的项目，包含了`gcc\g++\gdb`等工具。也就是说，安装`MinGw`后，我们就可以使用`gcc`和`g++`命令了。

您可以从[MinGW的官网](http://www.mingw.org)下载最新版本的`MinGW `进行安装.直接解压到`C:\MinGW`目录下.

####在cmd中使用gcc

假设我们有一个`test.c`文件在Z盘的`work`目录下。首先我们要在`cmd`中进入此目录。方法可以是在`work`目录空白处按住`Shift`点击鼠标右键，选择“在此处打开命令窗口”；也可以使用`cd`命令进入。

gcc的一般格式是
> gcc 源文件名 -o 可执行文件名

但是我们输入命令
> gcc test.c -o test

执行后却提示
> ‘gcc’ 不是内部或外部命令，也不是可运行的程序或批处理文件。

这是因为命令执行时，会在当前目录下查找名为`gcc`的可执行文件，如果查不到就在系统环境变量`path`记录的路径里寻找`gcc`可执行文件。但是目前这两个地方都没有。我们的`gcc`文件所在的目录是c盘下的`MinGW/bin`。
这时可以使用绝对路径来调用`gcc`可执行文件

```
Z:\work>c:/MinGW/bin/gcc test.c -o test
 
Z:\work>test.exe
hello world
```
这样就成功编译生成了可执行文件test.exe，然后就可以在cmd里运行了。

####配置环境变量

为了方便，一般我们会把gcc所在的路径加入系统的环境变量，这样就可以直接使用gcc命令而不用绝对路径。

> 右键计算机->属性->高级系统设置->环境变量

> * 在PATH里加入`C:\MinGW\bin` 记得，如果里面还有其他的变量，记得要加个分号啊，分号得在英文输入模式下输入的。 
> * 新建`LIBRARY_PATH`变量，如果有的话，在值中加入`C:\MinGW\lib` 这是标准库的位置。 
> * 新建`C_INCLUDEDE_PATH`变量，值设为`C:\MinGW\include`

> 下面就是要判断一下我们的`MinGW`是否安装成功，直接运行`cmd`命令行，输入`g++ -v` 如果出现`gcc`版本号说明安装成功

配置环境变量也可以用批处理的方法

将下面代码复制,粘贴到新建文本文档中,保存为 .bat 格式 ,右键以管理员身份运行.

```
wmic ENVIRONMENT where "name='path' and username='<system>'" set VariableValue="%path%;C:\MinGW\bin"

wmic ENVIRONMENT create name="LIBRARY_PATH",username="<system>",VariableValue="C:\MinGW\lib"

wmic ENVIRONMENT create name="C_INCLUDEDE_PATH",username="<system>",VariableValue="C:\MinGW\include"

pause 
```
`pause`作用是暂停命令行窗口以便查看环境变量是否添加成功

下面我们就可以输入命令来检验是否成功,当然添加环境变量后不会在 `Sublime Text 3` 中立即生效,需要重启计算机才行.

> gcc test.c -o test

###Sublime Text 3默认c/c++编译系统的不足

####不足之处
> 1. 程序输出捕获到Sublime窗口中，这样导致不能运行时输入信息。执行含有scanf语句的代码会卡住。
2. 默认情况下c和c++没有进行区分，全部当做c++格式来处理了。
解决办法
第一个是设置在新的cmd窗口执行程序，这样就可以输入信息。
第二个是针对c语言单独写一个build配置文件。

####默认的编译配置文件在哪


在Sublime的安装目录的Packages文件夹中，有个文件叫C++.sublime-package
这个实际上是zip的压缩包包含了c++的默认系统设置，修改后缀名为zip后解压，可以在里面找到C++ Single File.sublime-build文件，内容如下：

```json
{
	"shell_cmd": "g++ \"${file}\" -o \"${file_path}/${file_base_name}\"",
	"file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
	"working_dir": "${file_path}",
	"selector": "source.c, source.c++",
 
	"variants":
	[
		{
			"name": "Run",
			"shell_cmd": "g++ \"${file}\" -o \"${file_path}/${file_base_name}\" && \"${file_path}/${file_base_name}\""
		}
	]
}
```

这是JSON格式的配置文件，可以看到 selector部分确实是c和c++都选择的。
我们只要略作修改，就可以实现我们的需要了。
但是这是系统的配置，并不建议修改。建议大家把用户配置放到用户文件夹下，来代替默认的编译配置。


###新建编译系统

---

####c语言

> 选择tool –> Build System –> New Build System
然后输入以下代码

```
{
	"working_dir": "$file_path",
	"cmd": "gcc -Wall \"$file_name\" -o \"$file_base_name\"",
	"file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
	"selector": "source.c",
 
	"variants": 
	[
		{	
		"name": "Run",
        	"shell_cmd": "gcc -Wall \"$file\" -o \"$file_base_name\" && start cmd /c \"${file_path}/${file_base_name} & pause\""
		}
	]
}
```
按Ctrl+s保存，会自动打开user目录（Sublime Text 3\Packages\User），我们修改 文件名为 c.sublime-build，保存在此目录。
这时候，可以在Tools -> Build System下看到刚才新建的c了

> 选中后就可以使用了。
 `Build System`中除了选择具体的编译系统，还可以选择第一个：`Automatic` 自动选择，会根据打开的文件后缀自动选择。由于默认情况`.c`文件`sublime`识别为`c++`类型，所以使用自动选择的时候还需要修改一点：
先用`sublime`打开`.c`文件的时候 默认是`c++`格式
点击右下角处的`c++  `选择`Open all with current extension as .. `然后选择`C`
这样以后打开`.c`文件就默认是c类型
这时候按`Ctrl+Shift+B`
第三个c就是对应执行配置文件中的第三行`  gcc -Wall $file_name -o $file_base_name ` 作用是编译。
第四个`c-Run`对应后面的命令 ` gcc -Wall $file -o $file_base_name && start cmd /c \”${file_path}/${file_base_name} & pause\”` ，作用是是在新的`cmd`窗口运行。这样就可以对`scanf`等函数进行输入了。

---

####C++
gcc虽然可以编译c++代码，但是不能进行c++的连接函数库操作。所以针对c++代码一般使用g++来编译。
方法和上面的c语言的配置一样，只要把配置文件中的gcc改为g++ ，source.c改为source.c++ ，保存文件名c.sublime-build改为c++.sublime-build就可以了。
这里增加了-std=c++11 选项，是按照C++11标准进行编译，不需要的话可以去掉，配置文件如下：

```
{
	"encoding": "utf-8",
	"working_dir": "$file_path",
	"shell_cmd": "g++ -Wall -std=c++11 \"$file_name\" -o \"$file_base_name\"",
	"file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
	"selector": "source.c++",
 
	"variants": 
	[
		{	
		"name": "Run",
        	"shell_cmd": "g++ -Wall -std=c++11 \"$file\" -o \"$file_base_name\" && start cmd /c \"${file_path}/${file_base_name} & pause\""
		}
	]
}
```
这个配置文件编译的时候也会运行  g++ -Wall -std=c++0x $file_name -o $file_base_name && cmd /c ${file_path}/${file_base_name} ，如果只想编译，可以把&&后面去掉就可以了。
实际上，我们可以利用Varians ，来配置多个不同的编译命令。例如下面的配置文件有编译 ，捕获输出运行，cmd运行三种

```
{
	"encoding": "utf-8",
	"working_dir": "$file_path",
	"shell_cmd": "g++ -Wall -std=c++11 \"$file_name\" -o \"$file_base_name\"",
	"file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
	"selector": "source.c++",
 
	"variants": 
	[
		{	
		"name": "Run in sublime",
        	"shell_cmd": "g++ -Wall -std=c++11 \"$file_name\" -o \"$file_base_name\" && cmd /c ${file_path}/${file_base_name}"
		},
		{	
		"name": "CMD Run",
        	"shell_cmd": "g++ -Wall -std=c++11 \"$file\" -o \"$file_base_name\" && start cmd /c \"${file_path}/${file_base_name} & pause\""
		}
	]
}
```

---

###中文编码乱码的问题

---

由于Sublime Text 3中文件默认编码格式是utf-8 ，而windows中的命令行默认编码格式是GBK 。所以代码中出现中文时运行会乱码。
解决思路也很简单，就是让他们编码一致就可以了。

####1. 修改cmd编码为utf-8

使用chcp命令可以查看当前字符集，默认是936 ，可以使用chcp 65001修改字符集为utf-8
然而似乎只对当前打开的窗口有效，一个麻烦的办法是每次代码里运行system来切换字符集（噗）

####2. 修改源代码格式为GBK
Sublime原生并不支持GBK编码，但如果安装了ConvertToUTF8插件，就可以正确显示ANSI或者GBK编码的文件。因此，装插件后打开GBK编码的源代码文件，也不会乱码。
一个更巧妙地办法是使用编译器的选项 -fexec-charset 来设置代码中字符串的编码，这样源文件可以使用utf-8编码，只是编译的时候用指定的编码来编译源代码中的字符串。
在编译命令gcc中加入选项 -fexec-charset=GBK 来说明将代码中的字符串按照GBK编码，从而和CMD窗口一致，也不会乱码。
修改后的c语言的配置文件如下：

```
{
	"working_dir": "$file_path",
	"cmd": "gcc -Wall -fexec-charset=GBK \"$file_name\" -o \"$file_base_name\"",
	"file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
	"selector": "source.c",
 
	"variants": 
	[
		{	
		"name": "Run",
        	"shell_cmd": "gcc -Wall -fexec-charset=GBK \"$file\" -o \"$file_base_name\" && start cmd /c \"${file_path}/${file_base_name} & pause\""
		}
	]
}
```

但是加入这个选项后，如果要编译的不是utf-8 ，而是GBK ，必须还要加入-finput-charset=GBK 选项来制定源代码的编码格式，否则会提示错误
error: converting to execution character set: Illegal byte sequence。
而加入这个选项后编译utf-8又会乱码。。。所以，目前博主还没找到源文件是utf-8编码和gbk编码两种情况下中文都不会乱码的方法。。。


---

###使用makefile编译多个文件


sublime可以使用makefile来编译多个文件，以便支持稍大一点的工程项目。只要在侧边栏中打开相关的文件夹，确保文件夹中包含makefile文件。此时按下Ctrl+Shift+B ，会有make的选项，点击执行就可以了。

---

###sublime-build编译系统配置文件

这个编译文件是JSON文件，遵循JSON的语法。JSON 数据的书写格式是：
“名称”: “值”   例如    “firstName” : “John”
值中如果还有双引号要用转义  \” 来表示

####用到的名称

| 名称         | 含义                              |
|:-----        |-----------------------------------|
|working_dir   | 运行cmd是会先切换到 working_dir指定的工作目录|
|cmd           | 包括命令及其参数。如果不指定绝对路径，外部程序会在你系统的:const:PATH 环境变量中搜索。|
|shell_cmd     |相当于shell:true的cmd ，cmd可以通过shell运行。 |
| file_regex   |该选项用Perl的正则表达式来捕获构建系统的错误输出到sublime的窗口。|
|selector      |	在选定 Tools / Build System / Automatic 时根据这个自动选择编译系统。|
|variants      |用来替代主构建系统的备选。例如Run命令。会显示在tool的命令中。|
|name          |只在variants下面有，设置命令的名称，例如Run。|

####支持的变量

只列举用到的

| 名称        | 含义                                  |
|:------------|:--------------------------------------|
| \$file_path   | 当前文件所在目录路径, e.g., C:\Files. |
| \$file        | 当前文件的详细路径, e.g., C:\Files\Chapter1.txt.|
|\$file_name    |文件全名（含扩展名）, e.g., Chapter1.txt.|
|\$file_extension |当前文件扩展名, e.g., txt.|
|\$file_base_name|当前文件名（不包括扩展名）, e.g., Document.|

变量的使用可以直接使用，也可以使用花括号括起来，例如 \${project_name}
还可以使用:设置默认值  \${project_name:Default}

---

到此,Sublime Text 的 C/C++ 开发环境已经配置好了 ,由于安装 Sublime Text 版本为便携版 ,所以当其他电脑上需要配置开发环境时,只需要将 Sublime Text 的程序文件夹直接复制即可 .
并添加系统环境变量,并安装MinGW (也是可以复制的)


