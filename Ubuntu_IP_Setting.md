# Ubuntu IP Setting

1. 查看網路卡介面
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
   
2. 產生網路介面設定檔
```>> sudo netplan generate```

3. 打開 ```/etc/netplan/01-netcfg.yaml``` 網路介面設定檔（或其他的設定檔），填入以下資訊

```bash
# 網路介面設定檔
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      addresses: [ 192.168.56.10/24 ]
      gateway4: 192.168.56.1
      nameservers:
          search: [ your.domain.tw ]
          addresses: [ 8.8.8.8, 9.9.9.9 ]
```

4. 測試並套用網路介面設定檔
```bash
>> sudo netplan try
#120 秒內沒有進行確認，就會自動恢復成原來的網路設定，這個功能可以避免在遠端
#更改設定時，不小心把自己檔在外面。
```

> 也可以直接套用網路介面設定檔
```>> sudo netplan apply```

5. 查看網路設定
```bash
>> ifconfig enp0s3
enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.56.10  netmask 255.255.255.0  broadcast 192.168.56.1
        inet6 2001:e10:2000:17:e643:4bff:fe20:bddb  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::e643:4bff:fe20:bddb  prefixlen 64  scopeid 0x20<link>
        ether e4:43:4b:20:bd:db  txqueuelen 1000  (Ethernet)
        RX packets 14028  bytes 945915 (945.9 KB)
        RX errors 0  dropped 686  overruns 0  frame 0
        TX packets 617  bytes 123948 (123.9 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device memory 0x9e100000-9e17ffff
```