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

```
set sendmail="/usr/bin/msmtp"
set use_from=yes
set realname="QianyuGuo"
set from=qygtmac@sina.com
set envelope_from=yes
set rfc2047_parameters=yes
set charset="utf-8"
set send_charset="gb2312"
set send_charset="utf-8"
set send_charset="us-ascii:gbk:utf-8"
```

* 在～目录下新建.msmtprc文件和.msmtp.log文件

```
account default
host smtp.sina.com
user qygtmac (一定是邮箱@前面的部分)
from qygtmac@sina.com
password *****(邮箱登录密码)
auth login
tls off
logfile ~/.msmtp.log
```

# 发送邮件

往目标邮箱qianyuguo@tju.edu.cn发送邮件

* 方式一

```shell
echo "邮件文本" | mutt -s "邮件主题(Subject)" qianyuguo@tju.edu.cn -a ~/tar_test.tar.gz(附件) 
```

* 方式二

邮件文本还可以从文件中读出

```shell
vim text.txt
mutt -s "邮件主题(Subject)" qianyuguo@tju.edu.cn -a ~/tar_test.tar.gz <text.txt
```

