# Server端部署

## 初始化数据

* 我们使用的是开源的mysql数据库，需要先配置mysql并倒入表结构：

```bash
# yum install mysql-server
# service mysqld start
# chkconfig mysqld on
# mysql -uroot < idcos-osinstall.sql
```

## 部署server

* 修改配置文件idcos-os-install.json，配置数据库连接：

```json
"repo": {
    "connection": "用户名:密码@tcp(localhost:3306)/idcos-osinstall?charset=utf8&parseTime=True&loc=Local"
},
```

* 修改配置文件idcos-os-install.json，设置PXE配置文件目录：

```json
"osInstall":{
    "pxeConfigDir":"/var/lib/tftpboot/pxelinux.cfg"
}
```

* 运行可执行文件，执行文件会监听8083端口：

```bash
# chmod 755 os-install-server
# nohup ./os-install-server &>os-install-server.log &
```

## 部署UI前端

1. 解压 idcos-osinstall-ui.tar.gz 到web server目录

```bash
# mkdir /home/www
# tar zxpf idcos-osinstall-ui.tar.gz -C /home/www
```

2. 设置虚拟目录规则，以nginx为例：

```nginx
server {
    listen       80 default_server;
    server_name  _;

    include /etc/nginx/default.d/*.conf;

    location / {
        root   /home/www;
        index  index.html index.htm;
    }

    location /api/ {
        proxy_pass http://127.0.0.1:8083;
    }

    error_page  404              /404.html;
    location = /404.html {
        root   /usr/share/nginx/html;
    }

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```

部署完成后，访问地址：

[http://localhost/](http://localhost/)
