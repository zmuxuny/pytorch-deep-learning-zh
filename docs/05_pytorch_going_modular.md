[查看源码](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/05_pytorch_going_modular.md) | [查看幻灯片](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/slides/05_pytorch_going_modular.pdf) 

# 05. PyTorch 模块化实践

本节要回答的问题是：“如何把 notebook 里的代码转换成 Python 脚本？”

为此，我们会把 [notebook 04. PyTorch Custom Datasets](https://www.learnpytorch.io/04_pytorch_custom_datasets/) 中最有用的代码单元，整理成一组 Python 脚本，并保存到名为 [`going_modular`](https://github.com/mrdbourke/pytorch-deep-learning/tree/main/going_modular) 的目录里。

## 什么是模块化（going modular）？

模块化指的是：把 notebook 代码（来自 Jupyter Notebook 或 Google Colab）拆分成多个功能清晰的 Python 脚本。

例如，我们可以把 notebook 中的一系列代码单元拆成下面这些文件：

* `data_setup.py` - 用于准备数据与按需下载数据。
* `engine.py` - 包含各种训练相关函数。
* `model_builder.py` 或 `model.py` - 用于创建 PyTorch 模型。
* `train.py` - 负责调用其他文件并训练目标模型。
* `utils.py` - 存放常用工具函数。

> **注意：** 上述文件命名与目录组织取决于你的具体场景和代码需求。Python 脚本和 notebook 单元一样灵活，几乎任何功能都可以单独拆出来。

## 为什么要做模块化？

Notebook 非常适合快速迭代探索和实验。

但在更大规模项目中，Python 脚本通常更易复现、也更便于运行。

当然这点也存在争议，比如 [Netflix 展示过他们如何将 notebook 用于生产代码](https://netflixtechblog.com/notebook-innovation-591ee3221233)。

**生产代码（Production code）** 是指对人或系统持续提供服务的代码。

例如，如果你有一个在线应用供他人访问使用，那么支撑该应用运行的代码就是**生产代码**。

另外，像 fast.ai 的 [`nb-dev`](https://github.com/fastai/nbdev)（notebook development 的缩写）这类工具，也支持你用 Jupyter Notebook 编写完整的 Python 库（包括文档）。

### Notebook 与 Python 脚本的优缺点

两种方式各有支持者。

下表总结了一些核心差异。

|               | **优点**                           | **缺点**                   |
| ------------- | ---------------------------------- | -------------------------- |
| **Notebooks** | 易于实验和快速上手                 | 版本管理可能较难           |
|               | 易于分享（例如 Google Colab 链接） | 不便只复用某一小部分       |
|               | 可视化能力强                       | 文本与图形可能干扰代码阅读 |

|                    | **优点**                                        | **缺点**                                                  |
| ------------------ | ----------------------------------------------- | --------------------------------------------------------- |
| **Python scripts** | 可将代码模块化复用（减少在 notebook 里重复写）  | 实验可视化不如 notebook（通常要运行整段脚本而非单个单元） |
|                    | 可配合 git 做版本管理                           |                                                           |
|                    | 许多开源项目采用脚本方式                        |                                                           |
|                    | 更适合大项目部署到云平台（notebook 支持相对少） |                                                           |

### 我的工作流

我通常会先在 Jupyter/Google Colab notebook 中启动机器学习项目，用于快速实验与可视化。

当某些方案验证可行后，再把最有价值的代码迁移到 Python 脚本中。

<img src="https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/05-my-workflow-for-experimenting.png" alt="一种可参考的机器学习编码流程：先在 Jupyter/Colab 验证，再迁移到 Python 脚本。" width=1000/>

*机器学习代码的工作流没有唯一答案。有人喜欢先写脚本，也有人（比如我）更喜欢先用 notebook，再迁移到脚本。*

### 真实世界中的 PyTorch

在实际项目中，你会看到很多基于 PyTorch 的仓库都通过 Python 脚本来说明如何运行训练流程。

例如，文档里常会要求你在终端执行如下命令来训练模型：

```
python train.py --model MODEL_NAME --batch_size BATCH_SIZE --lr LEARNING_RATE --num_epochs NUM_EPOCHS
```

<img src="https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/05-python-train-command-line-annotated.png" alt="使用不同超参数训练 PyTorch 模型的命令行示例" width=1000/> 

*在命令行运行 PyTorch 的 `train.py`，并传入不同的超参数设置。*

这里的 `train.py` 是目标脚本，通常会包含训练 PyTorch 模型所需函数。

而 `--model`、`--batch_size`、`--lr`、`--num_epochs` 这类参数称为命令行参数标志（argument flags）。

你可以按需传入参数值，只要与 `train.py` 中定义兼容就能运行，不兼容则会报错。

例如，如果我们希望用 notebook 04 中的 TinyVGG 训练 10 个 epoch，batch size 为 32、学习率为 0.001：

```
python train.py --model tinyvgg --batch_size 32 --lr 0.001 --num_epochs 10
```

你可以在 `train.py` 里定义任意数量的参数标志来满足你的实验需求。

PyTorch 官方关于训练 SOTA 计算机视觉模型的博客也采用了这种风格。

<img src="https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/05-training-sota-recipe.png" alt="训练先进计算机视觉模型的 PyTorch 训练脚本配方" width=800/>

*使用 8 张 GPU 训练 SOTA 视觉模型的 PyTorch 命令行训练方案。来源：[PyTorch blog](https://pytorch.org/blog/how-to-train-state-of-the-art-models-using-torchvision-latest-primitives/#the-training-recipe)。*

## 本节将涵盖内容

本节核心思想是：**把有价值的 notebook 代码单元转换为可复用的 Python 文件。**

这样可以避免反复书写同样代码。

本节包含两个 notebook：

1. [**05. Going Modular: Part 1 (cell mode)**](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/going_modular/05_pytorch_going_modular_cell_mode.ipynb) - 以传统 Jupyter/Colab 方式运行，是 [notebook 04](https://www.learnpytorch.io/04_pytorch_custom_datasets/) 的精简版本。
2. [**05. Going Modular: Part 2 (script mode)**](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/going_modular/05_pytorch_going_modular_script_mode.ipynb) - 与 Part 1 基本一致，但增加了将主要模块写入 Python 脚本的能力，例如 `data_setup.py` 和 `train.py`。

本文档聚焦 05 的 Part 2（script mode）中那些顶部带有 `%%writefile ...` 的代码单元。

### 为什么分成两部分？

因为很多时候，理解“差异”是学习最快的方式。

把两个 notebook 并排运行，你会清楚看到它们的不同，而关键学习点就藏在这些差异里。

<img src="https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/05-notebook-cell-mode-vs-script-mode.png" alt="单元模式 notebook 与脚本模式 notebook 的运行对比" width=1000/>

*把第 05 节两个 notebook 并排运行。你会发现 **script mode notebook 额外多了一些代码单元**，用于把 cell mode 中的代码转换成 Python 脚本。*

### 本节目标

完成本节后，我们希望达成两件事：

1. 能通过一行命令在终端训练 notebook 04（Food Vision Mini）中的模型：`python train.py`。
2. 建立一套可复用的 Python 脚本目录结构，例如：

```
going_modular/
├── going_modular/
│   ├── data_setup.py
│   ├── engine.py
│   ├── model_builder.py
│   ├── train.py
│   └── utils.py
├── models/
│   ├── 05_going_modular_cell_mode_tinyvgg_model.pth
│   └── 05_going_modular_script_mode_tinyvgg_model.pth
└── data/
    └── pizza_steak_sushi/
        ├── train/
        │   ├── pizza/
        │   │   ├── image01.jpeg
        │   │   └── ...
        │   ├── steak/
        │   └── sushi/
        └── test/
            ├── pizza/
            ├── steak/
            └── sushi/
```

### 注意事项

* **Docstring** - 可复现且易理解的代码非常重要，因此我们写入脚本的函数/类都尽量遵循 Google 的 [Python docstring style](https://google.github.io/styleguide/pyguide.html#383-functions-and-methods)。
* **脚本顶部导入** - 由于这些 Python 脚本都可看作一个小程序，通常应在文件开头完成依赖导入，例如：

```python
# 导入 train.py 所需模块
import os
import torch
import data_setup, engine, model_builder, utils

from torchvision import transforms
```

## 去哪里获得帮助？

本课程所有材料都可在 [GitHub](https://github.com/mrdbourke/pytorch-deep-learning) 获取。

遇到问题时，可以到课程的 [GitHub Discussions 页面](https://github.com/mrdbourke/pytorch-deep-learning/discussions) 提问。

此外，[PyTorch documentation](https://pytorch.org/docs/stable/index.html) 与 [PyTorch developer forums](https://discuss.pytorch.org/) 也非常值得参考。

## 0. Cell mode 与 script mode

像 [05. Going Modular Part 1 (cell mode)](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/going_modular/05_pytorch_going_modular_cell_mode.ipynb) 这样的 cell mode notebook，就是常规运行的 notebook，每个单元是代码或 markdown。

像 [05. Going Modular Part 2 (script mode)](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/going_modular/05_pytorch_going_modular_script_mode.ipynb) 这样的 script mode notebook 与之类似，但其中很多代码单元会被写出为 Python 脚本。

> **注意：** 你并不一定要通过 notebook 创建 Python 脚本，也可以直接在 [VS Code](https://code.visualstudio.com/) 这类 IDE 中创建。这里展示 script mode notebook，只是为了演示从 notebook 走向脚本化的一种路径。

## 1. 获取数据

05 章两个 notebook 的数据获取方式与 [notebook 04](https://www.learnpytorch.io/04_pytorch_custom_datasets/#1-get-data) 一致。

通过 Python 的 `requests` 模块从 GitHub 下载 `.zip` 文件并解压。

```python 
import os
import requests
import zipfile
from pathlib import Path

# 设置数据目录路径
data_path = Path("data/")
image_path = data_path / "pizza_steak_sushi"

# 如果图像目录不存在，则下载并准备数据
if image_path.is_dir():
    print(f"{image_path} directory exists.")
else:
    print(f"Did not find {image_path} directory, creating one...")
    image_path.mkdir(parents=True, exist_ok=True)
    
# 下载 pizza、steak、sushi 数据
with open(data_path / "pizza_steak_sushi.zip", "wb") as f:
    request = requests.get("https://github.com/mrdbourke/pytorch-deep-learning/raw/main/data/pizza_steak_sushi.zip")
    print("Downloading pizza, steak, sushi data...")
    f.write(request.content)

# 解压 pizza、steak、sushi 数据
with zipfile.ZipFile(data_path / "pizza_steak_sushi.zip", "r") as zip_ref:
    print("Unzipping pizza, steak, sushi data...") 
    zip_ref.extractall(image_path)

# 删除 zip 文件
os.remove(data_path / "pizza_steak_sushi.zip")
```

执行后会在 `data` 目录下得到 `pizza_steak_sushi` 子目录，其中包含按标准图像分类格式组织的 pizza、steak、sushi 图片。

```
data/
└── pizza_steak_sushi/
    ├── train/
    │   ├── pizza/
    │   │   ├── train_image01.jpeg
    │   │   ├── test_image02.jpeg
    │   │   └── ...
    │   ├── steak/
    │   │   └── ...
    │   └── sushi/
    │       └── ...
    └── test/
        ├── pizza/
        │   ├── test_image01.jpeg
        │   └── test_image02.jpeg
        ├── steak/
        └── sushi/
```

## 2. 创建 Dataset 与 DataLoader（`data_setup.py`）

有了数据后，就可以把它转成 PyTorch `Dataset` 和 `DataLoader`（训练集一个、测试集一个）。

我们把相关代码封装为 `create_dataloaders()` 函数。

然后通过 `%%writefile going_modular/data_setup.py` 写入脚本文件。

```py title="data_setup.py"
%%writefile going_modular/data_setup.py
"""
包含创建图像分类 PyTorch DataLoader 的功能。
"""
import os

from torchvision import datasets, transforms
from torch.utils.data import DataLoader

NUM_WORKERS = os.cpu_count()

def create_dataloaders(
    train_dir: str, 
    test_dir: str, 
    transform: transforms.Compose, 
    batch_size: int, 
    num_workers: int=NUM_WORKERS
):
  """创建训练与测试 DataLoader。

  接收训练与测试目录路径，
  先构建 PyTorch Dataset，再构建 PyTorch DataLoader。

  Args:
    train_dir: 训练目录路径。
    test_dir: 测试目录路径。
    transform: 训练/测试数据所用的 torchvision 变换。
    batch_size: 每个 DataLoader 中每个 batch 的样本数。
    num_workers: 每个 DataLoader 使用的 worker 数。

  Returns:
    返回 (train_dataloader, test_dataloader, class_names) 元组。
    其中 class_names 是目标类别名称列表。
    使用示例：
      train_dataloader, test_dataloader, class_names = \
        = create_dataloaders(train_dir=path/to/train_dir,
                             test_dir=path/to/test_dir,
                             transform=some_transform,
                             batch_size=32,
                             num_workers=4)
  """
  # 使用 ImageFolder 创建数据集
  train_data = datasets.ImageFolder(train_dir, transform=transform)
  test_data = datasets.ImageFolder(test_dir, transform=transform)

  # 获取类别名称
  class_names = train_data.classes

  # 将图像数据转换为 DataLoader
  train_dataloader = DataLoader(
      train_data,
      batch_size=batch_size,
      shuffle=True,
      num_workers=num_workers,
      pin_memory=True,
  )
  test_dataloader = DataLoader(
      test_data,
      batch_size=batch_size,
      shuffle=False, # 测试集通常不需要打乱
      num_workers=num_workers,
      pin_memory=True,
  )

  return train_dataloader, test_dataloader, class_names
```

现在如果我们想创建 `DataLoader`，可以直接调用 `data_setup.py` 里的函数：

```python
# 导入 data_setup.py
from going_modular import data_setup

# 创建训练/测试 dataloader，并获得类别名列表
train_dataloader, test_dataloader, class_names = data_setup.create_dataloaders(...)
```

## 3. 构建模型（`model_builder.py`）

在前面几个 notebook（03 和 04）中，我们已经多次手写 TinyVGG。

因此，把模型放到独立文件里更合理，便于反复复用。

下面通过 `%%writefile going_modular/model_builder.py` 将 `TinyVGG()` 模型类写入脚本：

```python title="model_builder.py"
%%writefile going_modular/model_builder.py
"""
包含用于实例化 TinyVGG 的 PyTorch 模型代码。
"""
import torch
from torch import nn 

class TinyVGG(nn.Module):
  """创建 TinyVGG 网络结构。

  在 PyTorch 中复现 CNN Explainer 网站上的 TinyVGG 结构。
  原始结构见：https://poloclub.github.io/cnn-explainer/
  
  Args:
    input_shape: 输入通道数。
    hidden_units: 层间隐藏单元数。
    output_shape: 输出单元数。
  """
  def __init__(self, input_shape: int, hidden_units: int, output_shape: int) -> None:
      super().__init__()
      self.conv_block_1 = nn.Sequential(
          nn.Conv2d(in_channels=input_shape, 
                    out_channels=hidden_units, 
                    kernel_size=3, 
                    stride=1, 
                    padding=0),  
          nn.ReLU(),
          nn.Conv2d(in_channels=hidden_units, 
                    out_channels=hidden_units,
                    kernel_size=3,
                    stride=1,
                    padding=0),
          nn.ReLU(),
          nn.MaxPool2d(kernel_size=2,
                        stride=2)
      )
      self.conv_block_2 = nn.Sequential(
          nn.Conv2d(hidden_units, hidden_units, kernel_size=3, padding=0),
          nn.ReLU(),
          nn.Conv2d(hidden_units, hidden_units, kernel_size=3, padding=0),
          nn.ReLU(),
          nn.MaxPool2d(2)
      )
      self.classifier = nn.Sequential(
          nn.Flatten(),
          # in_features 的形状从哪里来？
          # 因为网络每一层都会压缩并改变输入数据的形状。
          nn.Linear(in_features=hidden_units*13*13,
                    out_features=output_shape)
      )
    
  def forward(self, x: torch.Tensor):
      x = self.conv_block_1(x)
      x = self.conv_block_2(x)
      x = self.classifier(x)
      return x
      # return self.classifier(self.conv_block_2(self.conv_block_1(x))) # <- 利用 operator fusion 带来的优势
```

    现在我们就不必每次都从零写 TinyVGG，可以直接导入：

```python
import torch
# 导入 model_builder.py
from going_modular import model_builder
device = "cuda" if torch.cuda.is_available() else "cpu"

# 基于 model_builder.py 实例化模型
torch.manual_seed(42)
model = model_builder.TinyVGG(input_shape=3,
                              hidden_units=10, 
                              output_shape=len(class_names)).to(device)
```

## 4. 创建 `train_step()`、`test_step()` 以及整合函数 `train()`

我们在 [notebook 04](https://www.learnpytorch.io/04_pytorch_custom_datasets/#75-create-train-test-loop-functions) 里写过几个训练函数：

1. `train_step()` - 接收模型、`DataLoader`、损失函数和优化器，在该 `DataLoader` 上训练模型。
2. `test_step()` - 接收模型、`DataLoader` 和损失函数，在该 `DataLoader` 上评估模型。
3. `train()` - 在给定 epoch 数下组合执行前两者，并返回结果字典。

这些函数就是训练流程的“引擎”，适合统一放进 `engine.py`，通过 `%%writefile going_modular/engine.py` 写入：

```python title="engine.py"
%%writefile going_modular/engine.py
"""
包含训练与测试 PyTorch 模型的函数。
"""
import torch

from tqdm.auto import tqdm
from typing import Dict, List, Tuple

def train_step(model: torch.nn.Module, 
               dataloader: torch.utils.data.DataLoader, 
               loss_fn: torch.nn.Module, 
               optimizer: torch.optim.Optimizer,
               device: torch.device) -> Tuple[float, float]:
  """训练 PyTorch 模型一个 epoch。

  将目标模型切换为训练模式，并执行训练所需步骤
  （前向传播、损失计算、优化器更新）。

  Args:
    model: 待训练的 PyTorch 模型。
    dataloader: 训练数据 DataLoader。
    loss_fn: 需要最小化的损失函数。
    optimizer: 用于最小化损失的优化器。
    device: 计算设备（如 "cuda" 或 "cpu"）。

  Returns:
    返回训练损失和训练准确率元组。
    形式为 (train_loss, train_accuracy)，例如：
    
    (0.1112, 0.8743)
  """
  # 切换到训练模式
  model.train()
  
  # 初始化训练损失与准确率
  train_loss, train_acc = 0, 0
  
  # 遍历 DataLoader 的每个 batch
  for batch, (X, y) in enumerate(dataloader):
      # 将数据发送到目标设备
      X, y = X.to(device), y.to(device)

      # 1. 前向传播
      y_pred = model(X)

      # 2. 计算并累计损失
      loss = loss_fn(y_pred, y)
      train_loss += loss.item() 

      # 3. 优化器梯度清零
      optimizer.zero_grad()

      # 4. 反向传播
      loss.backward()

      # 5. 优化器更新
      optimizer.step()

      # 计算并累计所有 batch 的准确率
      y_pred_class = torch.argmax(torch.softmax(y_pred, dim=1), dim=1)
      train_acc += (y_pred_class == y).sum().item()/len(y_pred)

  # 计算每个 batch 的平均损失与准确率
  train_loss = train_loss / len(dataloader)
  train_acc = train_acc / len(dataloader)
  return train_loss, train_acc

def test_step(model: torch.nn.Module, 
              dataloader: torch.utils.data.DataLoader, 
              loss_fn: torch.nn.Module,
              device: torch.device) -> Tuple[float, float]:
  """测试 PyTorch 模型一个 epoch。

  将目标模型切换为评估模式，并在测试数据上执行前向传播。

  Args:
    model: 待测试的 PyTorch 模型。
    dataloader: 测试数据 DataLoader。
    loss_fn: 用于计算测试损失的损失函数。
    device: 计算设备（如 "cuda" 或 "cpu"）。

  Returns:
    返回测试损失和测试准确率元组。
    形式为 (test_loss, test_accuracy)，例如：
    
    (0.0223, 0.8985)
  """
  # 切换到评估模式
  model.eval() 
  
  # 初始化测试损失与准确率
  test_loss, test_acc = 0, 0
  
  # 开启推理上下文
  with torch.inference_mode():
      # 遍历 DataLoader 的每个 batch
      for batch, (X, y) in enumerate(dataloader):
          # 将数据发送到目标设备
          X, y = X.to(device), y.to(device)
  
          # 1. 前向传播
          test_pred_logits = model(X)

          # 2. 计算并累计损失
          loss = loss_fn(test_pred_logits, y)
          test_loss += loss.item()
          
          # 计算并累计准确率
          test_pred_labels = test_pred_logits.argmax(dim=1)
          test_acc += ((test_pred_labels == y).sum().item()/len(test_pred_labels))
          
  # 计算每个 batch 的平均损失与准确率
  test_loss = test_loss / len(dataloader)
  test_acc = test_acc / len(dataloader)
  return test_loss, test_acc

def train(model: torch.nn.Module, 
          train_dataloader: torch.utils.data.DataLoader, 
          test_dataloader: torch.utils.data.DataLoader, 
          optimizer: torch.optim.Optimizer,
          loss_fn: torch.nn.Module,
          epochs: int,
          device: torch.device) -> Dict[str, List]:
  """训练并测试 PyTorch 模型。

  在多个 epoch 中循环调用 train_step() 与 test_step()，
  在同一训练循环里完成训练和测试。

  持续计算、打印并保存评估指标。

  Args:
    model: 需要训练和测试的 PyTorch 模型。
    train_dataloader: 训练数据 DataLoader。
    test_dataloader: 测试数据 DataLoader。
    optimizer: 用于最小化损失的优化器。
    loss_fn: 在训练集和测试集上计算损失的函数。
    epochs: 训练 epoch 数。
    device: 计算设备（如 "cuda" 或 "cpu"）。

  Returns:
    返回包含训练/测试损失与训练/测试准确率的字典，
    每个指标都按 epoch 存储在列表中。
    形式为：{train_loss: [...],
                  train_acc: [...],
                  test_loss: [...],
                  test_acc: [...]} 
    例如 epochs=2 时：
                 {train_loss: [2.0616, 1.0537],
                  train_acc: [0.3945, 0.3945],
                  test_loss: [1.2641, 1.5706],
                  test_acc: [0.3400, 0.2973]} 
  """
  # 创建空结果字典
  results = {"train_loss": [],
      "train_acc": [],
      "test_loss": [],
      "test_acc": []
  }
  
  # 按 epoch 循环执行训练与测试
  for epoch in tqdm(range(epochs)):
      train_loss, train_acc = train_step(model=model,
                                          dataloader=train_dataloader,
                                          loss_fn=loss_fn,
                                          optimizer=optimizer,
                                          device=device)
      test_loss, test_acc = test_step(model=model,
          dataloader=test_dataloader,
          loss_fn=loss_fn,
          device=device)
      
      # 打印训练进度
      print(
          f"Epoch: {epoch+1} | "
          f"train_loss: {train_loss:.4f} | "
          f"train_acc: {train_acc:.4f} | "
          f"test_loss: {test_loss:.4f} | "
          f"test_acc: {test_acc:.4f}"
      )

      # 更新结果字典
      results["train_loss"].append(train_loss)
      results["train_acc"].append(train_acc)
      results["test_loss"].append(test_loss)
      results["test_acc"].append(test_acc)

  # 在所有 epoch 结束后返回结果
  return results
```

现在有了 `engine.py`，我们可以这样导入并调用：

```python
# 导入 engine.py
from going_modular import engine

# 通过 engine.py 调用 train()
engine.train(...)
```

## 5. 创建模型保存函数（`utils.py`）

很多场景下，你会希望在训练过程中或训练完成后保存模型。

既然我们在前面 notebook 已多次写过保存代码，把它封装成函数并存文件更合理。

通常会把这类辅助函数放在 `utils.py`（utilities 的缩写）中。

下面通过 `%%writefile going_modular/utils.py` 将 `save_model()` 写入 `utils.py`：

```python title="utils.py"
%%writefile going_modular/utils.py
"""
包含用于 PyTorch 训练与模型保存的工具函数。
"""
import torch
from pathlib import Path

def save_model(model: torch.nn.Module,
               target_dir: str,
               model_name: str):
  """将 PyTorch 模型保存到目标目录。

  Args:
    model: 要保存的目标模型。
    target_dir: 保存目录。
    model_name: 模型文件名，扩展名需为 ".pth" 或 ".pt"。
  
  Example usage:
    save_model(model=model_0,
               target_dir="models",
               model_name="05_going_modular_tingvgg_model.pth")
  """
  # 创建目标目录
  target_dir_path = Path(target_dir)
  target_dir_path.mkdir(parents=True,
                        exist_ok=True)
  
  # 创建模型保存路径
  assert model_name.endswith(".pth") or model_name.endswith(".pt"), "model_name should end with '.pt' or '.pth'"
  model_save_path = target_dir_path / model_name

  # 保存模型 state_dict()
  print(f"[INFO] Saving model to: {model_save_path}")
  torch.save(obj=model.state_dict(),
             f=model_save_path)
```

现在如果要使用 `save_model()`，就不必重复手写，直接导入调用：

```python
# 导入 utils.py
from going_modular import utils

# 保存模型到文件
save_model(model=...
           target_dir=...,
           model_name=...)
```

## 6. 训练、评估并保存模型（`train.py`）

正如前文所说，你经常会看到 PyTorch 仓库把核心流程整合到 `train.py`。

这个文件本质上就是在说：“用当前可用数据来训练模型”。

在我们的 `train.py` 中，会组合前面所有脚本功能并执行完整训练流程。

这样我们就可以通过一行命令训练模型：

```
python train.py
```

创建 `train.py` 的步骤如下：

1. 导入依赖：`torch`、`os`、`torchvision.transforms`，以及 `going_modular` 目录中的脚本 `data_setup`、`engine`、`model_builder`、`utils`。
  * **注意：** 由于 `train.py` 位于 `going_modular` 目录内部，可直接用 `import ...`，不必写 `from going_modular import ...`。
2. 设置超参数：batch size、epoch 数、学习率、隐藏单元数（后续可用 [Python 的 `argparse`](https://docs.python.org/3/library/argparse.html) 从命令行传入）。
3. 设置训练与测试目录。
4. 编写设备无关代码。
5. 创建数据变换。
6. 使用 `data_setup.py` 创建 DataLoader。
7. 使用 `model_builder.py` 创建模型。
8. 设置损失函数与优化器。
9. 使用 `engine.py` 训练模型。
10. 使用 `utils.py` 保存模型。

我们可以在 notebook 单元里通过 `%%writefile going_modular/train.py` 创建该文件：

```python title="train.py"
%%writefile going_modular/train.py
"""
使用设备无关代码训练 PyTorch 图像分类模型。
"""

import os
import torch
import data_setup, engine, model_builder, utils

from torchvision import transforms

# 设置超参数
NUM_EPOCHS = 5
BATCH_SIZE = 32
HIDDEN_UNITS = 10
LEARNING_RATE = 0.001

# 设置目录
train_dir = "data/pizza_steak_sushi/train"
test_dir = "data/pizza_steak_sushi/test"

# 设置目标设备
device = "cuda" if torch.cuda.is_available() else "cpu"

# 创建数据变换
data_transform = transforms.Compose([
  transforms.Resize((64, 64)),
  transforms.ToTensor()
])

# 借助 data_setup.py 创建 DataLoader
train_dataloader, test_dataloader, class_names = data_setup.create_dataloaders(
    train_dir=train_dir,
    test_dir=test_dir,
    transform=data_transform,
    batch_size=BATCH_SIZE
)

# 借助 model_builder.py 创建模型
model = model_builder.TinyVGG(
    input_shape=3,
    hidden_units=HIDDEN_UNITS,
    output_shape=len(class_names)
).to(device)

# 设置损失函数与优化器
loss_fn = torch.nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model.parameters(),
                             lr=LEARNING_RATE)

# 借助 engine.py 启动训练
engine.train(model=model,
             train_dataloader=train_dataloader,
             test_dataloader=test_dataloader,
             loss_fn=loss_fn,
             optimizer=optimizer,
             epochs=NUM_EPOCHS,
             device=device)

# 借助 utils.py 保存模型
utils.save_model(model=model,
                 target_dir="models",
                 model_name="05_going_modular_script_mode_tinyvgg_model.pth")
```

太好了！

现在我们可以通过下面这行命令训练 PyTorch 模型：

```
python train.py
```

这会自动串联并调用我们之前创建的所有脚本。

如果需要，我们还可以在 `train.py` 中接入 Python 的 `argparse` 参数解析，以支持像前面讨论那样传入不同超参数：

```
python train.py --model MODEL_NAME --batch_size BATCH_SIZE --lr LEARNING_RATE --num_epochs NUM_EPOCHS
```

## 练习

**资源：**

* [05 章练习模板 notebook](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/extras/exercises/05_pytorch_going_modular_exercise_template.ipynb)
* [05 章示例答案 notebook](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/extras/solutions/05_pytorch_going_modular_exercise_solutions.ipynb)
  * [YouTube 上的 05 章答案实战讲解](https://youtu.be/ijgFhMK3pp4)

**练习题：**

1. 将“获取数据”（上方第 1 节）的代码写成独立 Python 脚本，例如 `get_data.py`。
  * 当你运行 `python get_data.py` 时，应先检查数据是否已存在；若存在则跳过下载。
  * 若下载成功，你应能从 `data` 目录访问 `pizza_steak_sushi` 图像数据。
2. 使用 [Python 的 `argparse` 模块](https://docs.python.org/3/library/argparse.html)，让 `train.py` 支持从命令行传入自定义超参数。
  * 添加参数以支持修改：
    * 训练/测试目录
    * 学习率
    * Batch size
    * 训练 epoch 数
    * TinyVGG 的隐藏单元数
  * 上述参数默认值应保持与 notebook 05 一致。
  * 例如，你应能运行类似以下命令，以学习率 0.003、batch size 64 训练 20 个 epoch：`python train.py --learning_rate 0.003 --batch_size 64 --num_epochs 20`。
  * **注意：** `train.py` 依赖第 05 节中创建的其他脚本（如 `model_builder.py`、`utils.py`、`engine.py`），请确保它们可用。可在课程 GitHub 的 [`going_modular` 目录](https://github.com/mrdbourke/pytorch-deep-learning/tree/main/going_modular/going_modular) 获取。
3. 编写预测脚本（例如 `predict.py`），输入图像路径并结合已保存模型完成预测。
  * 例如，运行 `python predict.py some_image.jpeg` 时，应由训练好的 PyTorch 模型输出预测结果。
  * 可参考 [notebook 04 中“自定义图像预测函数”部分](https://www.learnpytorch.io/04_pytorch_custom_datasets/#113-putting-custom-image-prediction-together-building-a-function)。
  * 你可能还需要补充加载已训练模型的代码。

## 课外拓展

* 想进一步了解 Python 项目结构，可阅读 Real Python 的 [Python Application Layouts](https://realpython.com/python-application-layouts/)。
* 想改进 PyTorch 代码风格，可参考 [Igor Susmelj 的 PyTorch style guide](https://github.com/IgorSusmelj/pytorch-styleguide#recommended-code-structure-for-training-your-model)（本章风格也参考了该指南及类似仓库）。
* 想查看官方团队的 `train.py` 与其他训练脚本示例，可参考 PyTorch 视觉库的 [`classification` GitHub 仓库](https://github.com/pytorch/vision/tree/main/references/classification)。
