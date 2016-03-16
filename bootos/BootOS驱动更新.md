# BootOS驱动更新

> 普通用户如果没有特殊的需求不需要定制BootOS，可以省略接下来的BootOS驱动更新和打包。

BootOS是由标准的CentOS定制而成，所以非常容易定制。这里我们提供的BootOS是基于CentOS 6.7的系统，支持的网络驱动如下：

```bash
# ls /lib/modules/`uname -r`/kernel/drivers/net/
3c59x.ko     b44.ko      cnic.ko   e100.ko       ifb.ko      macvtap.ko     netxen          ppp_generic.ko  r6040.ko    slhc.ko        tg3.ko           virtio_net.ko
8139cp.ko    benet       cxgb3     enic          igb         mdio.ko        niu.ko          ppp_mppe.ko     r8169.ko    slip.ko        tlan.ko          vmxnet3
8139too.ko   bna         cxgb4     epic100.ko    igbvf       mii.ko         ns83820.ko      pppoe.ko        s2io.ko     smsc9420.ko    tulip            vxge
8390.ko      bnx2.ko     cxgb4vf   ethoc.ko      ipg.ko      mlx4           pch_gbe         pppol2tp.ko     sc92031.ko  starfire.ko    tun.ko           vxlan.ko
acenic.ko    bnx2x       dl2k.ko   fealnx.ko     ixgb        mlx5           pcmcia          pppox.ko        sfc         sundance.ko    typhoon.ko       wan
amd8111e.ko  bonding     dnet.ko   forcedeth.ko  ixgbe       myri10ge       pcnet32.ko      ppp_synctty.ko  sis190.ko   sungem.ko      usb              wimax
atl1c        can         dummy.ko  hyperv        ixgbevf     natsemi.ko     phy             qla3xxx.ko      sis900.ko   sungem_phy.ko  veth.ko          wireless
atl1e        cassini.ko  e1000     i40e          jme.ko      ne2k-pci.ko    ppp_async.ko    qlcnic          skge.ko     sunhme.ko      via-rhine.ko     xen-netfront.ko
atlx         chelsio     e1000e    i40evf        macvlan.ko  netconsole.ko  ppp_deflate.ko  qlge            sky2.ko     tehuti.ko      via-velocity.ko
```

## 更新BootOS驱动

这里以igb驱动为例，首先需要安装开发编译工具以及内核头文件和开发包

```bash
# yum install kernel-devel kernel-headers gcc make rpm-build wget
```

接着下载igb最新的驱动，然后解压缩开始编译

```bash
# mkdir -p /root/rpmbuild/SOURCES/
# wget -P /root/rpmbuild/SOURCES/ https://downloadmirror.intel.com/13663/eng/igb-5.3.2.tar.gz
# tar zxpf /root/rpmbuild/SOURCES/igb-5.3.2.tar.gz
# rpmbuild -bb igb-5.3.2/igb.spec
```

编译好的rpm包放在```/root/rpmbuild/RPMS/x86_64/igb-5.3.2-1.x86_64.rpm```，需要离线安装到BootOS里面