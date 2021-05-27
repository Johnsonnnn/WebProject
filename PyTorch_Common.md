---
tags: PyTorch
---

# PyTorch Common

### Use official dataset
```python
import torchvision

train_data = torchvision.datasets.MNIST(
    root='./mnist/',
    train=True,
    download=True,
    transform=torchvision.transforms.ToTensor()
)
```

### Merge Datasets
```python
import torch.utils.data as Data
a = [[1, 1, 1, 1], [2, 2, 2, 2]]
b = [3, 4]

c = Data.TensorDataset(a, b)
dataloader = Data.DataLoader(dataset=c, batch_size=1, shuffle=True)

for (x, y) in dataloader:
  print(x, y)
```

### Define Module
```python
import torch.nn as nn

class Net(nn.Module):
  def __init__(self):
    super(Net, self).__init__()
    
    self.encoder = nn.Sequential(
        nn.Linear(28 * 28, 128),
        nn.Tanh(),
        nn.Linear(128, 64),
        nn.Tanh(),
        nn.Linear(64, 16),
        nn.Tanh(),
        nn.Linear(16, 3),
        nn.Tanh(),
    )
    
    # print module constructure
    print(self.encoder)
    
  def forward(self, x):
    encoded = self.encoder(x)
    return encoded
```

### Optimizer, Loss
```python
import torch
import torch.nn as nn

optimizer = torch.optim.Adam(net.parameters(), lr=LR)
loss_func = nn.MSELoss()
...

loss = loss_func(x, y)

...

optimizer.zerograd()
loss.backward()
optimizer.step()

...
```

### Commonly used
```python
a = np.arange(100)
tensor = torch.from_numpy(a).type(torch.FloatTensor)

b = tensor.view(-1, 10, 10)


```