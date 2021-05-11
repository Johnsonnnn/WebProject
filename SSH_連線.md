---
tags: Linux
---

# SSH 連線

## 1. 生成 RSA 密鑰

```bash
ssh-keygen -t rsa
```

## 2. 複製密鑰到目標 server
+ ### 方法1
```bash
# 複製 id_rsa.pub 到目標 server 的 /home/user
scp id_rsa.pub user@remote_server_IP:/home/user

# 登入 SSH
ssh user@remote_server_IP

# 將密鑰複製到 /home/user/.ssh/authorized_keys
cat /home/user/id_rsa.pub >> .ssh/authorized_keys
```

+ ### 方法2
```bash
# 將以上三步驟合為一步驟
ssh-copy-id -i .ssh/id_rsa.pub user@remote_server_IP
```

