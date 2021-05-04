# Linux httpd 虛擬機相互連接與實作

## 虛擬機相互連接
:::danger
+ 兩台虛擬機必須在同一台主機
+ httpd(apache) server 防火牆要關掉
+ 要在同一網域
:::

1. 設定網路介面卡皆為Host-Only:
   + 裝置>網路>網路設定>附加到[僅限主機介面卡](Virtual Box)
2. 將兩台的網路設定為同一網域:
>例如:
IPADDRESS: 192.168.56.10 和 192.168.56.11
GATEWAY: 192.168.56.1
NETWORK: 192.168.56.0
NETMASK: 255.255.255.0
DNS1: 8.8.8.8
DNS2: 9.9.9.9
3. 測試兩台機器是否有通
>```>> ping 192.168.56.xx```



## httpd 設定與執行


:::info
Pre-requirement:
1. Install HTTP (Apache).
    + ```yum install httpd```
2. Configure basic web page.
    + Edit:  ```/var/www/html/index.html```
3. Start httpd services
    + ```systemctl start httpd.service```
    + ```systemctl status httpd.service```
4. Stop firewalld service
    + ```systemctl stop firewalld.service```
5. Web browser for connection testing.
:::

1. Needed packages:
    ```
    yum install mod_ssl openssl
    ```
    
2. Create a self-signed certificate:
    ```=
    # 產生私鑰
    openssl genrsa -out ca.key 2048

    # 產生 CSR。You will need to enter some infomation for the CSR.
    openssl req -new -key ca.key -out ca.csr

    # 產生自我簽署的金鑰
    openssl x509 -req -days 365 -in ca.csr -signkey ca.key -out ca.crt

    # 複製檔案至正確位置
    cp ca.crt /etc/pki/tls/certs/ca.crt
    cp ca.key /etc/pki/tls/private/ca.key
    cp ca.csr /etc/pki/tls/private/ca.csr
    ```

3. Configure SSL for Apache
    Add these to ```/etc/httpd/conf.d/ssl.conf```
    ```=
    SSLCertificateFile /etc/pki/tls/certs/ca.crt
    SSLCertificateKeyFile /etc/pki/tls/private/ca.key
    ```
    
4. Restart Apache
    ```systemctl restart httpd.service```
    
5. Open the **https** port in firewall
    ```firewall-cmd --add-service=https --zone=public --permanent```
    - [Linux Firewall - firewalld](https://hackmd.io/Hm0azl9OSs6HoVN-ltSRZQ)

6. Web-browser test: http**s**://...


## Problem and Solution
### apache在啟動時錯誤:
```bash
>> yum install httpd

Job for httpd.service failed because the control process exited with
error code.See "systemctl status httpd.service" and "journalctl -xe"
for details.
```
### 查看目前 Listening 的 Port:
```bash
netstat -punta | grep LISTEN
```
![](https://i.imgur.com/JINLSwX.jpg)


### Solution:
```bash
pkill httpd
```

