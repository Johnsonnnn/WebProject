---
tags: Python, Opencv
---
# Python Opencv 使用 HSV 擷取特定顏色

## HSV 色彩對照表
![](https://i.imgur.com/JZ5CNSm.png)
這個對照表只是大部分範圍
要更仔細就要使用 PS 查看HSV

## PS 的 HSV 值轉換
PS 中
> H 範圍在 0 ~ 360 。
> S 範圍在 0 ~ 1 %
> V 範圍在 0 ~ 1 %

Python 中
> H 範圍在 0 ~ 180
> S 範圍在 0 ~ 255
> V 範圍在 0 ~ 255

所以在Python 中就要將
```python
python_H = ps_H / 2
python_S = ps_S * 255 / 100
python_V = ps_V * 255 / 100
```

## 取出黃色
```python
import cv2
import numpy as np

# 讀取圖片
img = cv2.imread('./image.jpg')

# 圖片縮放為原本的0.5倍大小
img = cv2.resize(img, None, fx=0.5, fy=0.5)

# 轉為 HSV
hsv_img = cv2.cvtColor(reimg, cv2.COLOR_BGR2HSV)

# 取出黃色
mask = cv2.inRange(hsv_img, (26, 43, 46), (34, 255, 255))

# 為原圖加上遮罩
masked_img = cv2.add(img, np.zeros(np.shape(img), dtype=np.uint8), mask=mask)

# 顯示 hsv 圖片
cv2.imshow('yellow', mask)

# 顯示遮罩
cv2.imshow('yellow', mask)

# 顯示遮罩後的圖片
cv2.imshow('masked img', mask)

cv2.waitKey(0)
```

## BGR 通道分割
```python
(B, G, R) = cv2.split(img)
```