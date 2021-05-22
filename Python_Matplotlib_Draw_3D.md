---
tags: Python
---

# Python Matplotlib Draw 3D


### Single plot 3D
```python
fig = plt.figure()
value = np.random.uniform(1, 15, 10240)


ax = fig.add_subplot(1, 1, 1, projection='3d')

color_map = plt.cm.get_cmap()
map = ax.scatter(R, G, B, c=value, cmap=color_map)
fig.colorbar(map, ax=ax)
plt.show()
```

### multiplot 3D
```python
fig = plt.figure()
value = np.random.uniform(1, 15, 10240)

ax = fig.add_subplot(1, 2, 1, projection='3d')

color_map = plt.cm.get_cmap()
map = ax.scatter(R, G, B, c=value, cmap=color_map)
fig.colorbar(map, ax=ax)

ax = fig.add_subplot(1, 2, 2, projection='3d')
color_map = plt.cm.get_cmap()
map = ax.scatter(sR, sG, sB, c=value, cmap=color_map)
fig.colorbar(map, ax=ax)

plt.show()
```