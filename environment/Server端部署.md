# Server端部署

## 初始化数据

* 数据库：mysql
* 编码：utf8
* 执行步骤：使用命令行或者客户端工具将idcos-osinstall.sql导入，会自动生成idcos-osinstall数据库（注意设定utf8编码)

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
chmod 755 os-install-server
nohup ./os-install-server &>os-install-server.log &
```

## 部署UI前端

1. 解压 idcos-osinstall-ui.tar.gz 到web server目录
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
        proxy_pass http://localhost:8083;
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

[http://localhost/#/dashboard/main](http://localhost/#/dashboard/main)