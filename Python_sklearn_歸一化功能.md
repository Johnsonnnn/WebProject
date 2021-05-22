---
tags: Python
---

# Python Sklearn scale, StandardScale, normalize, MinMaxScale, QuantileTransformer

# scale
| axis |
| --- |
| 0 (default)|
| 1 |
```python
ss = scale(data, axis=0)
```

## StandardScaler
```python
standard = StandardScaler().fit_transform(data)
```

## normalize
| norm | axis | 
| --- | --- |
| l1 | 0 (default) |
| l2 (default) | 1 |
| max |
```python 
nor = normalize(data, norm='l2')
```

## MinMaxScale
```python
scaler = MinMaxScaler().fit_transform(data)
```

## QuantileTransformer
| output_distribution param |
| --- |
| normal |
| uniform (default) |
```python
quan = QuantileTransformer(output_distribution="normal").(data)
```