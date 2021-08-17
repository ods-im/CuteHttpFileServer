       
## 简介 

CuteHttpFileServer/chfs是一个免费的、HTTP协议的文件共享服务器，使用浏览器可以快速访问。它具有以下特点：

* 单个文件，核心功能无需其他文件 
* 跨平台运行，支持主流平台：Windows，Linux和Mac 
* 界面简洁，简单易用 
* 支持扫码下载和手机端访问，手机与电脑之间共享文件非常方便 
* 支持账户权限控制和地址过滤 
* 支持快速分享文字片段 
* 支持webdav协议

与其他常用文件共享方式（如FTP，飞秋，网盘，自己建站）相比，具有使用简单，适用场景更多的优点，在个人使用以及共享给他人的场景中非常方便快捷。




## 下载
#### 命令行程序
	[版本更新日志](http://iscute.cn/tar/chfs/2.0/chfs-changelog.txt)
	
	    chfs-linux-386-2.0.zip](http://iscute.cn/tar/chfs/2.0/chfs-linux-386-2.0.zip) 
	
	    chfs-linux-amd64-2.0.zip](http://iscute.cn/tar/chfs/2.0/chfs-linux-amd64-2.0.zip) 
	
	    chfs-linux-arm-2.0.zip](http://iscute.cn/tar/chfs/2.0/chfs-linux-arm-2.0.zip)
	
	    chfs-linux-arm64-2.0.zip](http://iscute.cn/tar/chfs/2.0/chfs-linux-arm64-2.0.zip) 
	
	    chfs-linux-mips-2.0.zip ](http://iscute.cn/tar/chfs/2.0/chfs-linux-mips-2.0.zip)
	
	    chfs-linux-mips-softfloat-2.0.zip](http://iscute.cn/tar/chfs/2.0/chfs-linux-mips-softfloat-2.0.zip) 
	
	    ](http://iscute.cn/tar/chfs/2.0/chfs-linux-mips64-2.0.zip)chfs-linux-mips64-2.0.zip 
	
	    ](http://iscute.cn/tar/chfs/2.0/chfs-linux-mips64-softfloat-2.0.zip)chfs-linux-mips64-softfloat-2.0.zip 
	
	   ](http://iscute.cn/tar/chfs/2.0/chfs-linux-mips64le-2.0.zip)chfs-linux-mips64le-2.0.zip 
	
	   ](http://iscute.cn/tar/chfs/2.0/chfs-linux-mipsle-2.0.zip)chfs-linux-mipsle-2.0.zip 
	
	    ](http://iscute.cn/tar/chfs/2.0/chfs-mac-386-2.0.zip)chfs-mac-386-2.0.zip 
	
	   ](http://iscute.cn/tar/chfs/2.0/chfs-mac-amd64-2.0.zip)chfs-mac-amd64-2.0.zip 
	
	   ](http://iscute.cn/tar/chfs/2.0/chfs-windows-x64-2.0.zip)chfs-windows-x64-2.0.zip 
	
	    ](http://iscute.cn/tar/chfs/2.0/chfs-windows-x86-2.0.zip)chfs-windows-x86-2.0.zip 
	
	 [chfs-支持低版本操作系统(MS XP,OpenBSD 6.0...).zip](http://iscute.cn/tar/chfs/2.0/chfs-支持低版本操作系统(MS XP,OpenBSD 6.0...).zip) 

#### GUI程序
    [gui-chfs-windows.zip ](http://iscute.cn/tar/chfs/2.0/gui-chfs-windows.zip) 
# 基本用法
#### 非系统服务运行
该程序是一个控制台程序，可直接双击运行，或在控制台/命令行中运行。可通过命令行参数进行相关配置，如使用'chfs --help'来查看帮助：
```sh
usage: chfs.exe []

Flags:
  --help              Show context-sensitive help (also try --help-long and
                      --help-man).
  --path=DIRECTORIES  Directories where store shared files, separated by '|'.
  --port=PORT         HTTP listening port(Default is 80).
  --allow=LIST        Allowed IPv4 addresses(Allow any address by default).
                      
                      White list mode: "listitem1[,listitem2,...]" e.g.
                      "192.168.1.2-192.168.1.10,192.169.1.222" allows this 10
                      addresses.
                      
                      Black list mode: "not(listitem1[,listitem2,...])" e.g.
                      "not(192.168.1.2-192.168.1.10,192.169.1.222)" bans this 10
                      addresses!
  --rule=LIST         Access rules(anybody can access any thing by default).
                      
                      List defines like:"USER:PWD:MASK[:DIR:MASK...][|...]":
                      
                        1,USER and PWD is account name and password
                        2,MASK:''=NO present,'r'=read,'w'=write,'d'=delete
                        3,r=view+download,w=r+upload+create+rename,d=w+delete
                        4,DIR is directory name, allows wildcard('*' & '?')
                        5,The 3rd field is access mask of shared root directory
                        6,The optional fields is pairs of sub-directory and mask
                        7,The optional sub-directory's mask overwrite parent's
                        8,You should avoid '|' ':' and white space(exclude DIR)
                      
                      For instance: "::|root:123456:rw" bans guest, and defines
                      a account 'root' can do anything
  --log=DIRECTORY     Log directory. Empty value will disable log.
  --file=FILE         A configuration file which overwrites & enhence the
                      settings.
  --version           Show application version.
```
#### 参数说明：
```sh
help:	显示帮助信息
path:	你要共享的目录，默认为程序运行目录。如果需要共享多个目录，则用“|”符号隔开。注意：如果路径带有空格，则需要将整个路径用引号包住。
port:	程序使用的端口号，默认为80
allow:	IP地址过滤，可使用白名单模式或黑名单模式
rule:	账户及访问权限，允许一个账户多点登陆，默认情况下匿名用户具有读写权限，其语法为：

RULEITEM1[|RULEITEM2|RULEITEM3...]

每个RULEITEM代表一个账户信息及其访问权限，多个RULEITEM则用'|'进行分割，RULEITEM的语法为：

USER:PWD:MASK[:DIR:MASK...]

每个项由“:”来分隔，前三个项是必须的，分别对应：账户名、账户密码、共享目录根目录的访问权限。后面的可选的项，必须成对出现，用来设定根目录下面的子级目录的访问权限。一些规定：

* 对于匿名用户，前两个项都为空
* 访问权限分为四种：""(不可访问)，"R"(只读)，"W"(读写)，"D"(写+删除)。读权限指的是下载，写权限指上传、新建等操作，删除权限是在写权限的基础上加上删除权限。
* 各项的值应避免出现空白键，':'及'|'（目录名除外）
log:	用户操作日志存放目录，默认是程序所在目录下的logs中。禁用日志功能只需将其赋值为空即可。
file:	配置文件，该文件可配置上述配置项，语法相同，如果配置有效则覆盖对应配置项。另外，一些功能需要通过配置文件进行配置，比如页面自定义和SSL证书设置。下载配置文件模板
version:	显示程序版本号
```
#### 几个例子：
```sh
//都使用默认参数，共享目录为程序运行目录，监听端口号为80
chfs

//共享目录为D盘，监听端口号为8080
chfs --path="d:/" --port=8080

//共享目录为"d:\\projects"和"e:\\nsis"，监听端口号为80
chfs --path="d:\\projects|e:\\nsis"

//白名单模式，允许192.168.1.2-192.168.1.100以及192.168.1.200进行访问
chfs --allow="192.168.1.2-192.168.1.100,192.168.1.200"

//黑名单模式，禁止192.168.1.2-192.168.1.100以及192.168.1.200进行访问
chfs --allow="not(192.168.1.2-192.168.1.100,192.168.1.200)"

//匿名用户具有只读权限（默认情况下匿名用户具有读写权限）
//账户ceshizu，密码为ceshizu123，对根目录的权限为只读，但对test目录具有读写权限
//账户yanfazu，密码为yanfazu123，对根目录的权限为只读，但对yanfa目录具有读写权限
chfs --rule="::r|ceshizu:ceshizu123:r:test:rw|yanfazu:yanfazu123:r:yanfa:rw"

//匿名用户什么权限都没有（默认情况下匿名用户具有读写权限）
//账户admin，密码为admin123，具有读写权限
//账户zhangsan，密码为zhangsan123，对根目录的权限为不可读写，但对zhangsanfiles目录具有读写权限
chfs --rule="::|admin:admin123:rw|zhangsan:zhangsan123::zhangsanfiles:rw"

//通过配置文件进行配置，该文件可以不存在，待以后需要更改配置时使用
chfs --file="d:\chfs\chfs.ini"
```

Tips 1：在Windows系统中，可以使用右键弹出菜单快捷地共享某个目录。步骤如下：
```sh
1, 下载[注册表模板文件](http://iscute.cn/asset/chfs.reg)
2, 在该文件中编辑你的chfs.exe的真实路径，并可添加其他参数
3, 双击该脚本文件，进行注册表添加</pre>
```
Tips 2：另外，有几个功能需要通过配置文件中进行配置，其中主要的配置项有：
```sh
1, html.title： 自定义网页标题
2, html.notice: 自定义网页顶部的公告板。可以是文字，也可以是HTML标签，此时，需要适用一对``(反单引号，通过键盘左上角的ESC键下面的那个键输出)来包住所有HTML标签
3, ssl.cert和ssl.key: 用来配置SSL，启用HTTPS
4, folder.leaf.download: 仅最后一个目录可以打包下载
5, session.timeout: 会话的时长，单位是分钟</pre>
```
## 以系统服务运行
本程序不是一个服务程序，所以如果你要以系统服务运行，需要自己创建服务。下面给出Windows平台的创建服务方法(通过NSSM工具)：
```sh
1, 将chfs.exe放在指定目录，假设为：d:\program\cutehttpfileserver
2, 到[http://www.nssm.cc/download](http://www.nssm.cc/download)下载nssm
3, 将解压后的nssm程序放在d:\program\cutehttpfileserver中
4, 在d:\program\cutehttpfileserver中运行命令行，或运行命令行并CD至该目录
5, 假设你的服务名称为cute_http_file_service，命令行中输入：nssm install cute_http_file_service
6, NSSM会弹出配置对话框，在该对话框中输入程序路径以及运行参数
7, 启动服务，命令行中输入：nssm start cute_http_file_service</pre>
```
## 高级用法

#### 如何启用HTTPS？
配置文件中有ssl.cert和ssl.key两个键值，设置好对应的文件目录即可。另外，chfs支持的最低SSL版本为SSLv3，不兼容SSL2的握手。对了，别忘了将监听端口设置为443

#### 我想自己搞一套页面，请问开发文档在哪里？
运行chfs后，通过地址:http://host:port/asset/api.html访问API文档。

#### 如何启用webdav？
程序默认支持webdav，跟http共用同一套访问规则。其地址为：http://host:port/webdav


## 测试说明
#### 运行主机
* **Windows XP：**√ 
* **Windows 10：**√ 
* **Debian 9：**√ 
* **CentOS 7：**√ 
* **其他：**未测试 
#### PC浏览器
* **IE：**11+ √ 
* **Edge：**√ 
* **Firefox：**√ 
* **Chrome：**√ 
* **Opera：**√ 
* **Safari：**√ 
* **其他:**未测试 

## 捐助
[捐助地址](https://pay.ods.im/)
