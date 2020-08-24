安装教程参考地址：https://www.ytyzx.org/index.php/%E5%A6%82%E4%BD%95%E5%9C%A8CentOS7%E4%B8%AD%E5%AE%89%E8%A3%85MySQL
步骤1：
```wget https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm```
步骤2：
5.下载完毕后输入“md5sum mysql57-community-release-el7-9.noarch.rpm”生成MD5值并确保同官方网站上的MD5值（参考第3步）相同。
   注意：建议运行此命令以确保文件无损坏。




6.确认MD5无误后输入“rpm -ivh mysql57-community-release-el7-9.noarch.rpm”并按回车键进行安装YUM源RPM安装包。


7.输入“yum install mysql-server”并按回车键确定即可开始安装。
   注意：因上一步已添加新的YUM存储库，故可直接安装


8.输入“y”开始下载并安装MySQL。


9.提示是否接受GPG密钥，输入“y”即可继续安装。

10.提示已经安装完毕。



11.输入“systemctl start mysqld”即可启动MySQL服务。

12.输入“systemctl status mysqld”即可查看当前MySQL服务状态。

13.由于MySQL默认开机自动启动，如需取消开机自动启动则输入“systemctl disable mysqld”。

14.输入“systemctl enable mysqld”则可设置为开机自动启动MySQL服务。


15.输入“grep 'temporary password' /var/log/mysqld.log”则可查看MySQL root用户临时密码。
     注意：此密码仅供第一次登陆MySQL使用，登录后必须修改。


16.在使用YUM安装时提示“Warning: RPMDB altered outside of yum.”。


17.故障原因为直接使用rpm安装时有可能导致此问题。



18.输入“yum history sync”同步即可排除此故障。
==================================================
然后

whereis mysql

可以看到MySQL 的安装目录是 /usr/bin/

 

启动服务

systemctl start mysqld

systemctl enable mysqld

systemctl status mysqld

 

查找初始密码

cat /var/log/mysqld.log | grep password

这里可以看到初始密码

 

进入mysql

mysql -uroot -p

 

修改初始密码

mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY '你的密码';

 

设置允许远程连接（新版MySQL的方式跟之前的不大一样）
复制代码

mysql> use mysql;

mysql> select host,user,authentication_string,plugin from user;

mysql> update user set host='%' where user='root';

mysql> flush privileges;

复制代码

 

查看字符编码

mysql> status

如果是【utf8mb4】那就不用改了

======================
修改mysql临时密码报错提示过于简单：
```mysql> set global validate_password_policy=0;
Query OK, 0 rows affected (0.00 sec)
```
