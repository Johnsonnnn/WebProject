---
tags: Python, Openvino
---

# Python Openvino IR model

## Read IR model

+ ### Method 1
:::danger
<b>Problem</b>: Recognize first image need more time (initalize time)
:::

| net.setPreferableBackend 參數|
| --- |
| cv2.dnn.DNN_BACKEND_DEFAULT |
| cv2.dnn.DNN_BACKEND_INFERENCE_ENGINE |
| cv2.dnn.DNN_BACKEND_OPENCV |

| net.setPreferableTarget 參數 |
| --- |
| cv2.dnn.DNN_TARGET_CPU |
| cv2.dnn.DNN_TARGET_MYRIAD |
| cv2.dnn.DNN_TARGET_GPU |

```python
# Use Opencv read Openvino IR model
net = cv2.dnn.readNetFromModelOptimizer(xml_path, bin_path)

net.setPreferableBackend(cv2.dnn.DNN_BACKEND_INFERENCE_ENGINE)

# Use VPU(NCS)
net.setPreferableTarget(cv2.dnn.DNN_TARGET_MYRIAD)

# Output node name
layerName = net.getLayerNames()

# Input Image (dims == 4)
net.setInput(blob_img)

# forward
net.forward(layerName)
```

+ ### Method 2

| ie.load_network --> device_name 參數 
| --- |
| CPU |
| GPU |
| MYRIAD |
```python
from openvino.inference_engine import IECore

# Read model and use openvino inference_engine to start
ie = IECore()

net = ie.read_network(model=model_xml, weights=model_bin)

# if want reuse network and define running device
net = ie.load_network(network=net, num_requests=2, device_name='CPU')

# Ready to input space
inputs = next(iter(net.input_info))

# async run
net.start_async(request_id=request_id, inputs={inputs:blob_img})
if net.requests[request_id].wait(-1) == 0:
  pass
  
# normal run
result = net.infer(inputs={inputs: blob_img})

```

## Preprocessing
```python
# input default type: BGR
# output: [n, c, h, w]
blob = cv2.dnn.blobFromImage(img, size=(w, h))

```