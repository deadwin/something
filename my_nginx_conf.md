nginx_conf目录在 /etc/nginx 下。
nginx 位于/usr/sbin目录。
示例如下：
#HTTPS server

    server {

        listen                     443 ssl;
        server_name                这里是你的域名www.abc.com;

        ssl_certificate            /xxx/xxx/xxx.pem;
        ssl_certificate_key        /xxx/xxx.key;

        ssl_session_cache          shared:SSL:1m;
        ssl_session_timeout        5m;
        ssl_ciphers                xxx;
        ssl_protocols              TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers  on;

        location / {
            proxy_pass http://127.0.0.1:xxx;
                root   html;
                index  index.html index.htm;
        }
    }


配置完成,校验文件，重启nginx，并开启防火墙443端口后，浏览器即可以https访问网站！

校验：nginx -t./ng 

执行以下命令重启Nginx服务器。

nginx -s stop
nginx -s start


参考：https://help.aliyun.com/document_detail/98728.html?spm=a2c4g.11186623.2.12.20b8625aUx5IgH#concept-n45-21x-yfb


如果要将http强制定下到https，参考如下：注意防火墙80端口得开着

server {
 listen 80;
 server_name localhost;   #将localhost修改为您证书绑定的域名，例如：www.example.com。
rewrite ^(.*)$ https://$host$1 permanent;   #将所有http请求通过rewrite重定向到https。
 location / {
index index.html index.htm;
}
}







