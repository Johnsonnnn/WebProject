---
tags: Python
---

# Python Pandas

### Read csv
```python
path = './test.csv'
df = pd.read_csv(path)

df = pd.read_csv(path, index=False, header=False)

# if file size == 0 will add header in csv
with open(path, 'w') as ff:
  df.to_csv(ff, header=ff.tell() == 0, index=False)
```


```python
df = pd.DataFrame(
    {
        'Date': 
             ['08/09/2018', 
              '10/09/2018', 
              '08/09/2018', 
              '10/09/2018'],
        'Fruit': 
             ['Apple', 
              'Apple', 
              'Banana', 
              'Banana'],
        'Sale':
             [34,
              12,
              22,
              27]
    })
print(df)
>>

         Date   Fruit  Sale
0  08/09/2018   Apple    34
1  10/09/2018   Apple    12
2  08/09/2018  Banana    22
3  10/09/2018  Banana    27
```

## Basic calculation
+ ### df.sum()
```python
# 以 columns 作為 index，對每個 columns 做總和，若是 str 則相連
print(df.sum())
>>

Date     08/09/201810/09/201808/09/201810/09/2018
Fruit                      AppleAppleBananaBanana
Sale                                           95
dtype: object
```

+ ### df.max()
```python
# 以 columns 作為 index，對每個 columns 求 max
print(df.max())
>>

Date     10/09/2018
Fruit        Banana
Sale             34
dtype: object
```

+ ### df.min()
```python
# 以 columns 作為 index，對每個 columns 求 min
print(df.min())
>>

Date     08/09/2018
Fruit         Apple
Sale             12
```

+ ### df.mean()
```python
# 以 columns 作為 index，只對每個 columns 數字做 mean
print(df.mean())
>>

Sale    23.75
dtype: float64
```

## Useful
+ ### Group by
```python
# 
print(df.groupby('Fruit')['Sale'].get_group('Apple'))
>>

# 以 Fruit 作為 index，Sale 為第一 columns，提取所有 Fruit 為 apple 的 Sale 欄位
0    34
1    12
Name: Sale, dtype: int64
```


+ ### Use df.groupby()
```python
# 以 fruit 作為 index，取得所有 Fruit 為 Apple 的資料
print(df.groupby('Fruit').get_group('Apple'))
>>

         Date  Fruit  Sale
0  08/09/2018  Apple    34
1  10/09/2018  Apple    12
```

+ ### 選取 row 的資料
```python
# 提取第 0 列的資料，columns 作為 index
print(df.loc[0])
>>

Date     08/09/2018
Fruit         Apple
Sale             34
Name: 0, dtype: object

# 使用下面更改過 index 的資料，取得 index 為 A 的資料
print(df.loc['A'])
>>

Date     08/09/2018
Fruit         Apple
Sale             34
Name: A, dtype: object

# iloc 是輸入第幾個，loc 是輸入 index name
# 選取 row == 1 的資料
print(df.iloc[1])
>>

Date     10/09/2018
Fruit         Apple
Sale             12
Name: B, dtype: object
```

+ ### Change index
```python
df.index = ['A', 'B', 'C', 'D']
>>

         Date   Fruit  Sale
A  08/09/2018   Apple    34
B  10/09/2018   Apple    12
C  08/09/2018  Banana    22
D  10/09/2018  Banana    27
```
+ ### set_index
```python
# 以 Fruit Sale 作為 index
print(df.set_index(['Fruit', 'Sale']))
>>

                   Date
Fruit  Sale            
Apple  34    08/09/2018
       12    10/09/2018
Banana 22    08/09/2018
       27    10/09/2018
```

