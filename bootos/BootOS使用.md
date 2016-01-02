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
  KERNEL http://osinstall.idcos.net/bootos/vmlinuz
  APPEND initrd=http://osinstall.idcos.net/bootos/initrd.img console=tty0 selinux=0 biosdevname=0 SERVER_ADDR=http://osinstall.idcos.net
  IPAPPEND 2
```

参数说明：

* 设定参数```TIMEOUT 30```，网络启动以后默认等待3秒钟自动进入BootOS
* 使用http方式来加载```vmlinuz```和```initrd.img```，取代传统的tftp加载方式，大文件效率更高
* 增加```biosdevname=0```参数，关闭了centos 6下面网卡自动重命名的情况，使用ethX的命名规范
* 设定参数```SERVER_ADDR=http://osinstall.idcos.net```，指定server端的地址，agent会解析此参数并向server端发起请求，请根据实际情况修改
* 设定```IPAPPEND 2```参数，一​些​服​务​器​拥​有​多​个​网​络​接​口​，可​能​无​法​将​BIOS所​知​的​第​一​个​网​络​接​口​设​定​为​eth0，这​将​导​致​安​装​程​序​使​用​与​PXE启​动​时​不​同​的​网​络​接​口​。增加此参数默认会使用PXE传递的网卡作为默认网络接口。