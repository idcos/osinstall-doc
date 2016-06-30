# XenServer安装模板

这里以XenServer 6.5系统为例，简单介绍一下kickstart的使用方法。

首先，需要下载XenServer 6.5的iso镜像，然后导入镜像文件内容：

```bash
# mount -o loop XenServer-6.5.0-xenserver.org-install-cd.iso /media/
# rsync -az /media/ /opt/cloudboot/home/www/xenserver/6.5/
```

最后，在安装设备的时候，PXE模板选择`xenserver6.5-x86_64`，系统模板选择`xenserver6.5`即可。
