# Windows安装模板

这里我们适配了**`Windows Server 2008 R2 Enterprise`**以及**`Windows Server 2012 R2 Datacenter`**，安装Windows需要开启samba支持。

首先，下载我们提供的`winpe.iso`文件，这里假设http根目录为`/home/www`，文件存放路径是`/home/www/winpe/winpe.iso`

其次，安装samba服务，修改其配置文件`/etc/samba/smb.conf`如下：

```bash
# yum install samba
# cat /etc/samba/smb.conf
[global]
    workgroup = WORKGROUP
    server string = Samba Server Version %v
    log file = /var/log/samba/log.%m
    max log size = 50
    security = share
[image]
    path = /home/samba
    browseable = yes
    writable = yes
    read only = no
    guest only = yes
    create mask = 0644
    directory mask = 0755
```

再次，创建相关目录结构，导入镜像文件，这里以`Windows Server 2008 R2`简体中文版为例：

```bash
# mkdir -p /home/samba/windows/{2008r2_cn,2008r2_en,2012r2_cn,2012r2_en,drivers/{2008r2,2012r2},firstboot}
# mount -o loop cn_windows_server_2008_r2_standard_enterprise_datacenter_and_web_with_sp1_x64_dvd_617598.iso /media
# rsync -az /media/ /home/samba/windows/2008r2_cn/
# umount /media
```

说明：

* `2008r2_cn`目录为`Windows Server 2008 R2`简体中文版ISO安装镜像导出的文件
* `2008r2_en`目录为`Windows Server 2008 R2`英文版ISO安装镜像导出的文件
* `2012r2_cn`目录为`Windows Server 2012 R2`简体中文版ISO安装镜像导出的文件
* `2012r2_en`目录为`Windows Server 2012 R2`英文版ISO安装镜像导出的文件
* `drivers/2008r2`目录为`Windows Server 2008 R2`在安装过程中所需要的驱动文件。这里建议每个硬件型号的驱动单独一个目录，目录里面包含`driver.sys`和`driver.inf`文件
* `drivers/2012r2`目录为`Windows Server 2012 R2`在安装过程中所需要的驱动文件。这里建议每个硬件型号的驱动单独一个目录，目录里面包含`driver.sys`和`driver.inf`文件
* `firstboot`目录包含`winconfig.exe`程序。该程序为我们自己开发的系统配置工具，可以支持消息进度上报，磁盘分区，配置网络和主机名，配置注册表等。该程序支持hook脚本，只需要在`firstboot`目录下创建`preinstall.cmd`和`postinstall.cmd`批处理脚本并编写相应的命令即可。程序在运行前会执行`preinstall.cmd`脚本，程序在结束后会执行`postinstall.cmd`脚本，然后重启操作系统，完成整个安装过程

最后，在安装设备的时候选择操作系统`win2008r2-x86_64`，系统模板选择`win2008r2_cn`即可。

驱动程序目录结构如下：

```bash
# tree -L 2 /home/samba/windows/drivers/
/home/samba/windows/drivers/
├── 2008r2
│   ├── intel_i350
│   └── megaraid_sas
└── 2012r2
    ├── intel_i350
    └── megaraid_sas
```
