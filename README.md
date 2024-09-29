# Classification-on-openmv

## Benchmarks on OpenMV
Include the benchmark results of model trained on edge impulse.The models are pretrained and finetuned on coustom data taken by OpenMV. <br>

**Depth Multiplier:**  MobileNet introduces a depth multiplier parameter that controls the number of input and output channels in the depthwise separable convolutions. It's used to reduce the model's complexity and size. A depth multiplier of 1.0 means no reduction, while a depth multiplier less than 1.0 (such as 0.35) reduces the number of channels in each layer.
Dropout rate is 0.1 in all models.<br>

## Dataset
The code of the data taken from the openMV is availble in the collect_data.py. To download dataset go the the [zip files](https://github.com/Abdulrehmanghani/Classification-on-openmv/blob/main/data_collection.py).<br>

### Pretrained models comparison 
The Status indcate the model deployed or not on the openMV.<br>

**Note:** This states are only for the coldrinks dataset.<br> 

| Model        | Input shape | Depth-Multiplier|   FPS      | Training acc | epochs | Status      |  Reson                         |
| ------------ | ----------- | --------------- | ---------- | ------------ | ------ | ----------- | ------------------------------ |
| Mobilenet v2 | 96*96       |      0.05       |    16      |  92.7%       |  20    | Working     |     -                          |
| Mobilenet v2 | 96*96       |      0.35       |     -      |  70.7%       |  20    | Not working | Model memory exceed the limit  |
| Mobilenet v2 | 96*96       |      0.1        |     -      |  92.7%       |  20    | Not working | Compute expensive              |
| Mobilenet v1 | 96*96       |      0.1        |   39.9     |  51.2%       |  20    | Working     |     -                          |
| Mobilenet v1 | 96*96       |      0.2        |   21.7     |  80.5%       |  20    | Working     |     -                          |
| Mobilenet v1 | 96*96       |      0.25       |   19.9     |  75.6%       |  20    | Working     |     -                          |

### Custom  models comparison <br> <br>

| Model        | Input shape |  Conv layers | kernel  |   Filters           |   FLOPS  |   FPS    | Training acc | epochs |  Status     |  Reson                         |
| ------------ | ----------- | ------------ | ------- | ------------------- | -------- | -------- | ------------ | ------ | ----------- | ------------------------------ |
| conv2d       | 96*96       |      3       |   3     |   16,32,32          | 0.0404 G |   9.1    |    92.7%     |  20    | Working     |     -                          |
| conv2d       | 96*96       |      4       |   3     |   2(16,32)          | 0.027 G  |   10.1   |    85.5%     |  20    | Working     |     -                          | 
| conv2d       | 96*96       |      6       |   3     |   2(16,32,48)       | 0.0283 G |   10.4   |    82.9%     |  20    | Working     |     -                          | 
| conv2d       | 96*96       |      8       |   3     | 2(16,32,48,64)      | 0.0289 G |   10.45  |    53.7%     |  20    | Working     |     -                          | 
| conv2d       | 96*96       |      8       |   3     | 2(16,32,64,128)     | 0.0298 G |   -      |    65.9%     |  20    | Not Working | Compute expensive              | 
| conv2d       | 96*96       |      10      |   3     | 2(16,32,64,128,256) | 0.0316 G |   -      |    56.7%     |  20    | Not Working | Model memory exceed the limit  |
| conv2d       | 64*64       |      6       |   3     | 2(16,32,64)         | 0.0129 G |   22.6   |    53.7%     |  20    | Working     |     -                          | 
| conv2d       | 64*64       |      8       |   3     | 2(16,32,64,128)     | 0.0133 G |   23     |    65.9%     |  20    | Working     |     -                          | 
