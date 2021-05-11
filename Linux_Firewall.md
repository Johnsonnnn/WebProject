---
tags: Linux, Firewall
---

# Linux Firewall

### 重新載入 firewall
```bash
firewall-cmd --reload
```
:::warning
+ 若先前未使用 --permanent 將會在 reload 後重新出現
    > 例如:
    > ```firewall-cmd --zone=public --remove-   service=ssh```
    > 在 reload 後 ssh 的服務依然存在
:::


### 設置預設的 zone
```bash
firewall-cmd --set-default-zone <zone-name>
```

### 查看開啟的 zone 跟對應的 network interface
```bash
firewall-cmd --get-active-zones

# 例如
# -------------------------------------
# home
#   interfaces: eth0 enp0s3
# -------------------------------------
# 就是 eth0 和 enp0s3 被規範於 home 的規則下
```

:::danger
1. 一張網卡只能存在一個zone裡面
> 例如:
> A zone 有 eth0
> B zone 就不能有 eth0

2. 假設我的網卡是enp0s3
> 當我從 zone A set default 到 zone b
> 會自動幫我將 enp0s3 換到 zone b
:::

:::warning
+ 若在新增功能時，未指定是哪個 zone ```--zone=<zone-name>``` 此功能將被加入到 default zone
:::

### 新增 network interface 到 zone
```bash
firewall-cmd --zone=public --add-interface=eth0
```

### 更換 network interface
```bash
firewall-cmd --zone=public --change-interface=eth0 --permanent
```

### Service


```bash
# 查看目前在資源包裡面所有能夠加入 zone 的 service
firewall-cmd --get-services

# 新增 service 到 zone
firewall-cmd --zone=public --add-service=ssh --permanent

# 從 zone 移除 service
firewall-cmd --zone=public --remove-service=ssh --permanent

# 列出目前所有 services
firewall-cmd --list-services
firewall-cmd --list-services --zone=public
```

```bash
# 查看 service 的細節
firewall-cmd --info-service=ssh

# ssh
#   ports: 22/tcp
#   protocols:
#   source-ports:
#   modules:
#   destination:
```
### 新增 service和自訂port
```bash
# 新增 service 到資源包裡面
firewall-cmd --new-service=iperf3 --permanent

# 設定 desctiption 到 service
firewall-cmd --permanent --service=iperf3 --set-description="iperf3 is a network performance testing tool"

# 設定 short description 到 service
firewall-cmd --permanent --service=iperf3 --set-short=iperf3

# 設定 port 到 service
firewall-cmd --permanent --service=iperf3 --add-port=5201/tcp
firewall-cmd --permanent --service=iperf3 --add-port=5201/udp

# 在資源包裡尋找 iperf3
firewall-cmd --get-services | grep iperf3
```
#### 創建 new service 後檔案會在"/etc/firewalld/services/iperf3.xml"裡面，後面是<new_service.xml>

```xml=
<?xml version="1.0" encoding="utf-8"?>
<service>
  <short>iperf3</short>
  <description>iperf3 is a network performance testing tool.</description>
  <port protocol="tcp" port="5201"/>
  <port protocol="udp" port="5201"/>
</service>
```
:::warning
+ 新增 service 到資源包後要 reload 才會生效
:::

#### 可以從檔案看到firewall service 裡面的 short, description, port，檔案在"/usr/lib/firewalld/services/ssh.xml:"，也可以直接將文字寫入檔案，創建 new service
```xml=
<?xml version="1.0" encoding="utf-8"?>
<service>
  <short>SSH</short>
  <description>Secure Shell (SSH) is a protocol for logging into and executing commands on remote machines...</description>
  <port protocol="tcp" port="22"/>
</service>
```

### Port
```bash
# 新增 port 到 zone
firewall-cmd --zone=public --add-port=9958/tcp

# 從 zone 移除 port
firewall-cmd --zone=public --remove-port=9958/tcp

# 列出目前所有的 ports
firewall-cmd --list-ports
firewall-cmd --list-ports --zone=public
```

:::warning
+ 移除 port 後要 reload 才會生效
:::


### 查看所有 zone 資訊
```bash
# 未指定就是目前的 default zone
firewall-cmd --list-all
firewall-cmd --zone=public --list-all
```



### 設置緊急模式
```bash
firewall-cmd --panic-on
firewall-cmd --panic-off

# 查看 panic 是否開啟
firewall-cmd --query-panic
```

## 連線時候的情況

### 1. 
當 A SSH 到 B 時候 B 把 Firewall 的服務移除
```bash
firewall-cmd --zone=public --remove-service=ssh --permanent
```
直到 A 退出 ssh 後重新連接 B 時候就無法連線

