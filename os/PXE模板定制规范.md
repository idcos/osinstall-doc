# PXE模板定制规范

系统安装所需的配置模板包括pxe安装模板和自动化部署模板，并且包含了一套初始化脚本。这里以CentOS 6为例，介绍一下kickstart的定制规范。

## pxe安装模板

```bash
DEFAULT centos6.7
LABEL centos6.7
KERNEL http://osinstall.idcos.com/centos/6.7/os/x86_64/images/pxeboot/vmlinuz
APPEND initrd=http://osinstall.idcos.com/centos/6.7/os/x86_64/images/pxeboot/initrd.img ksdevice=bootif ks=http://osinstall.idcos.com/api/osinstall/v1/device/getSystemBySn?sn={sn} console=tty0 selinux=0 biosdevname=0
IPAPPEND 2
```

说明：

* 使用```ksdevice=bootif```参数来指定pxe传递的网卡，配合```IPAPPEND 2```参数来使用
* 指定kickstart模板获取地址，使用api接口进行获取，server平台在生成pxe安装文件的同时会自动替换```{sn}```变量为本机序列号，在编写pxe安装模板的时候需要特别注意此用法
