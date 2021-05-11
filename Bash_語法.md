---
tags:Linux
---

# Bash 語法

##宣告
```bash=
test="score"
score=90
```

## 輸出
```bash=
echo "my $test is $score"
echo "my "$test" is "$score

# my score is 90
# my score is 90
```

## if else
```bash

$str1 = $str2 字串是否相同
$str1 != $str2 字串是否不相同
-n $str 當 $str1 不是 null, 回傳 true
-z $str 當 $str1 是 null, 回傳 true

-eq 等於
-ne 不等於
-gt 大於
-ge 大於等於
-lt 小於
-le 小於等於
```

```bash=
if [ $score -gt 60 ]
then
  echo "pass"
else
  echo "no pass"
fi

# pass
```
:::danger
[] 前後都必須空一格
:::

```bash
-d $file 是目錄
-f $file 是檔案
-r $file 可讀
-s $file 不是空檔案
-w $file 可寫入
-x $file 可執行
```

```bash
$file="/home/pi"
if [ -d $file ]
then
  echo "is dir"
else
  echo "not dir"
fi

# is dir
```

## 要執行指令
```bash
a="aa"
end=".txt"
sp="_"
# 創建 aa.txt
touch $a$end

# 創建 aa_.txt
touch $a$sp$end

# 創建 aa_a.txt
touch $a"_a"$end
```