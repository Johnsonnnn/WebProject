---
tags: Python
---

# Python multi plot and dynamic

```python
import matplotlib.pyplot as plt

f, a = plt.subplots(3, 2, figsize=(5, 2))
plt.ion()

for x in range(3):
    for i in range(2):
      a[x][i].clear()
      a[x][i].imshow(img[i])
      a[x][i].set_xticks(())
      a[x][i].set_yticks(())
    plt.draw()
    plt.pause(0.05)

plt.ioff()
plt.show()
```