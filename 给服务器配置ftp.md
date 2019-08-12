1.注意CT OS 7.4防火墙用的是firewall,不要看iptable的防火墙了

2.注意编辑/etc/vsftpd/vsftpd.conf中的配置。

3.ftp出现

```
错误:    读取目录列表失败


问题解决：

FTP客户端默认的传输模式是被动模式，因此在通信过程中会去寻找服务器端的ip地址进行连接，
由于阿里云的外网ip不是直接配在网卡上，因此在被动模式下客户端找不到有效的ip

在 vsftpd.conf 加一句 pasv_address=X.X.X.X #服务器外网IP
这样就可以了 
```
