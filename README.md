COMP5434 Big Data Computing

## Requirements
See the [installation instruction](INSTALL.md) for a step-by-step installation guide.
See the [server instruction](SERVER.md) for server settup.
- Install [cuda-8.0](https://developer.nvidia.com/cuda-downloads)
- Install [cudnn v5.1](https://developer.nvidia.com/cudnn)
- Download [Pytorch 2.7](https://pytorch.org) and clone the repository.
```bash
pip install http://download.pytorch.org/whl/cu80/torch-0.1.12.post2-cp27-none-linux_x86_64.whl
pip install torchvision
git clone https://github.com/meliketoy/wide-resnet.pytorch
```

## Implementation Details

|   epoch   | learning rate |  weight decay | Optimizer | Momentum | Nesterov |
|:---------:|:-------------:|:-------------:|:---------:|:--------:|:--------:|
|   0 ~ 60  |      0.1      |     0.0005    | Momentum  |    0.9   |   true   |
|  61 ~ 120 |      0.02     |     0.0005    | Momentum  |    0.9   |   true   |
| 121 ~ 160 |     0.004     |     0.0005    | Momentum  |    0.9   |   true   |
| 161 ~ 200 |     0.0008    |     0.0005    | Momentum  |    0.9   |   true   |

## CIFAR-10 Results

![alt tag](imgs/cifar10_image.png)

Below is the result of the test set accuracy for **CIFAR-10 dataset** training.

**Accuracy is the average of 5 runs**

| network           | dropout | preprocess | GPU:0 | GPU:1 | per epoch    | accuracy(%) |
|:-----------------:|:-------:|:----------:|:-----:|:-----:|:------------:|:-----------:|
| wide-resnet 28x10 |    0    |     ZCA    | 5.90G |   -   | 2 min 03 sec |    95.83    |
| wide-resnet 28x10 |    0    |   meanstd  | 5.90G |   -   | 2 min 03 sec |    96.21    |
| wide-resnet 28x10 |   0.3   |   meanstd  | 5.90G |   -   | 2 min 03 sec |    96.27    |
| wide-resnet 28x20 |   0.3   |   meanstd  | 8.13G | 6.93G | 4 min 10 sec |  **96.55**  |
| wide-resnet 40x10 |   0.3   |   meanstd  | 8.08G |   -   | 3 min 13 sec |    96.31    |
| wide-resnet 40x14 |   0.3   |   meanstd  | 7.37G | 6.46G | 3 min 23 sec |    96.34    |
