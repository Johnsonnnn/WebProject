---
tags: Python, Numpy, Pillow
---

# Python Numpy array and Pillow transfor

### Numpy array to PIL
```python
# arr must be uint8 and scale == [0 ~ 255]
img = Image.fromarray(arr)
```

### PIL to Numpy array
```python
ii = Image.open('test.jpg')
img = np.array(ii)

```