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
