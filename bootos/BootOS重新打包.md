# BootOS重新打包

## 解压BootOS

```bash
# mkdir bootos
# cd bootos
# wget -O - http://osinstall.idcos.net/bootos/initrd.img | xz -d | cpio -id
```

## 安装最新的igb驱动包

```bash
# cp /path/of/igb-5.3.2-1.x86_64.rpm .
# chroot $PWD ‘rpm -Uvh igb-5.3.2-1.x86_64.rpm’
Preparing...                ########################################### [100%]
   1:igb                    ########################################### [100%]
original pci.ids saved in /usr/local/share/igb
```

## 重新打包BootOS

```bash
# find . | cpio -co | xz -9 --format=lzma > /path/of/initrd.img
```

## 测试最新的驱动

```bash
# modinfo igb | head
filename:       /lib/modules/2.6.32-573.el6.x86_64/kernel/drivers/net/igb/igb.ko
version:        5.3.2
license:        GPL
description:    Intel(R) Gigabit Ethernet Network Driver
author:         Intel Corporation, <e1000-devel@lists.sourceforge.net>
srcversion:     B821C1F6B2F95B48EC6DFDA
alias:          pci:v00008086d000010D6sv*sd*bc*sc*i*
alias:          pci:v00008086d000010A9sv*sd*bc*sc*i*
alias:          pci:v00008086d000010A7sv*sd*bc*sc*i*
alias:          pci:v00008086d000010E8sv*sd*bc*sc*i*
```