# 安装tftp服务

安装tftp服务和syslinux的tftpboot工具，如下：

```bash
# yum install tftp-server syslinux-tftpboot
# chkconfig xinetd on
```

配置tftp服务，设定tftp根目录为```/var/lib/tftpboot```，修改```disable = no```

```bash
# cat /etc/xinetd.d/tftp
# default: off
# description: The tftp server serves files using the trivial file transfer \
#       protocol.  The tftp protocol is often used to boot diskless \
#       workstations, download configuration files to network-aware printers, \
#       and to start the installation process for some operating systems.
service tftp
{
        socket_type             = dgram
        protocol                = udp
        wait                    = yes
        user                    = root
        server                  = /usr/sbin/in.tftpd
        server_args             = -s /var/lib/tftpboot
        disable                 = no
        per_source              = 11
        cps                     = 100 2
        flags                   = IPv4
}
```
