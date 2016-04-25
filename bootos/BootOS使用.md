# BootOS使用

搭建BootOS启动环境，需要配置tftp启动文件，内容如下：

```bash
# cat /var/lib/tftpboot/pxelinux.cfg/default
DEFAULT menu.c32
PROMPT 0
TIMEOUT 30

LABEL bootos
  MENU LABEL ^BootOS
  MENU DEFAULT
  KERNEL http://osinstall.idcos.com/bootos/vmlinuz
  APPEND initrd=http://osinstall.idcos.com/bootos/initrd.img console=tty0 selinux=0 biosdevname=0 SERVER_ADDR=http://osinstall.idcos.com
  IPAPPEND 2
```

参数说明：

* 设定参数```TIMEOUT 30```，网络启动以后默认等待3秒钟自动进入BootOS
* 使用http方式来加载```vmlinuz```和```initrd.img```，取代传统的tftp加载方式，大文件效率更高
* 增加```biosdevname=0```参数，关闭了centos 6下面网卡自动重命名的情况，使用ethX的命名规范
* 设定参数```SERVER_ADDR=http://osinstall.idcos.com```，指定server端的地址，agent会解析此参数并向server端发起http请求，请根据实际情况修改
* 设定```IPAPPEND 2```参数，一些服务器拥有多个网络接口，可能无法将BIOS所知的第一个网络接口设定为eth0，这将导致安装程序使用与PXE启动时不同的网络接口。增加此参数默认会使用PXE传递的网卡作为默认网络接口。

***提示：`SERVER_ADDR`和`IPAPPEND 2`为必选参数，如若没有添加，则会导致bootos启动失败***

## 开发者模式

BootOS提供一个配置参数，可以打开开发者模式。那么开发者模式和普通模式有什么区别呢，下面简单介绍一下。

* 普通模式：服务器进入BootOS以后，agent自动启动，收集服务器产品型号（如Dell PowerEdge R420）并提交给Server和硬件配置数据库进行比对，如果硬件配置数据库并没有这个型号的硬件配置，那么agent不会执行硬件配置，会返回错误信息。
* 开发者模式：在开发者模式中，同样服务器进入BootOS以后，agent自动启动，收集服务器产品型号（如Dell PowerEdge R420）但不会和Server端硬件配置数据库进行比对，直接执行硬件配置，并返回结果。

开发者模式的意义在于什么？目前有些硬件型号的服务器不在硬件配置数据库，用户咨询是否可以支持其硬件配置。因为主流的Raid，OOB的配置基本是通用的，所以打开开发者模式以后，硬件配置脚本会自动检测该型号的硬件是否能支持，如果支持则会进行配置，请用户谨慎选择。

如何打开开发者模式？修改PXE default配置如下，增加```DEVELOPER=1```参数即可。

```bash
# cat /var/lib/tftpboot/pxelinux.cfg/default
DEFAULT menu.c32
PROMPT 0
TIMEOUT 30

LABEL bootos
  MENU LABEL ^BootOS
  MENU DEFAULT
  KERNEL http://osinstall.idcos.com/bootos/vmlinuz
  APPEND initrd=http://osinstall.idcos.com/bootos/initrd.img console=tty0 selinux=0 biosdevname=0 SERVER_ADDR=http://osinstall.idcos.com DEVELOPER=1
  IPAPPEND 2
```
