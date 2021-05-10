---
tags: Python, Opencv
---

# Python Opencv 常用功能

## 轉換成 HSV 格式
```python
cv2.cvtColor(reimg, cv2.COLOR_BGR2HSV)
```

## 根據 HSV 取出某特定顏色的 mask
```python
mask = cv2.inRange(img_hsv, (h_min, s_min, v_min), (h_max, s_max, v_max))
```

## 腐蝕
```python
kernel_Ero = np.ones((3,1),np.uint8)
imgEro = cv2.erode(mask, kernel_Ero, iterations=1)
```

## 膨脹
```python
kernel_Dia = np.ones((3,5),np.uint8)
imgDia = cv2.dilate(mask, kernel_Dia, iterations=3)
```

## 邊緣偵測
```python
canny = cv2.Canny(mask, 30, 255)
```

## 霍夫曼直線檢測
```python
lines = cv2.HoughLines(canny, 1, np.pi / 180, 50)

for line in lines:
    rho, theta = line[0]
    a = np.cos(theta)
    b = np.sin(theta)

    x0 = a * rho
    y0 = b * rho
    x1 = int(x0 + 1000 * (-b))
    y1 = int(y0 + 1000 * a)
    x2 = int(x0 - 1000 * (-b))
    y2 = int(y0 - 1000 * a)
    cv2.line(img_rgb, (x1, y1), (x2, y2), (0, 0, 255), 2)
```

## 邊緣檢測[劃出最小矩形]
```python
_,contouts,hie = cv2.findContours(imgDia,cv2.RETR_EXTERNAL,cv2.CHAIN_APPROX_NONE)

for i in contouts:
    # 邊緣內面積像素點
    acc = cv2.contourArea(i)

    # 轉換出左上角x, y, width, height
    x,y,w,h = cv2.boundingRect(i)
    cv2.rectangle(img, (x, y), (int(x + w), int(y + h)), (0, 255, 255), 2)

    ## 劃出最小矩形(使用cv2.findContours)
    # center[(x, y), (h, w), angle of rotation]
    # 可以從 rect裡看出矩形旋轉的角度
    rect = cv2.minAreaRect(i)

    # box.shape=(4, 2)
    box = cv2.boxPoints(rect)  
    box = np.int0(box)
    cv2.drawContours(img, [box], 0, (0,0,255), 2)
```

