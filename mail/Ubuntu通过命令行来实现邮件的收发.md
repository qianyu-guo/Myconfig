

# 简述

使用mutt和msmtp的组合来实现收发邮件。

msmtp是专门负责邮件发送的SMTP客户端软件，mutt是邮件用户代理客户端，由于是一个代理，所以必须要用到你自己的邮箱（比如163，gmail，outlook，qq均可）。

**注意**：在使用mutt发送邮件之前，一定要保证你的邮箱开通了SMTP/POP3服务，允许使用第三方代理客户端！

# 安装mutt和msmtp

```sh
sudo apt-get install mutt
sudo apt-get install msmtp
```

# 配置mutt和msmtp

* 在～目录下新建.muttrc文件

```shell
#vim ~/.muttrc
set sendmail="/usr/bin/msmtp"	#使用msmtp发送邮件
set use_from=yes
set realname="QianyuGuo"		#发件人,可以任取     
set from=qygtmac@sina.com		#发件人邮箱
set envelope_from=yes
set rfc2047_parameters=yes
set charset="utf-8"
set send_charset="gb2312"
set send_charset="utf-8"
set send_charset="us-ascii:gbk:utf-8"
```

* 在～目录下新建.msmtprc文件和.msmtp.log文件

```shell
#vim ~/.msmtprc
#vim ~/.msmtp.log
account default
host smtp.sina.com
user qygtmac		#一定是邮箱@前面的部分,不能随便写)
from qygtmac@sina.com
password *****		#邮箱登录密码
auth login
tls off
logfile ~/.msmtp.log
```

配置.msmtprc的权限，只允许自己有读和写的权限，其他人没有任何权限

```shell
sudo chmod 600 ~/.msmtptc
```

# 发送邮件

往目标邮箱qianyuguo@tju.edu.cn发送邮件。

* 方式一

```shell
echo "邮件文本" | mutt -s "邮件主题(Subject)" qianyuguo@tju.edu.cn -a ~/tar_test.tar.gz(附件) 
```

* 方式二

邮件文本还可以从文件中读出。

```shell
vim text.txt	#在该文件中添加邮件的文本内容
mutt -s "邮件主题(Subject)" qianyuguo@tju.edu.cn -a ~/tar_test.tar.gz <text.txt
```

**注意**：

经测试，**邮件的附件**(-a 附件)部分只能**写在邮箱名后面**，写在前面任何位置都出错，原因不详。

如果是多个收件人，邮箱地址使用**空格**或**逗号**隔开。

# 参考博客

[Ubuntu14.04+mutt+msmtp配置linux下命令行邮件客户端](http://www.linuxdown.net/config/2016/0123/4466.html)

[Linux 定时自动备份MySQL与网站并发送邮件](http://huacnlee.com/blog/linux-auto-backup-mysql-and-website/)

[Ubuntu Mutt邮箱的配置与使用](http://www.linuxdiyf.com/linux/23690.html)

