# Windows安装模板

这里我们适配了**`Windows Server 2008 R2 Enterprise`**以及**`Windows Server 2012 R2 Datacenter`**，同理其他 Windows 版本也适用，安装 Windows 需要开启 samba 支持。

导入镜像文件，这里以`Windows Server 2008 R2`简体中文版为例：

```bash
# mount -o loop cn_windows_server_2008_r2_standard_enterprise_datacenter_and_web_with_sp1_x64_dvd_617598.iso /media
# rsync -az /media/ /home/samba/windows/2008r2/
# umount /media
```

说明：

* `/home/samba/windows/2008r2`目录为`Windows Server 2008 R2`ISO安装镜像导出的文件
* `/home/samba/windows/drivers/2008r2`目录为`Windows Server 2008 R2`在安装过程中所需要的驱动文件。这里建议每个硬件型号的驱动单独一个目录，目录里面包含`driver.sys`和`driver.inf`文件
* `/home/samba/windows/firstboot`目录包含`winconfig.exe`程序。该程序为我们自己开发的系统配置工具，可以支持消息进度上报，磁盘分区，配置网络和主机名，配置注册表等。该程序支持hook脚本，只需要在`firstboot`目录下创建`preinstall.cmd`和`postinstall.cmd`批处理脚本并编写相应的命令即可。程序在运行前会执行`preinstall.cmd`脚本，程序在结束后会执行`postinstall.cmd`脚本，然后重启操作系统，完成整个安装过程

最后，在安装设备的时候选择操作系统`win2008r2-x86_64`，系统模板选择`win2008r2`即可。安装完成以后，默认Administrator用户的密码是```yunjikeji```

驱动程序目录结构如下：

```bash
/home/samba/windows/drivers/
|-- 2008r2
|   |-- broadcom
|   |-- intel_10gb
|   |-- intel_40gb
|   |-- intel_pro100
|   |-- intel_pro1000
|   |-- kvm
|   |-- lsi_sas2
|   |-- lsi_sas3
|   |-- megasas2
|   |-- megasr1
|   `-- percsas3
`-- 2012r2
    |-- broadcom
    |-- intel_10gb
    |-- intel_40gb
    |-- intel_pro100
    |-- intel_pro1000
    |-- kvm
    |-- lsi_sas2
    |-- lsi_sas3
    |-- megasas2
    |-- megasr1
    `-- percsas3
```


