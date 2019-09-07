## [用户和用户组的相关操作](https://blog.csdn.net/yajie_china/article/details/80745346)

## PHP总的配置文件
```bash
$ cat /usr/bin/php-config
```

## 查看端口进程
```bash
netstat命令各个参数说明如下：
-t : 指明显示TCP端口；
-u : 指明显示UDP端口；
-l : 仅显示监听套接字(所谓套接字就是使应用程序能够读写与收发通讯协议(protocol)与资料的程序)；
-p : 显示进程标识符和程序名称，每一个套接字/端口都属于一个程序；
-n : 不进行DNS轮询，显示IP(可以加速操作)即可显示当前服务器上所有端口及进程服务，于grep结合可查看某个具体端口及服务情况；
netstat -ntlp   //查看当前所有tcp端口；
netstat -ntulp |grep 80   //查看所有80端口使用情况；
netstat -an | grep 3306   //查看所有3306端口使用情况。
```

## 查看和卸载软件
[apt和apt-get的相关命令](https://blog.csdn.net/taotongning/article/details/82320472)
```bash
# 查看
$ dpkg -l|grep name
# dpkg 卸载
$ sudo dpkg -r 软件包名  卸载相应软件
# apt 卸载
$ apt-get remove 软件1 软件2来卸载
```
[彻底卸载的方法](https://www.jb51.net/article/144572.htm)

## Ubuntu18.04 安装MySQL
[参考地址](https://www.cnblogs.com/williamjie/p/11126486.html)
环境信息：   
OS：Ubuntu18.04   
```bash
$ sudo apt-get install mysql-server mysql-client
```

## 乌班图服务器中查看新装入mysql的账号与密码
```bash
$ sudo cat /etc/mysql/debian.cnf
```
**显示内容如下**
```bash
[sudo] password for ubuntu: 
# Automatically generated for Debian scripts. DO NOT TOUCH!
[client]
host     = localhost
user     = debian-sys-maint
password = HPieU0hVrcxFm5Y4
socket   = /var/run/mysqld/mysqld.sock
[mysql_upgrade]
host     = localhost
user     = debian-sys-maint
password = HPieU0hVrcxFm5Y4
socket   = /var/run/mysqld/mysqld.sock
```
其中mysql的账号和密码为user和password

## Redis服务器的启动和停止
[参考地址](https://baijiahao.baidu.com/s?id=1552330515936646&wfr=spider&for=pc)
Redis内置的配置进行启动命令：
```bash
$ redis-server &
```
Redis内置的配置进行停止命令：
```bash
$ redis-cli
$ 127.0.0.1:6379> shutdown
$ not connected>
```

## 允许root用户登录ssh
新安装的Ubuntu 16.04系统中ssh是不允许root用户登录的   
**重置管理员密码**
```bash
$ sudo password root
```
**切换为超级管理员**
```bash
$ sudo su
```
**编辑ssh的配置文件**
```bash
$ vim /etc/ssh/sshd_config
```
通过vim编辑器搜索关键字找到**PermitRootLogin prohibit-password**,将其屏蔽并在下面一行加入PermitRootLogin yes   
vim中修改显示如下
```bash
···
···
···
# Authentication:

LoginGraceTime 2m
#PermitRootLogin prohibit-password
PermitRootLogin yes
StrictModes yes
#MaxAuthTries 6
#MaxSessions 10
···
···
···
```
保存退出vim，重启ssh
```bash
$ service ssh restart
```
可直接通过xshell登录root账号了

## 乌班图安装多版本php
[安装多版本教程1?](https://www.cnblogs.com/wtgg/p/9767129.html)
[安装多版本教程2?](https://www.jb51.net/article/145899.htm)   
[安装多php版本出现的问题](https://segmentfault.com/a/1190000014160639)   
[apt-get相关命令](https://www.cnblogs.com/downey-blog/p/10473893.html)
```bash
$ vim /etc/nginx/sites-enabled/`需要修改项目的php版本`

location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php5.6-fpm.sock; # 请注意核对 PHP 版本
        fastcgi_index index.php;
       
重启服务器 $ reboot
```

## 查找php拓展和安装
```bash
$ apt-cache search php7.2

#常见模块
#php7.0-mysql php7.0-curl php7.0-gd php7.0-intl php-pear php7.0-imagick php7.0-imap php7.0-mcrypt php7.0-memcache php7.0-ming php7.0-ps php7.0-pspell php7.0-recode php7.0-snmp php7.0-sqlite php7.0-tidy php7.0-xmlrpc php7.0-xsl

#以下为必装模块：
#php7.0-cli，linux下cron定时执行程序
#php7.0-mysql，PHP对mysql的支持
#php7.0-gd，验证码、缩略图、裁剪必备
#php7.0-mcrypt，加密用的
#php7.0-curl，发送远程get／post请求

···
php-radius - radius client library for PHP
php-raphf - raphf module for PHP
php-redis - PHP extension for interfacing with Redis
php-rrd - PHP bindings to rrd tool system
php-sass - PHP bindings to libsass - fast, native Sass parsing in PHP
php-smbclient - PHP wrapper for libsmbclient
php-solr - PHP extension for communicating with Apache Solr server
php-ssh2 - Bindings for the libssh2 library
php-stomp - Streaming Text Oriented Messaging Protocol (STOMP) client module for PHP
php-uploadprogress - file upload progress tracking extension for PHP
php-uuid - PHP UUID extension
php-yac - YAC (Yet Another Cache) for PHP
php-yaml - YAML-1.1 parser and emitter for PHP
php-zmq - ZeroMQ messaging bindings for PHP
libapache2-mod-php5.6 - server-side, HTML-embedded scripting language (Apache 2 module)
libphp5.6-embed - HTML-embedded scripting language (Embedded SAPI library)
php-lua - PHP Embedded lua interpreter
···
$ apt-get install `复制上面需要的拓展,例如:php-rrd` `复制上面需要的第二个拓展` `依次类推`

#重启服务
$ service nginx restart
$ service php7.0-fpm restart
```
## 打包和解压缩命令
```bash
$ tar zxvf FileName.tar.tgz                # 解压
$ tar zcvf FileName.tar.tgz FileName       # 压缩
```

## ubuntu中安装vsftp
```bash
# 1、安装vsftpd
$ sudo apt install vsftpd
# 2、相关命令
$ sudo service vsftpd start    #启动vsftpd
$ sudo service vsftpd restart  #重启
$ sudo service vsftpd stop     #关闭
$ sudo service vsftpd status   #查看状态
$ sudo systemctl start vsftpd  #可忽略
$ sudo systemctl enable vsftpd #可忽略
# 3、执行
$ /lib/systemd/systemd-sysv-install enable vsftp #可忽略
# 4、服务器安全组添加21端口、查看防火墙是否开启、配置文件中打开listen=YES，关闭listen_ivp6=NO
# 5、新建目录/home/uftp作为用户主目录
$ sudo mkdir /home/uftp
# 6.1、新建用户uftp，强定用户主目录和所用shell，并设置密码
$ sudo useradd -d /home/uftp -s /bin/bash uftp
$ sudo passwd uftp
# 6.2、将目录/home/ftp的所属者和所属组都改为uftp:
$ sudo chown uftp(所属者):uftp(所属组) /home/uftp
# 6.3、新建文件/etc/vsftpd.user_list，用于存放允许访问ftp的用户：
$ sudo vim /etc/vsftpd.user_list
# 6.4、添加uftp，保存退出
uftp
~
~
# 6.5 编辑vsftpd配置文件
$ sudo vim /etc/vsftpd.conf
--------------------------------------------------------------------------------------------------------------------------------------
# Example config file /etc/vsftpd.conf
#
# The default compiled in settings are fairly paranoid. This sample file
# loosens things up a bit, to make the ftp daemon more usable.
# Please see vsftpd.conf.5 for all compiled in defaults.
#
# READ THIS: This example file is NOT an exhaustive list of vsftpd options.
# Please read the vsftpd.conf.5 manual page to get a full idea of vsftpd's
# capabilities.
#
#
# Run standalone?  vsftpd can run either from an inetd or as a standalone
# daemon started from an initscript.
listen=YES
#
# This directive enables listening on IPv6 sockets. By default, listening
# on the IPv6 "any" address (::) will accept connections from both IPv6
# and IPv4 clients. It is not necessary to listen on *both* IPv4 and IPv6
# sockets. If you want that (perhaps because you want to listen on specific
# addresses) then you must run two copies of vsftpd with two configuration
# files.
listen_ipv6=NO
#
# Allow anonymous FTP? (Disabled by default).
# anonymous_enable=YES
#
# Uncomment this to allow local users to log in.
local_enable=YES
#
# Uncomment this to enable any form of FTP write command.
write_enable=YES
userlist_file=/etc/vsftpd.user_list
userlist_enable=YES
userlist_deny=NO
#
# Default umask for local users is 077. You may wish to change this to 022,
# 默认是077，公共权限不足可以使用022
# umask = 022 时，新建的目录 权限是755，文件的权限是 644
# umask = 077 时，新建的目录 权限是700，文件的权限时 600
# if your users expect that (022 is used by most other ftpd's)
local_umask=022
#
# Uncomment this to allow the anonymous FTP user to upload files. This only
# has an effect if the above global write enable is activated. Also, you will
# obviously need to create a directory writable by the FTP user.
#anon_upload_enable=YES
#
# Uncomment this if you want the anonymous FTP user to be able to create
# new directories.
#anon_mkdir_write_enable=YES
#
# Activate directory messages - messages given to remote users when they
# go into a certain directory.
dirmessage_enable=YES
#
# If enabled, vsftpd will display directory listings with the time
# in  your  local  time  zone.  The default is to display GMT. The
# times returned by the MDTM FTP command are also affected by this
# option.
use_localtime=YES
#
# Activate logging of uploads/downloads.
xferlog_enable=YES
#
# Make sure PORT transfer connections originate from port 20 (ftp-data).
connect_from_port_20=YES
#
# If you want, you can arrange for uploaded anonymous files to be owned by
# a different user. Note! Using "root" for uploaded files is not
# recommended!
#chown_uploads=YES
#chown_username=whoever
#
# You may override where the log file goes if you like. The default is shown
# below.
#xferlog_file=/var/log/vsftpd.log
#
# If you want, you can have your log file in standard ftpd xferlog format.
# Note that the default log file location is /var/log/xferlog in this case.
#xferlog_std_format=YES
#
# You may change the default value for timing out an idle session.
#idle_session_timeout=600
#
# You may change the default value for timing out a data connection.
#data_connection_timeout=120
#
# It is recommended that you define on your system a unique user which the
# ftp server can use as a totally isolated and unprivileged user.
#nopriv_user=ftpsecure
#
# Enable this and the server will recognise asynchronous ABOR requests. Not
# recommended for security (the code is non-trivial). Not enabling it,
# however, may confuse older FTP clients.
#async_abor_enable=YES
#
# By default the server will pretend to allow ASCII mode but in fact ignore
# the request. Turn on the below options to have the server actually do ASCII
# mangling on files when in ASCII mode.
# Beware that on some FTP servers, ASCII support allows a denial of service
# attack (DoS) via the command "SIZE /big/file" in ASCII mode. vsftpd
# predicted this attack and has always been safe, reporting the size of the
# raw file.
# ASCII mangling is a horrible feature of the protocol.
#ascii_upload_enable=YES
#ascii_download_enable=YES
#
# You may fully customise the login banner string:
#ftpd_banner=Welcome to blah FTP service.
#
# You may specify a file of disallowed anonymous e-mail addresses. Apparently
# useful for combatting certain DoS attacks.
#deny_email_enable=YES
# (default follows)
#banned_email_file=/etc/vsftpd.banned_emails
#
# You may restrict local users to their home directories.  See the FAQ for
# the possible risks in this before using chroot_local_user or
# chroot_list_enable below.
#chroot_local_user=YES
#
# You may specify an explicit list of local users to chroot() to their home
# directory. If chroot_local_user is YES, then this list becomes a list of
# users to NOT chroot().
# (Warning! chroot'ing can be very dangerous. If using chroot, make sure that
# the user does not have write access to the top level directory within the
# chroot)
#chroot_local_user=YES
#chroot_list_enable=YES
# (default follows)
#chroot_list_file=/etc/vsftpd.chroot_list
#
# You may activate the "-R" option to the builtin ls. This is disabled by
# default to avoid remote users being able to cause excessive I/O on large
# sites. However, some broken FTP clients such as "ncftp" and "mirror" assume
# the presence of the "-R" option, so there is a strong case for enabling it.
#ls_recurse_enable=YES
#
# Customization
#
# Some of vsftpd's settings don't fit the filesystem layout by
# default.
#
# This option should be the name of a directory which is empty.  Also, the
# directory should not be writable by the ftp user. This directory is used
# as a secure chroot() jail at times vsftpd does not require filesystem
# access.
secure_chroot_dir=/var/run/vsftpd/empty
#
# This string is the name of the PAM service vsftpd will use.
pam_service_name=vsftpd
#
# This option specifies the location of the RSA certificate to use for SSL
# encrypted connections.
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
ssl_enable=NO

#
# Uncomment this to indicate that vsftpd use a utf8 filesystem.
#utf8_filesystem=YES
--------------------------------------------------------------------------------------------------------------------------------------

# 6.6、添加vsftpd.user_list文件
$ touch /etc/vsftpd.user_list
uftp
~
~

# 7、cmd中测试
> ftp [服务器ip]
C:\Users\LL>ftp 'ip地址'
连接到 '显示ip地址'。
220 (vsFTPd 3.0.3)
200 Always in UTF8 mode.
用户('ip地址':(none)):输入服务器中创建的账号和密码

# 查看所在远程服务器的路径
> ftp> pwd
# 查看本地的路径
> ftp> lcd
# 下载文件
> ftp> get [文件名]
# 上传文件
> ftp> put [文件名]

# 8、卸载vsftpd
$ apt remove --purge vsftpd

# 9、添加用户到vsftpd中
$ vim /etc/vsftpd.user_list #中加入用户名，如果是root，还需要把/etc/vsftpduser中的root删除
```
