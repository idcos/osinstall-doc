# 安装dhcp服务

网络启动依赖dhcp服务，并且需要配置pxe启动参数。

```bash
# yum install dhcp
# chkconfig dhcpd on
```

配置dhcp服务，请用户根据自己的实际情况修改网段

```bash
# cat /etc/dhcp/dhcpd.conf
allow booting;
allow bootp;
ddns-update-style none;
ping-check true;
ping-timeout 3;
default-lease-time 1800;
max-lease-time 3600;
next-server 192.168.0.1;
filename "gpxelinux.0";
option domain-name-servers 192.168.0.1;
option domain-search "idcos.net";
option root-path "192.168.0.1:/";

subnet 192.168.0.0 netmask 255.255.255.0 {
    range 192.168.0.101 192.168.0.200;
    option routers 192.168.0.1;
}
```
