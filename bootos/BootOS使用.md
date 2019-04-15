# BootOS使用

搭建BootOS启动环境，需要配置tftp启动文件，内容如下：

```bash
# cat /opt/cloudboot/var/lib/tftpboot/pxelinux.cfg/default
DEFAULT bootos
PROMPT 0
TIMEOUT 30

LABEL bootos
  MENU LABEL ^BootOS
  MENU DEFAULT
  KERNEL http://osinstall.idcos.com/bootos/bootos.img audit=0 selinux=0 biosdevname=0 net.ifnames=0 rd.retry=1 SERVER_ADDR=http://osinstall.idcos.com DEVELOPER=1 PRE=http://osinstall.idcos.com/pre.sh
  IPAPPEND 2
```

参数说明：

* 设定参数```TIMEOUT 30```，网络启动以后默认等待3秒钟自动进入BootOS
* 使用http方式来加载```bootos.img```，取代传统的tftp加载方式，大文件效率更高
* 增加```biosdevname=0```参数，关闭了centos 6下面网卡自动重命名的情况，使用ethX的命名规范
* 设定参数```SERVER_ADDR=http://osinstall.idcos.com```，指定server端的地址，agent会解析此参数并向server端发起http请求，请根据实际情况修改
* 设定```IPAPPEND 2```参数，一些服务器拥有多个网络接口，可能无法将BIOS所知的第一个网络接口设定为eth0，这将导致安装程序使用与PXE启动时不同的网络接口。增加此参数默认会使用PXE传递的网卡作为默认网络接口。

***提示：`SERVER_ADDR`和`IPAPPEND 2`为必选参数，如若没有添加，则会导致bootos启动失败***

## 高级选项

BootOS内置agent，并自动启动，负责硬件信息的采集和硬件初始化配置。这里提供了两个接口，可以方便调用用户自己的脚本，做一些更复杂的操作。

```bash
# cat /opt/cloudboot/var/lib/tftpboot/pxelinux.cfg/default
DEFAULT bootos
PROMPT 0
TIMEOUT 30

LABEL bootos
  MENU LABEL ^BootOS
  MENU DEFAULT
  KERNEL http://osinstall.idcos.com/bootos/bootos.img audit=0 selinux=0 biosdevname=0 net.ifnames=0 rd.retry=1 SERVER_ADDR=http://osinstall.idcos.com DEVELOPER=1 PRE=http://osinstall.idcos.com/pre.sh POST=http://osinstall.idcos.com/post.py
  IPAPPEND 2
```

参数说明：

* 设定参数```PRE=http://osinstall.idcos.com/pre.sh```，agent会在启动以后首先从指定URL获取程序并执行，程序可以是脚本也可以是二进制文件
* 设定参数```POST=http://osinstall.idcos.com/post.py```，agent会在重启系统之前从指定URL获取程序并执行，程序可以是脚本也可以是二进制文件

用户可以通过调用POST接口执行一些个性化的配置，例如个性化Raid配置，采集更多的系统信息等。
