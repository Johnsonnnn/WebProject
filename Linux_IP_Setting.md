# Linux IP Setting

查看 `/etc/sysconfig/network-scripts/` 裡面的資料夾
``` bash=
>> cd /etc/sysconfig/network-scripts/
>> ls


ifcfg-enp0s3  ifdown-ppp       ifup-eth     ifup-sit
ifcfg-lo      ifdown-routes    ifup-ippp    ifup-Team
ifdown        ifdown-sit       ifup-ipv6    ifup-TeamPort
ifdown-bnep   ifdown-Team      ifup-isdn    ifup-tunnel
ifdown-eth    ifdown-TeamPort  ifup-plip    ifup-wireless
ifdown-ippp   ifdown-tunnel    ifup-plusb   init.ipv6-global
ifdown-ipv6   ifup             ifup-post    network-functions
ifdown-isdn   ifup-aliases     ifup-ppp     network-functions-ipv6
ifdown-post   ifup-bnep        ifup-routes
```

網路卡為 `ifcfg-網路卡名稱`
此張網路卡名稱為 `enp0s3`
在網路卡詳細資料也可看到

```bash
>> ifconfig

enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.2.15  netmask 255.255.255.0  broadcast 10.0.2.255
        inet6 fe80::49cd:d69a:1408:7016  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:ef:e7:f0  txqueuelen 1000  (Ethernet)
        RX packets 930  bytes 106715 (104.2 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 642  bytes 70490 (68.8 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 12  bytes 984 (984.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 12  bytes 984 (984.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
若不能使用ifconfig的話
`ifconfig: command not found`
就要先安裝
`>> sudo yum install net-tools`



查看 `ifcfg-enp0s3`
```bash
>> cat ifcfg-enp0s3

TYPE="Ethernet"
BOOTPROTO="dhcp"
DEFROUTE="yes"
IPV4_FAILURE_FATAI="no"
IPV6_INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_FAILURE_FATAL="no"
IPV6_ADDR_GEN_MODE="stable-privacy"
NAME="enp0s3"
UUID="0b4532ad-2de2-4704-b520-74e622700fce"
DEVICE="enp0s3"
ONBOOT="yes"
DNS1="8.8.8.8"
PEERDNS="yes"
IPV6_PEERDNS="yes"
IPV6_PEERROUTES="yes"
IPV6_PRIVACY="no"
```

修改下面選項，若沒有就新增
```bash
BOOTPROTO="static"
ONBOOT="yes"
IPADDR="192.168.56.10"
GATEWAY="192.168.56.1"
NETWORK="192.168.56.0"
NETMASK="255.255.255.0"
DNS1="8.8.8.8"
DNS2="9.9.9.9"
```


> BOOTPROTO：IP 取得方式 static 代表靜態 IP 位址，dhcp 代表動態取得 IP 位址。

> ONBOOT：設定為 yes 代表開機自動啟動此網路介面。
IPADDR：IP 位址。
GATEWAY：預設閘道。
NETWORK：網路的位址。
NETMASK：網路遮罩。
DNS1：第一台 DNS 伺服器。
DNS2：第二台 DNS 伺服器。

```bash
# 啟動網路介面
>> ifup enp0s3

# 停用網路介面
>> ifdown enp0s3
```