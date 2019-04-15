# VMware安装模板

这里以VMware ESXi 6.0系统为例，简单介绍一下kickstart的使用方法。

首先，需要下载VMware ESXi 6.0的iso镜像，然后导入镜像文件内容：

```bash
# mount -o loop VMware-VMvisor-Installer-6.0.0.update01-3029758.x86_64.iso /media/
# mkdir -p /opt/cloudboot/home/www/esxi/6.0u1/
# rsync -az /media/ /opt/cloudboot/home/www/esxi/6.0u1/
# umount /media
```

由于我们要使用http方式加载模块，所以需要修改boot.cfg文件，原始内容如下：

```bash
# cat /opt/cloudboot/home/www/esxi/6.0u1/boot.cfg
bootstate=0
title=Loading ESXi installer
timeout=5
kernel=/tboot.b00
kernelopt=runweasel
modules=XXX
build=
updated=0
```

使用sed命令批量替换修改boot.cfg文件：

```bash
# sed -i.orig -e 's;/;http://osinstall.idcos.com/esxi/6.0u1/;g' -e '/kernelopt/d' /opt/cloudboot/home/www/esxi/6.0u1/boot.cfg
```

最后，在安装设备的时候，PXE模板选择`esxi6.0u1-x86_64`，系统模板选择`esxi6.0`即可。
