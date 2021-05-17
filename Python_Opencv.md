---
tags: Python, Opencv
---

# Python Opencv

+ 讀取格式為 BGR

###  讀取圖片
| 參數                 | 用法                 |
|:-------------------- | -------------------- |
| cv2.IMREAD_COLOR     | 正常顏色             |
| cv2.IMREAD_GRAYSCALE | 灰色                 |
| cv2.IMREAD_UNCHANGED | 正常顏色(包含透明度) |
```python
img = cv2.imread('./test.jpg')

img = cv2.imread('./test.jpg', cv2.IMREAD_GRAYSCALE)
```

### 寫入圖片
| 參數 | 用法 |
| --- | --- |
| [cv2.IMWRITE_JPEG_QUALITY, 90] | 設定 JPEG 圖片品質為 90（可用值為 0 ~ 100) |
| [cv2.IMWRITE_PNG_COMPRESSION, 5] | 設定 PNG 壓縮層級為 5（可用值為 0 ~ 9） |
```python
# 寫入 img 到 './test.jpg' 檔案中，會依據傳入的副檔名而不同
cv2.imwrite('./test.jpg', img)

# 設定 JPEG 圖片品質為 90（可用值為 0 ~ 100）
cv2.imwrite('./test.jpg', img, [cv2.IMWRITE_JPEG_QUALITY, 90])
```

### 縮放圖片

| 參數 | 說明 |
| cv2.INTER_AREA | 常用在縮小圖片 |
| cv2.INTER_CUBIC | 常用在放大圖片、4x4像素鄰域的雙三次插值 |
| cv2.INTER_NEAREST | 最近鄰插值 |
| cv2.INTER_LINEAR | 雙線性插值(默認) |
| cv2.INTER_LANCZOS4 | 8x8像素鄰域的Lanczos插值 |
```python
# cv2.resize(img, (w, h))
img = cv2.resize(img, (20, 40), cv2.INTER_AREA)

```


### 顯示圖片
+ 後面必須要加上```cv2.waitKey(0)``` 才會暫停且顯示圖片
```python
# 顯示在名為 'My Image' 的視窗中
cv2.imshow('My Image', img)
```

### 顯示視窗
```python
# 等待任意按鍵按下
cv2.waitKey(0)

# 等待 q 按下後跳出
if cv2.waitKey(1) & 0xFF == ord('q'):
  break
```

### 讓視窗可以自由縮放大小
```python
# 讓 'My Image' 視窗可以自由縮放大小
cv2.namedWindow('My Image', cv2.WINDOW_NORMAL)
```

### 關閉圖片視窗
```python
# 關閉 'My Image' 的圖片視窗
cv2.destroyWindow('My Image')

# 關閉所有視窗
cv2.destroyAllWindows()
```

### 圖片通道拆分
```python
# 拆分成 B, G, R 通道
B, G, R = cv2.split(img)
```

### 圖片通道合併
```python
# 合併 B, G, R 通道
merged_img = cv2.merge([B, G, R])
```

### 整張圖填滿同一個顏色
```python
# 整張圖填滿 100
img.fill(100)
```


### 畫直線
```python
# 畫直線，從 (0, 0) 到 (255, 255) 寬度 5px
cv2.line(img, (0, 0), (255, 255), (0, 0, 255), 5)
```

### 畫方框
```python
# cv2.rectangle(影像, 頂點座標, 對向頂點座標, 顏色, 線條寬度)

cv2.rectangle(img, (20, 60), (120, 160), (0, 255, 0), 2)

# 線寬 -1 == 填滿顏色
cv2.rectangle(img, (20, 60), (120, 160), (0, 255, 0), -1)

```

### 畫圓形
```python
# cv2.circle(影像, 圓心座標, 半徑, 顏色, 線條寬度)

cv2.circle(img, (90, 210), 30, (0, 255, 255), 3)
```

