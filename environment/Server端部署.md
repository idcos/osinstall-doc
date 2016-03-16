# Server端部署

## 下载

x86服务器安装下载链接如下：[http://www.idcos.com/X86/download.html](http://www.idcos.com/X86/download.html)

推荐使用编译好的二进制程序(包含UI、Server、BootOS、初始数据等)

程序目录结构如下：

```bash
idcos-osinstall
├── bootos
│   ├── initrd.img
│   └── vmlinuz
├── server
│   ├── idcos-osinstall.sql
│   └── osinstall-server-$version.x86_64.rpm
└── ui
    └── idcos-osinstall-ui.tar.gz
```

其中：

* bootos目录包含了bootos启动所需内核vmlinuz以及文件系统initrd.img
* server目录包含了数据库表结构idcos-osinstall.sql以及server安装包
* ui目录包含了ui的静态页面

## 初始化数据

* 我们使用的是开源的mysql数据库，需要先配置mysql并倒入表结构：

```bash
# yum install mysql-server
# service mysqld start
# chkconfig mysqld on
# mysql -uroot < /path/of/idcos-osinstall.sql
```

## 部署server

* 安装`osinstall-server`

```bash
# rpm -ivh /path/of/osinstall-server-$version.x86_64.rpm
```

* 修改配置文件`/etc/osinstall-server/osinstall-server.conf`，其中`$user`和`$password`是连接数据库的用户名和密码，请根据实际情况修改

```bash
# cat /etc/osinstall-server/osinstall-server.conf
{
  "repo": {
    "connection":"$user:$password@tcp(127.0.0.1:3306)/idcos-osinstall?charset=utf8&parseTime=True&loc=Local"
  },
  "osInstall":{
    "pxeConfigDir":"/var/lib/tftpboot/pxelinux.cfg"
   },
  "logger":{
      "logFile":"/var/log/osinstall-server.log",
      "level":"debug"
  },
  "rsa":{
    "publicKey":"/etc/osinstall-server/public.pem",
    "privateKey":"/etc/osinstall-server/private.pem"
  }
}
```

* 启动osinstall-server：

```bash
# service osinstall-server start
```

## 部署UI前端

* 解压 idcos-osinstall-ui.tar.gz 到web server目录

```bash
# mkdir /home/www
# tar zxpf /path/of/idcos-osinstall-ui.tar.gz -C /home/www
```

* 设置http根目录和api转发规则，以nginx为例，修改配置文件`/etc/nginx/conf.d/default.conf`如下：

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

其中：

* `root /home/www;` 参数指向http的根目录是`/home/www`
* `proxy_pass http://127.0.0.1:8083;` 将api请求转发到本机的`8083`端口，即`osinstall-server`监听的端口

部署完成后，访问地址：

[http://localhost/](http://localhost/)
