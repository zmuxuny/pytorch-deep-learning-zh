# 配置 PyTorch 编码环境

要把深度学习开发环境配置好，通常并不简单。

从硬件、软件到各种细节，都可能影响“你的代码能否在别人机器上和你本机一样运行”。

本课程会尽量把流程保持简单。

但也不会简单到让你离开本课程就无法复用。

我们提供两种配置方式：一种更省事，另一种前期步骤更多但长期更灵活。

1. 使用 Google Colab（最简单）
2. 在本地或远程机器自行配置（步骤稍多，但更可控）

**注意：** 下文都不能替代 [PyTorch 官方安装文档](https://pytorch.org/get-started/locally/)。如果你打算长期使用 PyTorch，建议熟悉官方文档。

## 1. 使用 Google Colab（最简单）

Google Colab 是一个免费的在线交互式计算环境（基于 Jupyter Notebooks，这是数据科学的常用标准）。

Google Colab 的优点：
* 几乎零配置（Colab 预装了 PyTorch，以及 pandas、NumPy、Matplotlib 等常见包）
* 可通过链接分享你的工作
* 可免费使用 GPU（让深度学习代码更快），付费后还能获得更强算力

Google Colab 的不足：
* 会话超时（多数 Colab 会话状态最多保留 2-3 小时，付费版会更久）
* 不能直接使用本地磁盘（但有替代方案）
* 对脚本化工程（把代码模块化）支持不如本地开发完善

### 先用 Colab 起步，必要时再扩展

课程前几章（00-04）我们会主要使用 Google Colab。

因为它已经足够满足这一阶段需求。

实际上，这也是我自己常用的工作流。

我会在 Google Colab 里完成大量入门和实验性工作。

当某个方案被验证并准备做成更大项目时，我再迁移到本地或云端环境。

### 如何开始使用 Google Colab

建议先过一遍 [Google Colab 入门 notebook](https://colab.research.google.com/notebooks/basic_features_overview.ipynb)，熟悉界面和常用按钮。

### 一键打开课程 notebook

熟悉 Colab 后，你可以在在线书版本或 GitHub 页面点击顶部的 "Open in Colab" 按钮，直接运行课程 notebook。

![open a course notebook in Google Colab via open in Colab button](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/setup-open-in-colab-cropped.gif)

如果你想复制一份 notebook 到 Google Drive，可点击 "Copy to Drive"。

### 通过链接在 Colab 打开 notebook

也可以把 GitHub 上的 notebook 链接直接粘贴到 Google Colab 打开。

![open a course notebook in Google Colab via GitHub link](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/setup-open-notebook-in-colab-via-link.png)

这样你会在 Colab 中得到一个可运行 notebook。

但这更适合快速测试。正式学习时，强烈建议你**自己手写代码**，而不是只跑现成代码。

### 在 Google Colab 开启 GPU

如果要使用支持 CUDA 的 NVIDIA GPU（CUDA 是让深度学习在 GPU 上加速的接口），可在 Colab 中进入 `Runtime -> Change runtime type -> Hardware Accelerator -> GPU`（注意：会触发运行时重启）。

![Getting access to a GPU in Google Colab](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/setup-get-gpu-colab-cropped.gif)

检查 Colab 是否已启用 GPU：

```
!nvidia-smi
```

如果有 GPU，会显示你当前分配到的型号信息。

检查 PyTorch 是否能访问 GPU：

```python
import torch  # Google Colab 默认已安装 torch
print(torch.cuda.is_available())  # 若 PyTorch 可使用 GPU，将返回 True
```

如果 PyTorch 成功识别 Colab GPU，输出会是 `True`。

## TK - 2. 本地配置（Linux 版本）

> **注意：** 再次强调，这不是 [PyTorch 本地安装官方文档](https://pytorch.org/get-started/locally/) 的替代，只是本课程可用的一种配置路径。

本节**主要面向 Linux 系统**（世界上最常见的系统）。如果你使用 Windows 或 macOS，请参考 PyTorch 官方文档。

本流程也**默认你有 NVIDIA GPU 可用**。

为什么采用这套方案？

因为这是我作为机器学习工程师几乎每天都在用的配置。它覆盖面广，且后续改造空间大。

开始吧。

### Linux + GPU 本地配置步骤
TK TODO - add step for install CUDA drivers
TK image - overall setup of the course environment (e.g. Jupyter Lab inside conda env)

1. [安装 Miniconda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html)（如果你已有 Anaconda 也可以）。关键是你能在命令行中使用 `conda`。继续下一步前，请先完整完成 Miniconda 官方安装流程。
2. 创建课程目录并进入。示例：
```
mkdir ztm-pytorch-course
cd ztm-pytorch-course
```
3. 在该目录下创建 `conda` 环境。下面命令会创建一个位于 `env` 子目录的环境（例如 `ztm-pytorch-course/env`）。出现 `y/n?` 时输入 `y`。
```
conda create --prefix ./env python=3.8.13
```
4. 激活该环境。
```
conda activate ./env
```
5. 安装课程依赖，包括 PyTorch 和 CUDA Toolkit（用于 GPU 加速）。以下命令可直接执行（**注意：** 这组命令针对 Linux + NVIDIA GPU，其他系统请参考 [PyTorch 安装文档](https://pytorch.org/get-started/locally/)）：
```
conda install -c pytorch pytorch=1.10.0 torchvision cudatoolkit=11.3 -y
conda install -c conda-forge jupyterlab torchinfo torchmetrics -y
conda install -c anaconda pip -y
conda install pandas matplotlib scikit-learn -y
```
6. 通过启动 Jupyter Lab 验证安装是否成功：

```bash
jupyter lab
```

7. Jupyter Lab 启动后，新建一个 notebook，在单元中运行以下代码：
```python
import pandas as pd
import numpy as np
import torch
import sklearn
import matplotlib
import torchinfo, torchmetrics

# 检查 PyTorch（应打印一个 tensor）
print(torch.randn(3, 3))

# 检查 GPU（应返回 True）
print(torch.cuda.is_available())
```

若以上代码无报错，即可开始课程。

如果遇到问题，可到 [Learn PyTorch GitHub Discussions](https://github.com/mrdbourke/pytorch-deep-learning/discussions) 提问，或查看 [PyTorch 安装文档](https://pytorch.org/get-started/locally/)。