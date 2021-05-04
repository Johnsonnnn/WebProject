# Cmd WIFI Command

```bash
# Show all connected wifi
>> netsh wlan show profiles

# Show "XX" wifi detail
>> netsh wlan show profiles XX key=clear

# 列出配置文件
>> netsh wlan show profile

# 導出配置文件
>> netsh wlan export profile key=clear

# 删除配置文件
>> netsh wlan delete profile name=""

# 添加配置文件
>> netsh wlan add profile filename=""

# Connect to wifi
>> netsh wlan connect name=""

# 列出接口
>> netsh wlan show interface

# 開啟接口
>> netsh interface set interface "Interface Name" enabled

# 列出所有可連接wifi詳細信息
>> netsh wlan show networks mode=bssid

# 為cmd/powershell設置代理
>> netsh winhttp set proxy 127.0.0.1:1080

# 取消代理
>> netsh winhttp reset proxy

# 查看代理
>> netsh winhttp show proxy


```