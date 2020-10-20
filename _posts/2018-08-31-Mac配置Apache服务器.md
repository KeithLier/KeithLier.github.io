#Mac上10分钟搞定Apache服务器配置

目的：创建一个专属的测试环境

###一、Apache服务器

>* 使用最广的 Web 服务器

>* Mac自带Apache，只需要修改几个配置就可使用

>* 有些特殊的服务器功能，Apache都能很好的支持

###二、硬件要求

####1. Mac电脑开机密码

####2. MAC 10.10及以上（关于本机查看，当前最新版本是10.13.6）

###三、配置服务器（此过程会用到vim命令）

####1. 服务器操作常见命令

一般来说Mac系统都会自带Apache环境，此过程会要求输入密码，输入时是隐藏的，输入完成直接回车即可。

	sudo apachectl -v　   //查看系统的Apache版本
	ocsudo apachectl -k start   //启动Apache

此步骤过后就可以查看Apche是否已经启动了，在Safari地址栏中输入http://localhost 或 127.0.0.1 ，如果网页中出现 It Work！，已启动成功。


	sudo apachectl -k stop    //停止Apache
	sudo apachectl -k restart   //重启Apache
	
####2. 配置服务器的准备工作

①、在Finder中创建一个"Sites"的文件夹，直接创建在/Users/apple(当前用户名)目录下

②、修改配置文件中的"两个路径"，指向刚刚创建的文件夹(按照4. 流程命令步骤去做）

③、拷贝一个文件(按照4. 流程命令步骤去做）

####3. 配置服务器的注意事项

>* 关闭中文输入法

>* 命令和参数之间需要有"空格"

>* 修改系统文件一定记住"sudo"，否则会没有权限

>* 目录要在/Users/***(当前用户名) : 将你创建的文件夹Sites直接拖放到终端中就可以查看你创建的Apache服务器文件夹路径

####4. 配置服务器流程（以下是终端执行命令）

**1)切换工作目录 到 /etc/apache2**

	cd /etc/apache2
	
**2)备份文件**，以防不测，只需要执行一次就可以了(可以使用ls命令查看是否新增了httpd.conf.bak文件）

	sudo cp httpd.conf httpd.conf.bak

提示：如果后续操作出现错误！可以使用以下命令，恢复备份过的 httpd.conf 文件（此步骤不需执行）

	sudo cp httpd.conf.bak httpd.conf
	
**3)用vim编辑httpd.conf**，需要输入密码（vim里面只能用键盘，不能用鼠标，按 0 将光标移动到首行（0这是零，不是字母o），按 i 进入编辑模式。）

	sudo vim httpd.conf
	
**4)查找DocumentRoot**（command + f 搜索，终端中搜索不支持全文搜索，请切页搜索）修改两个/Library/WebServer/Documents改成自己的服务器文件夹路径（/Users/用户名/Sites）

**5)查找options**（按向下箭头走10行左右）修改`Options FollowSymLinks Multiviews`

加一个单词Indexes 如下

`Options Indexes FollowSymLinks Multiviews`

**6)查找php删除注释**

	#LoadModule php7_module libexec/apache2/libphp7.so 删除掉 #

**7)保存httpd.conf**

按 ESC 退出编辑模式，进入命令模式

	:wq       //保存并退出一下 
	:q!       //不保存退出!!!(这一步不需要执行，如果自己输入错了的话执行）
	
**8)切换工作目录 到 /etc**

	cd /etc
	
**9)拷贝php.ini文件**

	sudo cp php.ini.default php.ini
	
####5. 测试 Apache 服务器

	sudo apachectl -k restart      //重新启动apache服务器
	
若出现下图所示警告表示正常

![file-list](/Users/keith/Desktop/github/KeithLier/img/reminder.jpg)

在浏览器地址栏输入 127.0.0.1，刷新页面，可能还是显示**it Work！**请清空一下**safari-->”清除历史记录和网站数据"**，刷新页面。

如果你想页面里面多些内容，可以创建个demo.json，放一段json文本在里面，把它放到Sites文件夹里面，刷新页面。

Apache是一个服务器，为了保证用户的安全，每次重新启动计算机Apache不会自动启动，需要进入终端，手动启动一次。


###推荐一个还算不错的网站 [json在线编辑工具](http://www.bejson.com/jsoneditoronline/)

