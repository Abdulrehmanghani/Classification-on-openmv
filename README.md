# Classification-on-openmv

## Benchmarks on OpenMV
Include the benchmark results of model trained on edge impulse. 
The models are pretrained and finetuned on coustom data taken by OpenMV.
Depth Multiplier: MobileNet introduces a depth multiplier parameter that controls the number of input and output channels in the depthwise separable convolutions. It's used to reduce the model's complexity and size. A depth multiplier of 1.0 means no reduction, while a depth multiplier less than 1.0 (such as 0.35) reduces the number of channels in each layer.
Dropout rate is 0.1 in all models.

Pretrained models

| Model        | Input shape | Depth-Multiplier|   FPS      | Training acc | epochs | Status on openmv |
| ------------ | ----------- | --------------- | ---------- | ------------ | ------ | ---------------- |
| Mobilenet v2 | 96*96       |      0.05       |    16      |  92.7%       |  20    | Working          |
| Mobilenet v2 | 96*96       |      0.35       |     -      |  70.7%       |  20    | Not working      |  
| Mobilenet v2 | 96*96       |      0.1        |     -      |  92.7%       |  20    | Not working      |  
| Mobilenet v1 | 96*96       |      0.1        |   39.9     |  51.2%       |  20    | Working          |
| Mobilenet v2 | 96*96       |      0.2        |   21.7     |  80.5%       |  20    | Working          |  
| Mobilenet v2 | 96*96       |      0.25       |   19.9     |  75.6%       |  20    | Working          |

Custom  models

| Model        | Input shape |  Conv layers | kernel  |  Filters   |   FPS    | Training acc | epochs | Status on openmv |
| ------------ | ----------- | ------------ | ------- | ---------- | -------- | ------------ | ------ | ---------------- |
| conv2d       | 96*96       |      3       |   3     |  16,32,32  |  9.1     |    92.7%     |  20    |    Working       |
| conv2d       | 96*96       |      3       |   3     |  16,32,64  |    -     |    100%      |  20    |  Not  Working    | 

