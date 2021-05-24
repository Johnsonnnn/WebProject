---
tags: Python
---

# Python 多賦值問題，推論與結果


以下是我推論出來的，不確定是不是正確答案
```python
class Node:
	def __init__(self):
		self.parent = None

if __name__ == __main__:
	a = Node()
	a.parent = 20
```


## 題目一:
先來看他是如何賦值的，先給他們標上記號好分辨
```python
   (1), (2) =  (3),   (4)
a.parent, a = None, a.parent

輸出結果:
a = 20
```
### 1. <font color='red'>(x) 想法一:</font>

賦予數值的順序: (1)把 4 給 2 ，(2)把 3 給 1
(1) a = a.parent ，使得 a 等於 20
(2) a.parent = None，若此推論正確則這裡應該會有 error
但是由於 a 已經等於 20，不會有參數 parent
程序能正確運行，所以此推論錯誤

### 2. <font color='red'>(x) 想法二:</font>

順序: (1)把 3 給 1 ，(2)把 4 給 2
a.parent = None 使得 a.parent 值為 None
然後 a = a.parent，若依照此想法則 a 的答案應該會是 None
但是正確答案是20，此推論錯誤

### 3. <font color='red'>(x) 想法三:</font>

因為依照基本的 a, b = b, a 能夠正確交換順序
所以應該有暫時儲存資料的部分
先把右邊的 None, a.parent 放入暫存的資料區
然後順序: (1)把 4 給 2 ，(2)把 3 給 1
(1)a = a.parent 使得 a = 20
(2) a.parent = None ，因 a 無 parent
正確答案是20，此推論錯誤，也沒使用到暫存資料區
### 4. <font color='green'>(o) 想法四:</font>

一樣有個暫存區，把 None, a.parent 存入暫存區
順序: (1)把 3 給 1 ，(2)把 4 給 2
(1) a.parent = None，此時 a.parent 參數為 None
(2) 使得 a = a.parent
無暫存的時候這裡是應該是要錯誤的，但正確結果是 20
有暫存時候可以看到我們的暫存區 a.parent 的參數正好是 20 
所以將暫存區的 a.parent 賦予值給 a，此推論正確

## 題目二
```python
(1),  (2)   =    (3),   (4)
a, a.parent = a.parent, None

輸出結果:
AttributeError: 'int' object has no attribute 'parent'
```
### <font color='green'>(o) 想法一:</font>
依照上面第四部成功的結果來推算
把 a.parent, None 存入暫存區
順序: (1)把 3 給 1 ，(2)把 4 給 2
(1) a = a.parent 使得 a 的值為 20
(2) a.parent = None，因為 a 是 int 所以沒有 parent 參數
推論正確

## 題目三
已經知道兩個參數的運作方式，那三個參數是如何運作?
在已知題目一能正常運算，左右再加上一個參數試試
```python
  (1),   (2),   (3)   =  (4),    (5),  (6)
a.parent, a, a.parent = None, a.parent, 10
```
這次就先不看結果，看看之前推論是否正確
先把 None, a.parent, 10 放入暫存區
順序: (1)把 4 給 1 ,(2)把 5 給 2 ,(3)把 6 給 3
(1)a.parent = None，使得 a.parent 為 None
(2)a = a.parent，此時要從暫存區讀取資料:a.parent = 20
所以這裡的 a 為 20
(3)a.parent = 10，需要把 10 的值給 a.parent
但因為 a 目前為 20 所以他沒有參數 parent
來看結果
```python
輸出結果:
AttributeError: 'int' object has no attribute 'parent'
```
得出答案，此推論正確
* 要注意的地方是這裡的第二步(2)是從暫存區讀取資料，若是從第一步(1)的結果 a.parent = None 來把 a.parent 的值給 a 此時 a 的值為 None 應該輸出的是```AttributeError: 'NoneType' object has no attribute 'parent'```
