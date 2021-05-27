---
tags: Python, Pillow
---

# Python Pillow common

### Save to gif
```python
from PIL import Image
import numpy as  np


imgs = list()
for i in range(10):
  img = np.arange(300, dtype=np.uint8).reshape(10, 10, 3)
  img = np.clip(img, 0, 255)
  img = Image.fromarray(img)
  imgs.append(img)

# loop=0 will repeat always
imgs[0].save('test.gif', format='GIF', append_images=imgs[1:], save_all=True, duration=100, loop=0)
```