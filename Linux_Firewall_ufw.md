---
tags: Linux, Ubuntu, ufw
---
# Linux Firewall - ufw

:::warning
Ubuntu系統
:::

### 狀態
```bash
sudo ufw status
sudo ufw enable
sudo ufw disable
```

### 預設
```bash
# 預設允許
sudo ufw default allow

# 預設封鎖
sudo ufw default deny
```

### 設定 port
``` bash
# 允許 ssh
sudo ufw allow ssh

# 允許 22 port
sudo ufw allow 22

# 封鎖 21 port
sudo ufw deny 21
```

### 設定 port 範圍
```bash
# 允許 TCP 6000 ~ 6007
sudo ufw allow 6000:6007/tcp

# 封鎖 UDP 6000 ~ 6007
sudo ufw deny 6000:6007/udp
```

### 設定靜態 IP
```bash
# 允許 192.168.11.10 的所有連線
sudo ufw allow from 192.168.11.10

# 允許 192.168.11.1~192.168.11.255 的所有連線
sudo ufw allow from 192.168.11.0/24

# 封鎖 192.168.11.4 的所有連線
sudo ufw deny from 192.168.11.4
```

### 查看與刪除設定的規則
```bash
# 查看 ufw 狀態(帶有順序)
sudo ufw status numbered

# 刪除某一項規則
sudo ufw delete [the rule number]

# 重設所有規則
sudo ufw reset
```