### 畫橢圓形
```python
# cv2.ellipse(影像, 中心座標, 軸長, 旋轉角度, 起始角度, 結束角度, 顏色, 線條寬度)

# 傾斜 45 度的紫色橢圓形
cv2.ellipse(img, (180, 200), (25, 55), 45, 0, 360, (205, 0, 255), 2)
```

### 寫文字

| 字型參數 | 用法 |
| --- | --- |
| cv2.FONT_HERSHEY_SIMPLEX | |
| cv2.FONT_HERSHEY_PLAIN | |
| cv2.FONT_HERSHEY_DUPLEX | |
| cv2.FONT_HERSHEY_COMPLEX | |
| cv2.FONT_HERSHEY_TRIPLEX | |
| cv2.FONT_HERSHEY_COMPLEX_SMALL | |
| cv2.FONT_HERSHEY_SCRIPT_SIMPLEX | |
| cv2.FONT_HERSHEY_SCRIPT_COMPLEX | |
```python
# cv2.putText(影像, 文字, 座標, 字型, 大小, 顏色, 線條寬度, 線條種類)

cv2.putText(img, text, (10, 40), cv2.FONT_HERSHEY_SIMPLEX, 1, (0, 255, 255), 1, cv2.LINE_AA)
```

### 模糊降噪
```python
# 平均模糊
# cv2.blur(gray, (kernel_size, kernel_size))
cv2.blur(gray, (3, 3))

# 高斯模糊
# cv2.GaussianBlur(gray, (kernel_size, kernel_size), 0)
cv2.GaussianBlur(gray, (3,3), 0)

# 中值模糊
# cv2.medianBlur(gray, kernel_size)
cv2.medianBlur(gray, 3)

# 雙向模糊、雙邊濾波器
# cv2.bilateralFilter(gray, color,pace,pace)
# color σ即顏色空間的標準差，愈大代表在計算時需要考慮更多的顏色
# pace σ即坐標空間的標準差，這個參數與Guassian filter使用的相同，數值越大，代表越遠的像素有較的權值
cv2.bilateralFilter(gray, 5, 21, 21)
```

### 圖片規一化
| 參數 | 說明 |
| cv2.NORM_MINMAX | 陣列的數值被平移或縮放到一個指定的範圍，線性歸一化 |
| cv2.NORM_INF | 切比雪夫距離、絕對值的最大值 |
| cv2.NORM_L1 | 曼哈頓距離、絕對值的和 |
| cv2.NORM_L2 | 歐幾里德距離|
```python
# cv2.normalize(img, shape, min, max, cv2.NORM_MINMAX)

# Method 1
# 創建與 img 相同大小的 zero，歸一化後的圖片為 out
zero = np.zeros(shape=img.shape)
out = cv2.normalize(img, zero, 0, 1, cv2.NORM_MINMAX)

# Method 2
# 傳入 img 本身的話，結果會覆蓋回 img
cv2.normalize(img, img, 0, 1, cv2.NORM_MINMAX)
```

### 直方圖均衡化
```python
# 必須為單一通道(灰階)才可以進行均衡化
cv2.equalizeHist(gray)
```

### 邊緣偵測
```python
# cv2.Canny(blur_gray, low_threshold, high_threshold)
cv2.Canny(gray, 100, 255)
```

### 圖片 and、or、not
```python
cv2.bitwise_and(X, Y)

cv2.bitwise_or(X, Y)

cv2.bitwise_not(X)
```

### 閥值
| 參數 |
| --- |
| cv2.THRESH_BINARY |
| cv2.THRESH_BINARY_INV |
| cv2.THRESH_TRUNC |
| cv2.THRESH_TOZERO |
| cv2.THRESH_TOZERO_INV |
| cv2.THRESH_MASK |
| cv2.THRESH_OTSU |
| cv2.THRESH_TRIANGLE |

```python
# 返回的 ret 為閥值
ret, img = cv2.threshold(img, 100, 150, cv2.THRESH_TRIANGLE)

ret1, img1 = cv2.threshold(img, 0, 255, cv2.THRESH_BINARY + cv2.THRESH_OTSU)

```
