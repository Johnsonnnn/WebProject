---
tags: Python
---

# Python Numpy bytes np.array transfer

### np.array to bytes
```python
zeros = np.zeros(shape=[1, 10])
data_bytes = zeros.tobytes()
```

```python
da = b'hello'

# 一定要加 dtype
data = np.frombuffer(da, dtype=np.uint8)
```