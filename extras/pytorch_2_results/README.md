# PyTorch 2.0 简要测试结果

## 测试配置
* **模型：** ResNet50（来自 TorchVision）
* **数据：** CIFAR10（来自 TorchVision）
* **轮次：** 5（单次运行）与 3 x 5（多次运行）
* **Batch size：** 128
* **图像尺寸：** 224

完整代码见 [PyTorch 2.0 Intro notebook](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/extras/pytorch_2_intro.ipynb)。

## 单次运行（5 个 epoch）

### NVIDIA RTX 4080

![results of training a resnet50 model on a nvidia rtx 4080 for 5 epochs with a batch size of 128 and image size of 224](figures/single_run_NVIDIA_GeForce_RTX_4080_ResNet50_CIFAR10_224_train_epoch_time.png)

### NVIDIA A100

![results of training a resnet50 model on a nvidia a100 for 5 epochs with a batch size of 128 and image size of 224](figures/single_run_NVIDIA_A100-SXM4-40GB_ResNet50_CIFAR10_224_train_epoch_time.png)

## 多次运行（5 个 epoch，重复 3 次）

### NVIDIA RTX 4080

![results of training a resnet50 model on an rtx 4080 for 5 epochs with a batch size of 128 and image size of 224 for 3 rounds](figures/multi_run_NVIDIA_GeForce_RTX_4080_ResNet50_CIFAR10_224_train_epoch_time.png)

### NVIDIA A100

![results of training a resnet50 model on a nvidia a100 for 5 epochs with a batch size of 128 and image size of 224 for 3 rounds](figures/multi_run_NVIDIA_A100-SXM4-40GB_ResNet50_CIFAR10_224_train_epoch_time.png)