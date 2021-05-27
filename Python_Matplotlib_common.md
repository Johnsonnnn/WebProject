---
tags: Python, Matplotlib
---

# Python Matplotlib common

### 將 plt.fig 的圖片存成 np.array
```python
# one plot
fig = plt.figure()

# multi plot
fig, ax = plt.subplots(2, 2)

# to array
canvas.draw()
buf = fig.canvas.tostring_rgb()
w, h = canvas.get_width_height()
img = np.fromstring(buf, dtype=np.uint8).reshape(h, w, 3)
```
if not use ```canvas.draw()``` will
:::danger
```AttributeError: 'FigureCanvasTkAgg' object has no attribute 'renderer'```
:::


### get figsize
```python
w, h = plt.gcf().get_size_inches()
```

### save to gif
```python
ani = animation.ArtistAnimation(f, plt_imgs, interval=200, repeat_delay=1000)
ani.save("./test.gif",writer='pillow')
```