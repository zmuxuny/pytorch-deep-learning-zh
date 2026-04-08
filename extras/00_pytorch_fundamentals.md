<a href="https://colab.research.google.com/github/mrdbourke/pytorch-deep-learning/blob/main/00_pytorch_fundamentals.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a> 

[View Source Code](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/00_pytorch_fundamentals.ipynb) | [View Slides](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/slides/00_pytorch_and_deep_learning_fundamentals.pdf) | [Watch Video Walkthrough](https://youtu.be/Z_ikDlimN6A?t=76) 

# 00. PyTorch 基础

## 什么是 PyTorch？

[PyTorch](https://pytorch.org/) 是一个开源的机器学习与深度学习框架。

## PyTorch 可以用来做什么？

PyTorch 让你可以用 Python 操作和处理数据，并实现机器学习算法。

## 谁在使用 PyTorch？

全球很多顶级科技公司都在使用 PyTorch，例如 [Meta (Facebook)](https://ai.facebook.com/blog/pytorch-builds-the-future-of-ai-and-machine-learning-at-facebook/)、Tesla、Microsoft，以及像 [OpenAI](https://openai.com/blog/openai-pytorch/) 这样的 AI 研究机构，都用它推动研究并将机器学习落地到产品中。

![pytorch being used across industry and research](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/00-pytorch-being-used-across-research-and-industry.png)

例如，Tesla 的 AI 负责人 Andrej Karpathy 在多个演讲中（[PyTorch DevCon 2019](https://youtu.be/oBklltKXtDE)、[Tesla AI Day 2021](https://youtu.be/j0z4FweCy4M?t=2904)）分享过 Tesla 如何用 PyTorch 驱动自动驾驶视觉模型。

PyTorch 也在农业等行业中落地，例如用于 [拖拉机上的计算机视觉系统](https://medium.com/pytorch/ai-for-ag-production-machine-learning-for-agriculture-e8cfdb9849a1)。

## 为什么使用 PyTorch？

机器学习研究者非常偏爱 PyTorch。截止 2022 年 2 月，PyTorch 是 [Papers With Code 上使用最广的深度学习框架](https://paperswithcode.com/trends)（Papers With Code 是一个追踪研究论文及其代码仓库的网站）。

PyTorch 还在底层帮你处理了很多事情，例如 GPU 加速（让代码运行更快）。

因此你可以更专注在数据处理与算法实现，性能层面的很多工作交给 PyTorch。

再考虑到 Tesla、Meta（Facebook）等公司用它构建并部署模型，服务海量应用、车辆与用户，也说明它在工程与生产层面同样很可靠。

## 本章将涵盖什么

本课程由多个章节（notebook）组成。

每个 notebook 都聚焦 PyTorch 中的重要概念与实践。

后续章节会建立在前一章基础上（编号从 00、01、02 持续递进）。

本 notebook 讲解机器学习与深度学习最基础的构件：张量（tensor）。

具体会覆盖以下内容：

| **主题**                      | **内容**                                                                                                                                                                                                          |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **张量入门**                  | 张量是整个机器学习与深度学习的基础构建块。                                                                                                                                                                        |
| **创建张量**                  | 张量可以表示几乎任何类型的数据（图像、文本、数值表格等）。                                                                                                                                                        |
| **从张量中获取信息**          | 既然信息可以放进张量，就要学会把信息取出来。                                                                                                                                                                      |
| **张量操作**                  | 机器学习算法（如神经网络）会大量进行加法、乘法、拼接等张量运算。                                                                                                                                                  |
| **处理张量形状**              | 机器学习中最常见的问题之一是形状不匹配（把不兼容形状的张量混用）。                                                                                                                                                |
| **张量索引**                  | 如果你用过 Python 列表或 NumPy 数组索引，张量很类似，只是维度往往更多。                                                                                                                                           |
| **PyTorch 张量与 NumPy 混用** | PyTorch 使用张量（[`torch.Tensor`](https://pytorch.org/docs/stable/tensors.html)），NumPy 使用数组（[`np.ndarray`](https://numpy.org/doc/stable/reference/generated/numpy.ndarray.html)），实际项目中常需要互转。 |
| **可复现性**                  | 机器学习依赖大量随机性，因此很多时候你会希望“随机”变得可控。                                                                                                                                                      |
| **在 GPU 上运行张量**         | GPU（图形处理器）能显著加速代码，PyTorch 让 GPU 运行变得简单。                                                                                                                                                    |

## 遇到问题去哪里求助？

本课程所有材料都在 [GitHub](https://github.com/mrdbourke/pytorch-deep-learning) 上。

如果你遇到问题，也可以在仓库的 [Discussions 页面](https://github.com/mrdbourke/pytorch-deep-learning/discussions) 提问。

另外还有 [PyTorch 开发者论坛](https://discuss.pytorch.org/)，这是获取 PyTorch 相关帮助的优质社区。

## 导入 PyTorch

> **注意：** 在运行本 notebook 任何代码前，你应先完成 [PyTorch 安装配置步骤](https://pytorch.org/get-started/locally/)。
>
> 但如果你使用 **Google Colab**，一般可直接运行（Colab 已预装 PyTorch 与常用库）。

先导入 PyTorch，并查看当前版本。


```python
import torch
torch.__version__
```




    '1.13.1'



很好，看起来我们当前是 PyTorch 1.10.0+。

这意味着课程材料通常与 PyTorch 1.10.0+ 兼容；如果你本地版本明显更高，可能会遇到少量不一致。

如果遇到问题，请到课程的 [GitHub Discussions 页面](https://github.com/mrdbourke/pytorch-deep-learning/discussions) 反馈。

## 张量入门

现在 PyTorch 已导入，接下来学习张量。

张量是机器学习中的核心基础构件。

它的作用是以数值形式表示数据。

例如，一张图像可表示为形状 `[3, 224, 224]` 的张量，对应 `[colour_channels, height, width]`：即图像有 `3` 个颜色通道（红、绿、蓝），高度 `224` 像素，宽度 `224` 像素。

![example of going from an input image to a tensor representation of the image, image gets broken down into 3 colour channels as well as numbers to represent the height and width](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/00-tensor-shape-example-of-image.png)

在张量术语中，这个张量有三个维度，分别对应 `colour_channels`、`height` 与 `width`。

不过先别着急。

我们通过实际编码来继续理解张量。


### 创建张量

PyTorch 的核心就是张量，官方甚至专门为 [`torch.Tensor`](https://pytorch.org/docs/stable/tensors.html) 类准备了完整文档页面。

你的第一个小作业是花 10 分钟浏览 [`torch.Tensor` 文档](https://pytorch.org/docs/stable/tensors.html)。当然可以稍后再做。

先上代码。

我们先创建一个 **scalar（标量）**。

标量就是单个数字，在张量语境里是 0 维张量。

> **注意：** 这也是本课程的一贯风格。我们会大量实操代码，同时也会安排你阅读 PyTorch 文档来熟悉官方资料。课程结束后你一定还会继续深入，而文档会是你最常访问的学习资源之一。


```python
# Scalar
scalar = torch.tensor(7)
scalar
```




    tensor(7)



看到上面输出了 `tensor(7)` 吗？

这说明 `scalar` 虽然是一个数字，但它的数据类型依然是 `torch.Tensor`。

我们可以通过 `ndim` 属性查看张量维度数。


```python
scalar.ndim
```




    0



如果我们想把张量里的数字取出来呢？

也就是把它从 `torch.Tensor` 转成 Python 整数？

可以使用 `item()` 方法。


```python
# Get the Python number within a tensor (only works with one-element tensors)
scalar.item()
```




    7



接下来看看 **vector（向量）**。

向量是 1 维张量，但可以包含多个数字。

比如你可以用 `[3, 2]` 表示房子的 `[bedrooms, bathrooms]`，也可以用 `[3, 2, 2]` 表示 `[bedrooms, bathrooms, car_parks]`。

关键点是：向量（以及更一般的张量）对“表示什么数据”非常灵活。


```python
# Vector
vector = torch.tensor([7, 7])
vector
```




    tensor([7, 7])



很好，`vector` 现在包含两个 7（我最喜欢的数字）。

你觉得它有几维？


```python
# Check the number of dimensions of vector
vector.ndim
```




    1



看起来有点反直觉：`vector` 里有两个数，但只有 1 个维度。

这里有个小技巧。

在 PyTorch 里，你可以通过最外层方括号（`[`) 的层数来判断张量维度，只看一侧即可。

`vector` 最外层有几层方括号？

张量另一个重要概念是 `shape` 属性，它告诉你内部元素是如何组织的。

我们来看下 `vector` 的形状。


```python
# Check shape of vector
vector.shape
```




    torch.Size([2])



上面返回 `torch.Size([2])`，表示向量形状为 `[2]`。原因很直接：我们在方括号里放了两个元素（`[7, 7]`）。

接下来看看 **matrix（矩阵）**。


```python
# Matrix
MATRIX = torch.tensor([[7, 8], 
                       [9, 10]])
MATRIX
```




    tensor([[ 7,  8],
            [ 9, 10]])



数字更多了。矩阵和向量一样灵活，只是它多了一个维度。




```python
# Check number of dimensions
MATRIX.ndim
```




    2



`MATRIX` 有两个维度（你有数最外层方括号的层数吗？）。

你觉得它的 `shape` 会是什么？


```python
MATRIX.shape
```




    torch.Size([2, 2])



输出是 `torch.Size([2, 2])`，因为 `MATRIX` 的“深度”为 2，“宽度”也为 2。

接着创建一个 **tensor（张量）** 怎么样？


```python
# Tensor
TENSOR = torch.tensor([[[1, 2, 3],
                        [3, 6, 9],
                        [2, 4, 5]]])
TENSOR
```




    tensor([[[1, 2, 3],
             [3, 6, 9],
             [2, 4, 5]]])



这个张量看起来很不错。

我想强调：张量几乎可以表示任何类型的数据。

我们刚创建的这个张量，甚至可以表示一家牛排和杏仁酱商店的销售数据（这两样都是我爱吃的）。

![a simple tensor in google sheets showing day of week, steak sales and almond butter sales](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/00_simple_tensor.png)

你觉得它有几维？（提示：继续用“数方括号”技巧）


```python
# Check number of dimensions for TENSOR
TENSOR.ndim
```




    3



那它的形状呢？


```python
# Check shape of TENSOR
TENSOR.shape
```




    torch.Size([1, 3, 3])



可以看到，输出为 `torch.Size([1, 3, 3])`。

维度顺序是从外到内。

也就是：有 1 组 `3 x 3` 的数据。

![example of different tensor dimensions](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/00-pytorch-different-tensor-dimensions.png)

> **注意：** 你可能发现我给 `scalar`、`vector` 用小写命名，而 `MATRIX`、`TENSOR` 用大写命名，这是有意为之。实际中，标量和向量常用小写字母表示（如 `y`、`a`），矩阵和张量常用大写字母表示（如 `X`、`W`）。
>
> 你也会看到 matrix 与 tensor 在一些语境下被交替使用，这是常见现象。因为在 PyTorch 中我们统一使用 `torch.Tensor`，但具体是“标量/向量/矩阵/高维张量”，取决于内部数据的形状与维度。

做个小结。

| 名称               | 它是什么                                         | 维度数量                               | 常见记号（小写/大写） |
| ------------------ | ------------------------------------------------ | -------------------------------------- | --------------------- |
| **scalar（标量）** | 单个数值                                         | 0                                      | 小写（如 `a`）        |
| **vector（向量）** | 具有方向的一组数（如带方向的风速）或一般一维数列 | 1                                      | 小写（如 `y`）        |
| **matrix（矩阵）** | 二维数值数组                                     | 2                                      | 大写（如 `Q`）        |
| **tensor（张量）** | n 维数值数组                                     | 任意维；0 维张量是标量，1 维张量是向量 | 大写（如 `X`）        |

![scalar vector matrix tensor and what they look like](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/00-scalar-vector-matrix-tensor.png)

### 随机张量

前面我们已经知道，张量用于表示数据。

而像神经网络这样的机器学习模型，会在张量上做运算并寻找模式。

但在真实建模里，你很少会像前面那样手动逐个写张量。

更常见的是：模型以随机初始化的大张量开始，随后在训练中不断调整这些数值，使其更好地表示数据模式。

本质上就是：

`随机初始化 -> 观察数据 -> 更新参数 -> 再观察数据 -> 再更新参数...`

作为数据科学实践者，你可以决定模型如何初始化、如何表示数据、如何优化更新。

这些步骤我们后面都会实操。

现在先看如何创建随机张量。

可以使用 [`torch.rand()`](https://pytorch.org/docs/stable/generated/torch.rand.html)，并通过 `size` 指定形状。


```python
# Create a random tensor of size (3, 4)
random_tensor = torch.rand(size=(3, 4))
random_tensor, random_tensor.dtype
```




    (tensor([[0.9900, 0.1882, 0.1744, 0.7445],
             [0.9445, 0.7044, 0.7024, 0.7877],
             [0.0218, 0.7861, 0.9037, 0.9690]]),
     torch.float32)



`torch.rand()` 的优势在于 `size` 非常灵活，想要什么形状都可以。

例如，你可以创建图像常见形状 `[224, 224, 3]` 的随机张量（`[height, width, color_channels]`）。


```python
# Create a random tensor of size (224, 224, 3)
random_image_size_tensor = torch.rand(size=(224, 224, 3))
random_image_size_tensor.shape, random_image_size_tensor.ndim
```




    (torch.Size([224, 224, 3]), 3)



### 全 0 与全 1 张量

有时候你只需要全 0 或全 1 的张量。

这种场景在掩码（masking）中很常见，比如把某些位置置 0，告诉模型这些位置不要学习。

用 [`torch.zeros()`](https://pytorch.org/docs/stable/generated/torch.zeros.html) 创建全 0 张量。

同样通过 `size` 指定形状。


```python
# Create a tensor of all zeros
zeros = torch.zeros(size=(3, 4))
zeros, zeros.dtype
```




    (tensor([[0., 0., 0., 0.],
             [0., 0., 0., 0.],
             [0., 0., 0., 0.]]),
     torch.float32)



创建全 1 张量时改用 [`torch.ones()`](https://pytorch.org/docs/stable/generated/torch.ones.html) 即可。


```python
# Create a tensor of all ones
ones = torch.ones(size=(3, 4))
ones, ones.dtype
```




    (tensor([[1., 1., 1., 1.],
             [1., 1., 1., 1.],
             [1., 1., 1., 1.]]),
     torch.float32)



### 创建数值区间与同形张量

有时你需要一个数值区间，比如 1 到 10，或 0 到 100。

这时可以使用 `torch.arange(start, end, step)`。

其中：
* `start` = 起始值（如 0）
* `end` = 结束值（如 10）
* `step` = 步长（如 1）

> **注意：** 在 Python 里可用 `range()`。但在 PyTorch 中，`torch.range()` 已被弃用，未来可能报错。


```python
# Use torch.arange(), torch.range() is deprecated 
zero_to_ten_deprecated = torch.range(0, 10) # Note: this may return an error in the future

# Create a range of values 0 to 10
zero_to_ten = torch.arange(start=0, end=10, step=1)
zero_to_ten
```

    /tmp/ipykernel_2411/193451495.py:2: UserWarning: torch.range is deprecated and will be removed in a future release because its behavior is inconsistent with Python's range builtin. Instead, use torch.arange, which produces values in [start, end).
      zero_to_ten_deprecated = torch.range(0, 10) # Note: this may return an error in the future





    tensor([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])



有时你还需要“和已有张量形状一致”的新张量。

比如创建一个与已有张量同形状的全 0 张量。

可以用 [`torch.zeros_like(input)`](https://pytorch.org/docs/stable/generated/torch.zeros_like.html) 或 [`torch.ones_like(input)`](https://pytorch.org/docs/1.9.1/generated/torch.ones_like.html)，它们会返回与 `input` 同形状的全 0 / 全 1 张量。


```python
# Can also create a tensor of zeros similar to another tensor
ten_zeros = torch.zeros_like(input=zero_to_ten) # will have same shape
ten_zeros
```




    tensor([0, 0, 0, 0, 0, 0, 0, 0, 0, 0])



### 张量数据类型

PyTorch 提供了很多种 [张量数据类型](https://pytorch.org/docs/stable/tensors.html#data-types)。

有些更常用于 CPU，有些更适合 GPU。

理解它们的区别需要一点时间。

一般看到 `torch.cuda`，就意味着相关张量/计算在 GPU 上执行（NVIDIA GPU 依赖 CUDA 生态）。

最常见（也通常是默认）的类型是 `torch.float32` 或 `torch.float`。

这被称为“32 位浮点数”。

此外还有 16 位浮点（`torch.float16` 或 `torch.half`）和 64 位浮点（`torch.float64` 或 `torch.double`）。

再加上 8/16/32/64 位整数类型，初看会更复杂。

而且还不止这些。

> **注意：** 整数如 `7`，浮点数如 `7.0`。

之所以有这么多类型，核心与**计算精度（precision）**有关。

精度可以理解为“描述一个数值时保留的信息细节量”。

位宽越高，通常可表示细节越多，对应存储和计算代价也越高。

在深度学习里，运算次数极多，精度选择会显著影响速度与资源消耗。

所以低精度类型通常更快，但可能在准确率等指标上有一定损失。

> **参考资源：**
    * 查看 [PyTorch 数据类型文档](https://pytorch.org/docs/stable/tensors.html#data-types)。
    * 阅读 [Wikipedia: Precision (computer science)](https://en.wikipedia.org/wiki/Precision_(computer_science)) 了解计算精度。

下面演示如何通过 `dtype` 参数创建指定数据类型的张量。


```python
# Default datatype for tensors is float32
float_32_tensor = torch.tensor([3.0, 6.0, 9.0],
                               dtype=None, # defaults to None, which is torch.float32 or whatever datatype is passed
                               device=None, # defaults to None, which uses the default tensor type
                               requires_grad=False) # if True, operations perfromed on the tensor are recorded 

float_32_tensor.shape, float_32_tensor.dtype, float_32_tensor.device
```




    (torch.Size([3]), torch.float32, device(type='cpu'))



除了形状不匹配，PyTorch 里最常见的问题还包括数据类型不一致和设备不一致。

例如一个张量是 `torch.float32`，另一个是 `torch.float16`，很多运算会要求它们类型一致。

又或者一个张量在 CPU，另一个在 GPU，PyTorch 也通常要求参与同一运算的张量位于同一设备。

设备相关问题我们后面还会详细讲。

现在先创建一个 `dtype=torch.float16` 的张量。


```python
float_16_tensor = torch.tensor([3.0, 6.0, 9.0],
                               dtype=torch.float16) # torch.half would also work

float_16_tensor.dtype
```




    torch.float16



## 从张量中获取信息

当你创建好张量（或由他人、模块创建好）后，通常需要查看它们的关键信息。

我们前面已经接触过，其中最常用的三个属性是：
* `shape` - 张量形状是什么（很多运算有严格形状要求）
* `dtype` - 张量元素的数据类型是什么
* `device` - 张量存在哪个设备上（通常是 CPU 或 GPU）

我们创建一个随机张量并查看这些信息。


```python
# Create a tensor
some_tensor = torch.rand(3, 4)

# Find out details about it
print(some_tensor)
print(f"Shape of tensor: {some_tensor.shape}")
print(f"Datatype of tensor: {some_tensor.dtype}")
print(f"Device tensor is stored on: {some_tensor.device}") # will default to CPU
```

    tensor([[0.9270, 0.6217, 0.9093, 0.1493],
            [0.4354, 0.6207, 0.9224, 0.0312],
            [0.3300, 0.0959, 0.6050, 0.7674]])
    Shape of tensor: torch.Size([3, 4])
    Datatype of tensor: torch.float32
    Device tensor is stored on: cpu


> **注意：** PyTorch 中很多报错都和上面三个属性有关。看到错误时可以先问自己：
    * “形状是什么？类型是什么？设备在哪里？”

## 张量操作（tensor operations）

在深度学习里，图像、文本、视频、音频、蛋白质结构等数据都可表示成张量。

模型通过对张量进行大量运算（可能达到百万级以上）来学习输入数据中的模式。

这些运算主要围绕以下几类：
* 加法（Addition）
* 减法（Substraction）
* 乘法（元素级，Multiplication）
* 除法（Division）
* 矩阵乘法（Matrix multiplication）

基本上就这些。虽然还有更多操作，但这几类是神经网络的核心积木。

把这些操作按正确方式堆叠起来，就能构建很复杂的神经网络（就像搭乐高）。

### 基础运算

先从最基础的三个操作开始：加法（`+`）、减法（`-`）、乘法（`*`）。

它们的行为和你预期一致。


```python
# Create a tensor of values and add a number to it
tensor = torch.tensor([1, 2, 3])
tensor + 10
```




    tensor([11, 12, 13])




```python
# Multiply it by 10
tensor * 10
```




    tensor([10, 20, 30])



注意上面结果并没有变成 `tensor([110, 120, 130])`。因为张量值不会原地改变，除非你把结果重新赋值回变量。


```python
# Tensors don't change unless reassigned
tensor
```




    tensor([1, 2, 3])



接下来我们减去一个数，并把结果重新赋值给 `tensor`。


```python
# Subtract and reassign
tensor = tensor - 10
tensor
```




    tensor([-9, -8, -7])




```python
# Add and reassign
tensor = tensor + 10
tensor
```




    tensor([1, 2, 3])



PyTorch 也提供了很多内置函数，如 [`torch.mul()`](https://pytorch.org/docs/stable/generated/torch.mul.html#torch.mul)（乘法）和 [`torch.add()`](https://pytorch.org/docs/stable/generated/torch.add.html)（加法）。


```python
# Can also use torch functions
torch.multiply(tensor, 10)
```




    tensor([10, 20, 30])




```python
# Original tensor is still unchanged 
tensor
```




    tensor([1, 2, 3])



不过在日常代码里，更常直接使用 `*` 这类操作符。


```python
# Element-wise multiplication (each element multiplies its equivalent, index 0->0, 1->1, 2->2)
print(tensor, "*", tensor)
print("Equals:", tensor * tensor)
```

    tensor([1, 2, 3]) * tensor([1, 2, 3])
    Equals: tensor([1, 4, 9])


### 矩阵乘法（核心中的核心）

机器学习和深度学习（如神经网络）最常见的操作之一就是 [矩阵乘法](https://www.mathsisfun.com/algebra/matrix-multiplying.html)。

在 PyTorch 中，可通过 [`torch.matmul()`](https://pytorch.org/docs/stable/generated/torch.matmul.html) 执行矩阵乘法。

矩阵乘法要牢记两条规则：
1. **内维度**必须匹配：
  * `(3, 2) @ (3, 2)` won't work
  * `(2, 3) @ (3, 2)` will work
  * `(3, 2) @ (2, 3)` will work
2. 结果形状由**外维度**决定：
 * `(2, 3) @ (3, 2)` -> `(2, 2)`
 * `(3, 2) @ (2, 3)` -> `(3, 3)`

> **注意：** Python 里 `@` 是矩阵乘法运算符。

> **参考：** `torch.matmul()` 的完整规则见 [PyTorch 文档](https://pytorch.org/docs/stable/generated/torch.matmul.html)。

下面创建一个张量，对比元素级乘法和矩阵乘法。




```python
import torch
tensor = torch.tensor([1, 2, 3])
tensor.shape
```




    torch.Size([3])



两者关键区别在于：矩阵乘法会涉及求和累加，而元素级乘法不会。

For our `tensor` variable with values `[1, 2, 3]`:

| Operation                       | Calculation                     | Code                    |
| ------------------------------- | ------------------------------- | ----------------------- |
| **Element-wise multiplication** | `[1*1, 2*2, 3*3]` = `[1, 4, 9]` | `tensor * tensor`       |
| **Matrix multiplication**       | `[1*1 + 2*2 + 3*3]` = `[14]`    | `tensor.matmul(tensor)` |



```python
# Element-wise matrix multiplication
tensor * tensor
```




    tensor([1, 4, 9])




```python
# Matrix multiplication
torch.matmul(tensor, tensor)
```




    tensor(14)




```python
# Can also use the "@" symbol for matrix multiplication, though not recommended
tensor @ tensor
```




    tensor(14)



你当然可以手写循环做矩阵乘法，但不推荐。

内置 `torch.matmul()` 通常更快。


```python
%%time
# Matrix multiplication by hand 
# (avoid doing operations with for loops at all cost, they are computationally expensive)
value = 0
for i in range(len(tensor)):
  value += tensor[i] * tensor[i]
value
```

    CPU times: user 178 µs, sys: 62 µs, total: 240 µs
    Wall time: 248 µs





    tensor(14)




```python
%%time
torch.matmul(tensor, tensor)
```

    CPU times: user 272 µs, sys: 94 µs, total: 366 µs
    Wall time: 295 µs





    tensor(14)



## 深度学习最常见错误之一（形状错误）

由于深度学习大量依赖矩阵运算，而矩阵运算对形状有严格约束，所以“形状不匹配”是最高频错误之一。


```python
# Shapes need to be in the right way  
tensor_A = torch.tensor([[1, 2],
                         [3, 4],
                         [5, 6]], dtype=torch.float32)

tensor_B = torch.tensor([[7, 10],
                         [8, 11], 
                         [9, 12]], dtype=torch.float32)

torch.matmul(tensor_A, tensor_B) # (this will error)
```


    ---------------------------------------------------------------------------

    RuntimeError                              Traceback (most recent call last)

    /tmp/ipykernel_1722/2761025649.py in <module>
          8                          [9, 12]], dtype=torch.float32)
          9 
    ---> 10 torch.matmul(tensor_A, tensor_B) # (this will error)
    

    RuntimeError: mat1 and mat2 shapes cannot be multiplied (3x2 and 3x2)


要让 `tensor_A` 和 `tensor_B` 能相乘，需要让它们的内维度匹配。

常见方法是做 **转置（transpose）**，交换张量维度。

在 PyTorch 中可通过两种方式转置：
* `torch.transpose(input, dim0, dim1)`：`input` 为目标张量，`dim0` 与 `dim1` 为要交换的维度。
* `tensor.T`：对 `tensor` 做转置的简写。

我们先试第二种。


```python
# View tensor_A and tensor_B
print(tensor_A)
print(tensor_B)
```

    tensor([[1., 2.],
            [3., 4.],
            [5., 6.]])
    tensor([[ 7., 10.],
            [ 8., 11.],
            [ 9., 12.]])



```python
# View tensor_A and tensor_B.T
print(tensor_A)
print(tensor_B.T)
```

    tensor([[1., 2.],
            [3., 4.],
            [5., 6.]])
    tensor([[ 7.,  8.,  9.],
            [10., 11., 12.]])



```python
# The operation works when tensor_B is transposed
print(f"Original shapes: tensor_A = {tensor_A.shape}, tensor_B = {tensor_B.shape}\n")
print(f"New shapes: tensor_A = {tensor_A.shape} (same as above), tensor_B.T = {tensor_B.T.shape}\n")
print(f"Multiplying: {tensor_A.shape} * {tensor_B.T.shape} <- inner dimensions match\n")
print("Output:\n")
output = torch.matmul(tensor_A, tensor_B.T)
print(output) 
print(f"\nOutput shape: {output.shape}")
```

    Original shapes: tensor_A = torch.Size([3, 2]), tensor_B = torch.Size([3, 2])
    
    New shapes: tensor_A = torch.Size([3, 2]) (same as above), tensor_B.T = torch.Size([2, 3])
    
    Multiplying: torch.Size([3, 2]) * torch.Size([2, 3]) <- inner dimensions match
    
    Output:
    
    tensor([[ 27.,  30.,  33.],
            [ 61.,  68.,  75.],
            [ 95., 106., 117.]])
    
    Output shape: torch.Size([3, 3])


你也可以用 [`torch.mm()`](https://pytorch.org/docs/stable/generated/torch.mm.html)，它是 `torch.matmul()` 的常见简写（针对二维矩阵）。


```python
# torch.mm is a shortcut for matmul
torch.mm(tensor_A, tensor_B.T)
```




    tensor([[ 27.,  30.,  33.],
            [ 61.,  68.,  75.],
            [ 95., 106., 117.]])



如果不转置，就不满足矩阵乘法规则，会出现上面的报错。

看个可视化会更直观。

![visual demo of matrix multiplication](https://github.com/mrdbourke/pytorch-deep-learning/raw/main/images/00-matrix-multiply-crop.gif)

你也可以在 http://matrixmultiplication.xyz/ 自己做矩阵乘法可视化演示。

> **注意：** 这种运算也常称为两个矩阵的 [**点积（dot product）**](https://www.mathsisfun.com/algebra/vectors-dot-product.html)。



神经网络里到处都是矩阵乘法和点积。

[`torch.nn.Linear()`](https://pytorch.org/docs/1.9.1/generated/torch.nn.Linear.html)（也叫全连接层/前馈层）本质上就是输入 `x` 与权重矩阵 `A` 的矩阵乘法，再加上偏置。

$$
y = x\cdot{A^T} + b
$$

其中：
* `x` 是层输入（深度学习模型就是很多层的堆叠）。
* `A` 是层中的权重矩阵，初始通常为随机值，训练过程中会被更新（式子中的 `T` 表示转置）。
    * **注意：** 权重矩阵也常记作 `W` 或其他大写字母。
* `b` 是偏置项，用于对线性变换做平移。
* `y` 是层输出（对输入进行变换后得到）。

这就是线性函数（你可能见过 $y = mx+b$），其几何意义是直线变换。

我们来实际试试线性层。

你可以改改下面的 `in_features` 和 `out_features` 看看会发生什么。

留意输出形状和输入形状的关系。


```python
# Since the linear layer starts with a random weights matrix, let's make it reproducible (more on this later)
torch.manual_seed(42)
# This uses matrix multiplication
linear = torch.nn.Linear(in_features=2, # in_features = matches inner dimension of input 
                         out_features=6) # out_features = describes outer value 
x = tensor_A
output = linear(x)
print(f"Input shape: {x.shape}\n")
print(f"Output:\n{output}\n\nOutput shape: {output.shape}")
```

    Input shape: torch.Size([3, 2])
    
    Output:
    tensor([[2.2368, 1.2292, 0.4714, 0.3864, 0.1309, 0.9838],
            [4.4919, 2.1970, 0.4469, 0.5285, 0.3401, 2.4777],
            [6.7469, 3.1648, 0.4224, 0.6705, 0.5493, 3.9716]],
           grad_fn=<AddmmBackward0>)
    
    Output shape: torch.Size([3, 6])


> **思考题：** 如果把 `in_features` 从 2 改成 3，会报错吗？你该如何调整输入 `x` 的形状来适配？提示：回想上面我们是怎么处理 `tensor_B` 的。

如果你是第一次接触，矩阵乘法一开始会有点绕。

但多练几次、再看几个神经网络实现后，你会发现它无处不在。

记住这句话：矩阵乘法非常核心。

![matrix multiplication is all you need](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/00_matrix_multiplication_is_all_you_need.jpeg)

*When you start digging into neural network layers and building your own, you'll find matrix multiplications everywhere. **Source:** https://marksaroufim.substack.com/p/working-class-deep-learner*

### 求最小值、最大值、均值、求和等（聚合）

前面我们讲了很多张量操作，接下来看看聚合操作（把多值压缩成少值）。

先创建一个张量，再求它的 max、min、mean 和 sum。






```python
# Create a tensor
x = torch.arange(0, 100, 10)
x
```




    tensor([ 0, 10, 20, 30, 40, 50, 60, 70, 80, 90])



开始聚合运算。


```python
print(f"Minimum: {x.min()}")
print(f"Maximum: {x.max()}")
# print(f"Mean: {x.mean()}") # this will error
print(f"Mean: {x.type(torch.float32).mean()}") # won't work without float datatype
print(f"Sum: {x.sum()}")
```

    Minimum: 0
    Maximum: 90
    Mean: 45.0
    Sum: 450


> **注意：** 像 `torch.mean()` 这类方法通常要求张量是 `torch.float32`（或其他特定浮点类型），否则会失败。

同样的操作也可以直接使用 `torch` 函数调用。


```python
torch.max(x), torch.min(x), torch.mean(x.type(torch.float32)), torch.sum(x)
```




    (tensor(90), tensor(0), tensor(45.), tensor(450))



### 最值对应的位置（索引）

你还可以用 [`torch.argmax()`](https://pytorch.org/docs/stable/generated/torch.argmax.html) 和 [`torch.argmin()`](https://pytorch.org/docs/stable/generated/torch.argmin.html) 找到最大值/最小值所在索引。

当你只关心“位置”而不是“具体数值”时，这非常有用（后面讲 [softmax 激活函数](https://pytorch.org/docs/stable/generated/torch.nn.Softmax.html) 时会再次遇到）。


```python
# Create a tensor
tensor = torch.arange(10, 100, 10)
print(f"Tensor: {tensor}")

# Returns index of max and min values
print(f"Index where max value occurs: {tensor.argmax()}")
print(f"Index where min value occurs: {tensor.argmin()}")
```

    Tensor: tensor([10, 20, 30, 40, 50, 60, 70, 80, 90])
    Index where max value occurs: 8
    Index where min value occurs: 0


### 修改张量数据类型

前面提到过，深度学习里常见问题之一是张量类型不一致。

例如一个是 `torch.float64`，另一个是 `torch.float32`，运算时可能报错。

但这是可以修复的。

你可以使用 [`torch.Tensor.type(dtype=None)`](https://pytorch.org/docs/stable/generated/torch.Tensor.type.html) 转换张量类型，`dtype` 传入目标类型即可。

先创建一个张量并检查其默认类型（`torch.float32`）。


```python
# Create a tensor and check its datatype
tensor = torch.arange(10., 100., 10.)
tensor.dtype
```




    torch.float32



接着创建同样内容但 `dtype=torch.float16` 的张量。




```python
# Create a float16 tensor
tensor_float16 = tensor.type(torch.float16)
tensor_float16
```




    tensor([10., 20., 30., 40., 50., 60., 70., 80., 90.], dtype=torch.float16)



同理也可以转换成 `torch.int8`。


```python
# Create a int8 tensor
tensor_int8 = tensor.type(torch.int8)
tensor_int8
```




    tensor([10, 20, 30, 40, 50, 60, 70, 80, 90], dtype=torch.int8)



> **注意：** 不同类型起初确实容易混淆。可以这样理解：位宽越低（如 16、8），精度通常越低，但计算更快、模型更小。移动端网络常用 8 位整数以提升速度与部署效率，但准确性可能不如 float32。更多可读 [precision in computing](https://en.wikipedia.org/wiki/Precision_(computer_science))。

> **练习建议：** 我们已经覆盖了不少方法，但 [`torch.Tensor` 文档](https://pytorch.org/docs/stable/tensors.html) 里还有很多。建议花 10 分钟浏览，挑几个感兴趣的方法自己写代码试一遍。

### 形状变换：reshape、stack、squeeze、unsqueeze

很多时候你需要改变张量形状或维度，但不改变其中数值。

常用方法如下：

| 方法                                                                                                        | 一句话说明                                                               |
| ----------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| [`torch.reshape(input, shape)`](https://pytorch.org/docs/stable/generated/torch.reshape.html#torch.reshape) | 将 `input` 变为目标 `shape`（若兼容），也可用 `torch.Tensor.reshape()`。 |
| [`torch.Tensor.view(shape)`](https://pytorch.org/docs/stable/generated/torch.Tensor.view.html)              | 返回原张量在新形状下的视图（共享同一底层数据）。                         |
| [`torch.stack(tensors, dim=0)`](https://pytorch.org/docs/1.9.1/generated/torch.stack.html)                  | 在新维度 `dim` 上堆叠一组张量（所有张量形状需一致）。                    |
| [`torch.squeeze(input)`](https://pytorch.org/docs/stable/generated/torch.squeeze.html)                      | 删除所有长度为 `1` 的维度。                                              |
| [`torch.unsqueeze(input, dim)`](https://pytorch.org/docs/1.9.1/generated/torch.unsqueeze.html)              | 在指定 `dim` 位置插入一个长度为 `1` 的维度。                             |
| [`torch.permute(input, dims)`](https://pytorch.org/docs/stable/generated/torch.permute.html)                | 返回一个维度重排后的视图（不复制底层数据）。                             |

为什么要用这些？

因为神经网络本质上就是对张量不断变换与计算。若形状不符合矩阵规则就会报错，这些方法能帮你把维度整理到可运算状态。

我们来逐个试一下。

先创建一个张量。


```python
# Create a tensor
import torch
x = torch.arange(1., 8.)
x, x.shape
```




    (tensor([1., 2., 3., 4., 5., 6., 7.]), torch.Size([7]))



先用 `torch.reshape()` 增加一个维度。


```python
# Add an extra dimension
x_reshaped = x.reshape(1, 7)
x_reshaped, x_reshaped.shape
```




    (tensor([[1., 2., 3., 4., 5., 6., 7.]]), torch.Size([1, 7]))



也可以用 `torch.view()` 改变视图。


```python
# Change view (keeps same data as original but changes view)
# See more: https://stackoverflow.com/a/54507446/7900723
z = x.view(1, 7)
z, z.shape
```




    (tensor([[1., 2., 3., 4., 5., 6., 7.]]), torch.Size([1, 7]))



要记住，`torch.view()` 只是创建同一底层数据的新视图。

所以修改视图中的值，也会影响原张量。


```python
# Changing z changes x
z[:, 0] = 5
z, x
```




    (tensor([[5., 2., 3., 4., 5., 6., 7.]]), tensor([5., 2., 3., 4., 5., 6., 7.]))



如果想把张量按新维度堆叠多次，可用 `torch.stack()`。


```python
# Stack tensors on top of each other
x_stacked = torch.stack([x, x, x, x], dim=0) # try changing dim to dim=1 and see what happens
x_stacked
```




    tensor([[5., 2., 3., 4., 5., 6., 7.],
            [5., 2., 3., 4., 5., 6., 7.],
            [5., 2., 3., 4., 5., 6., 7.],
            [5., 2., 3., 4., 5., 6., 7.]])



如果要移除所有长度为 1 的维度呢？

可使用 `torch.squeeze()`（把张量“挤压”掉单维度）。


```python
print(f"Previous tensor: {x_reshaped}")
print(f"Previous shape: {x_reshaped.shape}")

# Remove extra dimension from x_reshaped
x_squeezed = x_reshaped.squeeze()
print(f"\nNew tensor: {x_squeezed}")
print(f"New shape: {x_squeezed.shape}")
```

    Previous tensor: tensor([[5., 2., 3., 4., 5., 6., 7.]])
    Previous shape: torch.Size([1, 7])
    
    New tensor: tensor([5., 2., 3., 4., 5., 6., 7.])
    New shape: torch.Size([7])


而 `torch.unsqueeze()` 是反向操作：在指定位置加回一个长度为 1 的维度。


```python
print(f"Previous tensor: {x_squeezed}")
print(f"Previous shape: {x_squeezed.shape}")

## Add an extra dimension with unsqueeze
x_unsqueezed = x_squeezed.unsqueeze(dim=0)
print(f"\nNew tensor: {x_unsqueezed}")
print(f"New shape: {x_unsqueezed.shape}")
```

    Previous tensor: tensor([5., 2., 3., 4., 5., 6., 7.])
    Previous shape: torch.Size([7])
    
    New tensor: tensor([[5., 2., 3., 4., 5., 6., 7.]])
    New shape: torch.Size([1, 7])


你还可以用 `torch.permute(input, dims)` 重排维度顺序，返回的是视图而非深拷贝。


```python
# Create tensor with specific shape
x_original = torch.rand(size=(224, 224, 3))

# Permute the original tensor to rearrange the axis order
x_permuted = x_original.permute(2, 0, 1) # shifts axis 0->1, 1->2, 2->0

print(f"Previous shape: {x_original.shape}")
print(f"New shape: {x_permuted.shape}")
```

    Previous shape: torch.Size([224, 224, 3])
    New shape: torch.Size([3, 224, 224])


> **注意：** `permute` 返回的是视图（共享底层数据），所以改视图会影响原张量。

## 索引（从张量中选取数据）

有时你只想取张量中的一部分数据（如某一列、某一行）。

这时就用索引。

如果你用过 Python 列表或 NumPy 数组索引，PyTorch 的索引逻辑非常相近。


```python
# Create a tensor 
import torch
x = torch.arange(1, 10).reshape(1, 3, 3)
x, x.shape
```




    (tensor([[[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9]]]),
     torch.Size([1, 3, 3]))



索引顺序通常是从外层维度到内层维度（可结合方括号理解）。


```python
# Let's index bracket by bracket
print(f"First square bracket:\n{x[0]}") 
print(f"Second square bracket: {x[0][0]}") 
print(f"Third square bracket: {x[0][0][0]}")
```

    First square bracket:
    tensor([[1, 2, 3],
            [4, 5, 6],
            [7, 8, 9]])
    Second square bracket: tensor([1, 2, 3])
    Third square bracket: 1


你还可以用 `:` 表示“该维度全部元素”，再用逗号 `,` 继续指定下一维。


```python
# Get all values of 0th dimension and the 0 index of 1st dimension
x[:, 0]
```




    tensor([[1, 2, 3]])




```python
# Get all values of 0th & 1st dimensions but only index 1 of 2nd dimension
x[:, :, 1]
```




    tensor([[2, 5, 8]])




```python
# Get all values of the 0 dimension but only the 1 index value of the 1st and 2nd dimension
x[:, 1, 1]
```




    tensor([5])




```python
# Get index 0 of 0th and 1st dimension and all values of 2nd dimension 
x[0, 0, :] # same as x[0][0]
```




    tensor([1, 2, 3])



索引一开始可能有点绕，特别是高维张量。多练习并多做可视化，你会很快熟悉。

## PyTorch 张量与 NumPy

NumPy 是 Python 里最常用的数值计算库之一，PyTorch 对它提供了良好互操作支持。

最常用的两个方法是：
* [`torch.from_numpy(ndarray)`](https://pytorch.org/docs/stable/generated/torch.from_numpy.html)：NumPy array -> PyTorch tensor。
* [`torch.Tensor.numpy()`](https://pytorch.org/docs/stable/generated/torch.Tensor.numpy.html)：PyTorch tensor -> NumPy array。

我们来试一下。


```python
# NumPy array to tensor
import torch
import numpy as np
array = np.arange(1.0, 8.0)
tensor = torch.from_numpy(array)
array, tensor
```




    (array([1., 2., 3., 4., 5., 6., 7.]),
     tensor([1., 2., 3., 4., 5., 6., 7.], dtype=torch.float64))



> **注意：** NumPy 默认常用 `float64`，转到 PyTorch 后会保留该类型。
>
> 但 PyTorch 很多计算默认更偏向 `float32`。
>
> 因此如果你要把 NumPy `float64` 转成 PyTorch `float32`，可写：`tensor = torch.from_numpy(array).type(torch.float32)`。

由于上面重新赋值了 `tensor`，后续改 `tensor` 时，`array` 不会跟着变。


```python
# Change the array, keep the tensor
array = array + 1
array, tensor
```




    (array([2., 3., 4., 5., 6., 7., 8.]),
     tensor([1., 2., 3., 4., 5., 6., 7.], dtype=torch.float64))



反过来，从 PyTorch 转到 NumPy 可直接调用 `tensor.numpy()`。


```python
# Tensor to NumPy array
tensor = torch.ones(7) # create a tensor of ones with dtype=float32
numpy_tensor = tensor.numpy() # will be dtype=float32 unless changed
tensor, numpy_tensor
```




    (tensor([1., 1., 1., 1., 1., 1., 1.]),
     array([1., 1., 1., 1., 1., 1., 1.], dtype=float32))



同理，若重新赋值修改原 `tensor`，`numpy_tensor` 仍保持原值。


```python
# Change the tensor, keep the array the same
tensor = tensor + 1
tensor, numpy_tensor
```




    (tensor([2., 2., 2., 2., 2., 2., 2.]),
     array([1., 1., 1., 1., 1., 1., 1.], dtype=float32))



## 可复现性（让随机变得可控）

随着你学习深入，会发现神经网络和机器学习里“随机性”无处不在。

更准确说是“伪随机”。计算机本质是确定性的，因此所谓随机通常是通过算法模拟出来的随机序列。

这和深度学习有什么关系？

我们提到过：神经网络通常从随机参数开始，再通过张量运算不断更新参数，以更好拟合数据模式。

简化成一句话：

`随机初始化 -> 张量运算更新 -> 持续迭代优化`

随机性很有用，但有时我们希望它“少随机一点”。

为什么？

因为我们需要可重复实验。

比如你实现了一个能达到某个性能的算法。

你的同学想复现实验验证结果。

他要如何得到与你一致的结果？

这就是**可复现性（reproducibility）**的意义。

也就是说：同样代码在不同机器上，能否得到相同或非常接近的结果？

下面用一个简短例子说明 PyTorch 中的可复现性。

先创建两个随机张量。按直觉，它们应该不同。


```python
import torch

# Create two random tensors
random_tensor_A = torch.rand(3, 4)
random_tensor_B = torch.rand(3, 4)

print(f"Tensor A:\n{random_tensor_A}\n")
print(f"Tensor B:\n{random_tensor_B}\n")
print(f"Does Tensor A equal Tensor B? (anywhere)")
random_tensor_A == random_tensor_B
```

    Tensor A:
    tensor([[0.8016, 0.3649, 0.6286, 0.9663],
            [0.7687, 0.4566, 0.5745, 0.9200],
            [0.3230, 0.8613, 0.0919, 0.3102]])
    
    Tensor B:
    tensor([[0.9536, 0.6002, 0.0351, 0.6826],
            [0.3743, 0.5220, 0.1336, 0.9666],
            [0.9754, 0.8474, 0.8988, 0.1105]])
    
    Does Tensor A equal Tensor B? (anywhere)





    tensor([[False, False, False, False],
            [False, False, False, False],
            [False, False, False, False]])



结果和预期一致：两个张量值不同。

如果你希望两次随机生成结果一致呢？

也就是“仍然是随机数，但每次生成同一组随机序列”。

这时用 [`torch.manual_seed(seed)`](https://pytorch.org/docs/stable/generated/torch.manual_seed.html)。`seed` 是整数（如 `42`），用于固定随机序列。

我们来试试固定 seed 后的随机张量。


```python
import torch
import random

# # Set the random seed
RANDOM_SEED=42 # try changing this to different values and see what happens to the numbers below
torch.manual_seed(seed=RANDOM_SEED) 
random_tensor_C = torch.rand(3, 4)

# Have to reset the seed every time a new rand() is called 
# Without this, tensor_D would be different to tensor_C 
torch.random.manual_seed(seed=RANDOM_SEED) # try commenting this line out and seeing what happens
random_tensor_D = torch.rand(3, 4)

print(f"Tensor C:\n{random_tensor_C}\n")
print(f"Tensor D:\n{random_tensor_D}\n")
print(f"Does Tensor C equal Tensor D? (anywhere)")
random_tensor_C == random_tensor_D
```

    Tensor C:
    tensor([[0.8823, 0.9150, 0.3829, 0.9593],
            [0.3904, 0.6009, 0.2566, 0.7936],
            [0.9408, 0.1332, 0.9346, 0.5936]])
    
    Tensor D:
    tensor([[0.8823, 0.9150, 0.3829, 0.9593],
            [0.3904, 0.6009, 0.2566, 0.7936],
            [0.9408, 0.1332, 0.9346, 0.5936]])
    
    Does Tensor C equal Tensor D? (anywhere)





    tensor([[True, True, True, True],
            [True, True, True, True],
            [True, True, True, True]])



很好。

看起来 seed 已生效。

> **参考资源：** 我们这里只是触及可复现性的基础。建议继续阅读：
> * [PyTorch reproducibility 文档](https://pytorch.org/docs/stable/notes/randomness.html)（建议至少花 10 分钟浏览，先建立认知）。
> * [Wikipedia: Random seed](https://en.wikipedia.org/wiki/Random_seed)（理解随机种子与伪随机原理）。

## 在 GPU 上运行张量（加速计算）

深度学习算法需要大量数值计算。

默认情况下，这些计算通常在 CPU 上执行。

但另一类常见硬件 GPU（图形处理器）在神经网络核心操作（如矩阵乘法）上通常比 CPU 快很多。

你的机器可能就有 GPU。

如果有，训练神经网络时应尽量使用它，训练速度通常会显著提升。

接下来分两步：先获得 GPU 资源，再让 PyTorch 使用它。

> **注意：** 本课程提到“GPU”时，默认指支持 CUDA 的 [NVIDIA GPU](https://developer.nvidia.com/cuda-gpus)（除非另有说明）。




### 1. 获得 GPU

你可能已经熟悉 GPU；如果还不熟，下面是常见获取方式。

| **方式**                | **配置难度** | **优点**                       | **缺点**                           | **如何配置**                                                               |
| ----------------------- | ------------ | ------------------------------ | ---------------------------------- | -------------------------------------------------------------------------- |
| Google Colab            | 低           | 免费、几乎零配置、链接即可分享 | 结果不易持久保存、算力受限、会超时 | [Google Colab 指南](https://colab.research.google.com/notebooks/gpu.ipynb) |
| 自有设备                | 中           | 本地全可控                     | GPU 成本高、需前期投入             | [PyTorch 本地安装指南](https://pytorch.org/get-started/locally/)           |
| 云计算（AWS/GCP/Azure） | 中-高        | 前期投入小、可扩展算力大       | 持续运行成本高、配置较复杂         | [PyTorch 云平台指南](https://pytorch.org/get-started/cloud-partners/)      |

GPU 方案远不止这三种，但对入门阶段已足够。

我个人通常是 Colab + 本地机器做小规模实验，需要更大算力时再上云。

> **参考：** 如果你打算自购 GPU，可参考 [Tim Dettmers 的选购指南](https://timdettmers.com/2020/09/07/which-gpu-for-deep-learning/)。

检查是否可访问 NVIDIA GPU，可运行 `!nvidia-smi`。其中 `!` 表示在命令行执行。




```python
!nvidia-smi
```

    /usr/bin/sh: 1: nvidia-smi: not found


如果没有可用 NVIDIA GPU，通常会看到类似提示：

```
NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.
```

这时请回到上面的安装步骤重新检查环境。

如果有 GPU，则会输出类似下方信息：

```
Wed Jan 19 22:09:08 2022       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 495.46       Driver Version: 460.32.03    CUDA Version: 11.2     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla P100-PCIE...  Off  | 00000000:00:04.0 Off |                    0 |
| N/A   35C    P0    27W / 250W |      0MiB / 16280MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```



### 2. 让 PyTorch 使用 GPU

拿到 GPU 后，下一步是让 PyTorch 用 GPU 存储张量并执行计算。

这需要用到 [`torch.cuda`](https://pytorch.org/docs/stable/cuda.html) 模块。

直接实操更直观。

可用 [`torch.cuda.is_available()`](https://pytorch.org/docs/stable/generated/torch.cuda.is_available.html#torch.cuda.is_available) 检查 PyTorch 是否识别 GPU。



```python
# Check for GPU
import torch
torch.cuda.is_available()
```




    False



若输出 `True`，说明可用；若是 `False`，说明当前环境还未正确配置 GPU 支持。

通常我们希望代码可在 CPU 或 GPU 上自动运行。

这样无论谁运行代码，都能在现有设备上正常执行。

因此先定义 `device` 变量保存当前可用设备类型。


```python
# Set device type
device = "cuda" if torch.cuda.is_available() else "cpu"
device
```




    'cpu'



如果输出是 `"cuda"`，表示可用 GPU；若输出 `"cpu"`，则代码会继续在 CPU 上运行。

> **注意：** 在 PyTorch 中，推荐写 [**device agnostic code**](https://pytorch.org/docs/master/notes/cuda.html#device-agnostic-code)，即代码可在 CPU 与 GPU 间自动适配。

想更快可以用单 GPU；想再快一个量级，可考虑多 GPU。

可通过 [`torch.cuda.device_count()`](https://pytorch.org/docs/stable/generated/torch.cuda.device_count.html#torch.cuda.device_count) 查看可用 GPU 数量。


```python
# Count number of devices
torch.cuda.device_count()
```




    0



知道 GPU 数量有助于做多卡任务分配（PyTorch 也支持跨多卡并行）。

### 3. 把张量（和模型）放到 GPU

你可以对张量（模型同理，后面会讲）调用 [`to(device)`](https://pytorch.org/docs/stable/generated/torch.Tensor.to.html) 将其移动到指定设备。

为什么这样做？

因为 GPU 在数值计算上通常更快；若无 GPU，我们的“设备无关代码”会自动退回 CPU。

> **注意：** `some_tensor.to(device)` 会返回新副本。若要覆盖原变量，请重新赋值：
>
> `some_tensor = some_tensor.to(device)`

下面创建一个张量并尝试放到 GPU（若可用）。


```python
# Create tensor (default on CPU)
tensor = torch.tensor([1, 2, 3])

# Tensor not on GPU
print(tensor, tensor.device)

# Move tensor to GPU (if available)
tensor_on_gpu = tensor.to(device)
tensor_on_gpu
```

    tensor([1, 2, 3]) cpu





    tensor([1, 2, 3])



如果可用 GPU，上面输出会类似：

```
tensor([1, 2, 3]) cpu
tensor([1, 2, 3], device='cuda:0')
```

注意第二个张量的 `device='cuda:0'`，表示它在第 0 块 GPU（索引从 0 开始）。



### 4. 把张量移回 CPU

如果我们要把张量移回 CPU 呢？

比如你要和 NumPy 交互时就需要这么做（NumPy 不直接用 GPU）。

先尝试对 `tensor_on_gpu` 直接调用 [`torch.Tensor.numpy()`](https://pytorch.org/docs/stable/generated/torch.Tensor.numpy.html)。


```python
# If tensor is on GPU, can't transform it to NumPy (this will error)
tensor_on_gpu.numpy()
```




    array([1, 2, 3])



更稳妥的方式是先调用 [`Tensor.cpu()`](https://pytorch.org/docs/stable/generated/torch.Tensor.cpu.html) 回到 CPU。

这会把张量复制到 CPU 内存，从而可被 NumPy 使用。


```python
# Instead, copy the tensor back to cpu
tensor_back_on_cpu = tensor_on_gpu.cpu().numpy()
tensor_back_on_cpu
```




    array([1, 2, 3])



这一步返回的是 CPU 副本，原始 GPU 张量仍保留在原设备上。


```python
tensor_on_gpu
```




    tensor([1, 2, 3])



## 练习

以下练习都围绕上文代码展开。

你可以通过回看对应章节或参考链接完成它们。

**资源：**

* [00 章练习模板 notebook](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/extras/exercises/00_pytorch_fundamentals_exercises.ipynb)。
* [00 章参考解答 notebook](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/extras/solutions/00_pytorch_fundamentals_exercise_solutions.ipynb)（建议先独立完成再看）。

1. 文档阅读：学习深度学习（以及编程）很重要的一点是熟悉框架文档。课程后续会频繁使用 PyTorch 文档。建议先花 10 分钟阅读 [`torch.Tensor`](https://pytorch.org/docs/stable/tensors.html#torch-tensor) 与 [`torch.cuda`](https://pytorch.org/docs/master/notes/cuda.html#cuda-semantics)（暂时看不懂也没关系，先建立认识）。
2. 创建一个形状为 `(7, 7)` 的随机张量。
3. 用第 2 题的张量与另一个形状为 `(1, 7)` 的随机张量做矩阵乘法（提示：你可能需要转置第二个张量）。
4. 将随机种子设为 `0`，重做第 2 和第 3 题。
5. 我们看到了 `torch.manual_seed()`，那 GPU 有没有对应方法？（提示：查 `torch.cuda` 文档）如果有，把 GPU 随机种子设为 `1234`。
6. 创建两个形状为 `(2, 3)` 的随机张量并都发送到 GPU（需要可用 GPU）。创建时设置 `torch.manual_seed(1234)`（不必是 GPU 专用随机种子）。
7. 对第 6 题的两个张量做矩阵乘法（同样可能要调整其中一个张量的形状）。
8. 找出第 7 题输出的最大值和最小值。
9. 找出第 7 题输出中最大值和最小值对应的索引。
10. 创建形状为 `(1, 1, 1, 10)` 的随机张量，再去掉所有值为 `1` 的维度，得到形状 `(10)` 的新张量。创建时将 seed 设为 `7`，并打印两个张量及其形状。

## 课外延伸

* 花 1 小时学习 [PyTorch basics tutorial](https://pytorch.org/tutorials/beginner/basics/intro.html)（推荐先看 [Quickstart](https://pytorch.org/tutorials/beginner/basics/quickstart_tutorial.html) 和 [Tensors](https://pytorch.org/tutorials/beginner/basics/tensorqs_tutorial.html)）。
* 想更直观理解“张量如何表示数据”，可看这个视频：[What's a tensor?](https://youtu.be/f5liqUk0ZTw)
