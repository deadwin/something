使用forever:


forever start app.js

forever stop app.js



******************************
NodeJS运行时抛出: Error: listen EADDRINUSE ::5000:
原因：端口号 3000 已被占用
解决步骤：1.  netstat -lntp  查找系统所示正在使用的端口列表
	  2.kill -9 占用端口3000的进程ID号
	  3.如2无效，则可能是父进程导致的，需要kill父进程，或者干脆重启


****************************************
1.安装防火墙

   安装iptables-services ：

 

2.防火墙基本操作

 

   查看版本： firewall-cmd --version

 

   显示状态： firewall-cmd --state

 

　查看所有打开的端口： netstat -anp

 

   开启防火墙 systemctl start firewalld

 

　关闭防火墙 systemctl stop firewalld

 

    开启防火墙 service firewalld start
    若遇到无法开启
    先用：systemctl unmask firewalld.service
    然后：systemctl start firewalld.service

 

3.端口查询

 

    查询指定端口是否已开 firewall-cmd --query-port=666/tcp

 

    提示yes or no

 

    查询所有开启的端口 netstat -anp

4.开启端口

   如果上面端口查询没有开启的话，需要重新开启一下

   开启端口命令  

 

    添加  firewall-cmd --zone=public --add-port=80/tcp --permanent    （--permanent永久生效，没有此参数重启后失效）
    重新载入  firewall-cmd --reload
    查看    firewall-cmd --zone= public --query-port=80/tcp
    删除    firewall-cmd --zone= public --remove-port=80/tcp --permanent




*****************************************************************
手动搭建FTP站点（CentOS 7）
参考：https://help.aliyun.com/document_detail/92048.html?spm=a2c4g.11186623.6.1122.36627bfesFpCEY#section-821-887-8np
