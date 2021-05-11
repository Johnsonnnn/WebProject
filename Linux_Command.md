---
tags: Linux
---
# Linux Command

## 搜尋在檔案中的文字
```bash
# 在 /etc/*.conf 中搜尋 network 關鍵字
grep network /etc/*.conf

# 遞迴搜尋在 /etc 中搜尋所有檔案有 network 的關鍵字
grep -r network /etc

# 在 / 裡搜尋有關 *.txt 的檔案名稱
find / -name *.txt
```
> 關於 grep
> ```bash
> -r 遞迴搜尋
> -n 標示行號
> -v 反向匹配
> -i 不分大小寫
> ```


## 忽略 Permission denied
```
# 加上 | grep -v "Permission denied"
grep -v "Permission denied"
```

## 執行 ```test.sh``` 檔案
```bash
source test.sh
```

## 查看執行過的指令
+ 執行過的指令都會在 ```~/.bash_history``` 裡面
+ 直接用 history 查看

## 自動執行
+ 開啟 bash (terminal)都會自動執行 ```~/.bashrc```
+ 使用者登入時會執行```~/.profile```
+ 使用者登出時會執行```~/.bash_logout```


## 開機自動執行程式(Raspberry Pi)
要執行的檔案是 ```~/start.sh```

+ 方法1
```bash
# 到 /etc/xdg/lxsession/LXDE-pi 檔案下
cd /etc/xdg/lxsession/LXDE-pi

# 打開 autostart 進行編輯，沒有就直接創建
vi autostart
```

檔案內容為
```bash=
@lxpanel --profile LXDE-pi
@pcmanfm --desktop --profile LXDE-pi
@xscreensaver -no-splash

lxterminal --command="/home/pi/start.sh"
```

+ 方法2
```bash
# 編輯 /etc/rc.local
vi /etc/rc.local
```
在檔案尾部加入
```bash=
# 要在 exit 0 之前加入指令
/opt/my_script.sh

exit 0
```

