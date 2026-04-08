# PyTorch 进阶资源

即使 Zero to Mastery 的 PyTorch 全课程已经超过 40 小时，你学完后大概率仍会想继续深入。

毕竟这门课的定位是“帮你建立 PyTorch 学习动量”。

下面这些资源就是为课程后续进阶准备的延伸阅读。

先提醒一句：资源很多。

建议每个小节先挑 1-2 个资源深入，剩下的先收藏，后面再看。

“哪个最好？”

能进入这份清单的，整体都值得信赖。

多数资源是纯 PyTorch 相关，也有少量不是 PyTorch 专属，但在机器学习实践中同样很有价值。

## 🔥 纯 PyTorch 资源

- [**PyTorch blog**](https://pytorch.org/blog/) - 最权威的一手更新来源。我一般每月看 1 次左右。
- [**PyTorch documentation**](https://pytorch.org/docs) - 虽然课程里已经大量使用，但仍有很多内容没覆盖，建议持续查阅。
- [**PyTorch Performance Tuning Guide**](https://pytorch.org/tutorials/recipes/recipes/tuning_guide.html#) - 课程之后你最常做的事之一就是提速（训练和推理），这份官方性能调优指南非常实用。
- [**PyTorch Recipes**](https://pytorch.org/tutorials/recipes/recipes_index.html) - 官方“配方”集合，都是小而实用的工作流教程，例如 [Loading Data in PyTorch](https://pytorch.org/tutorials/recipes/recipes/loading_data_recipe.html) 和 [Saving and Loading models for Inference in PyTorch](https://pytorch.org/tutorials/recipes/recipes/saving_and_loading_models_for_inference.html)。
- [**PyTorch Ecosystem**](https://pytorch.org/ecosystem/) - 围绕 PyTorch 的生态工具总览，覆盖不同领域。比如 3D 视觉的 [PyTorch3D](https://pytorch3d.org)、数据增强的 [Albumentations](https://github.com/albumentations-team/albumentations)、模型评估的 [TorchMetrics](https://torchmetrics.readthedocs.io/en/stable/)。
- [**Setting up PyTorch in VSCode**](https://code.visualstudio.com/docs/datascience/pytorch-support) - VS Code 是非常流行的 IDE。课程主要用 Colab 方便入门，但你很快会转向 IDE 开发，这份文档很有帮助。

## 📈 让纯 PyTorch 更强的库

课程刻意聚焦纯 PyTorch（尽量少依赖外部库），因为你一旦掌握“原生写法”，扩展库就会更容易上手。

- [**fast.ai**](https://github.com/fastai/fastai) - 开源高层库，帮你处理很多重复工作。其免费 [course](https://course.fast.ai) 和 [documentation](https://docs.fast.ai) 都非常优秀。
- [**MosaicML for more efficient model training**](https://github.com/mosaicml/composer) - 训练越快，实验迭代越快。MosaicML 的 `Composer` 通过底层优化策略提升训练效率，文档质量也很高。
- [**PyTorch Lightning for reducing boilerplate**](https://www.pytorchlightning.ai) - 减少样板代码，把训练循环、checkpoint、日志等常见流程封装好，适合提升工程效率。

![Libraries that extend/make pure PyTorch better.](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/extras-001-libraries-to-make-pytorch-better-or-faster.jpeg)

*扩展并增强纯 PyTorch 的常用库。*

## 📖 PyTorch 相关书籍

- [**Machine Learning with PyTorch and Scikit-Learn by Sebastian Raschka**](https://www.amazon.com/Machine-Learning-PyTorch-Scikit-Learn-scikit-learn-ebook-dp-B09NW48MR1/dp/B09NW48MR1/) - 机器学习与深度学习入门佳作，先讲结构化数据上的传统方法，再进入 PyTorch 深度学习。
- [**PyTorch Step-by-Step series by Daniel Voigt Godoy**](https://pytorchstepbystep.com) - 与课程“代码优先”不同，这套书更偏“概念优先 + 代码示例”，含 Fundamentals、Computer Vision、Sequences（NLP）三册。
- [**Dive into Deep Learning**](https://d2l.ai) - 非常系统的深度学习在线书，含 PyTorch、TensorFlow、Gluon 示例，且免费。比如可以看其 [Vision Transformer 章节](https://d2l.ai/chapter_attention-mechanisms-and-transformers/vision-transformer.html)。
- **Bonus:** [fast.ai 课程](https://course.fast.ai) 也有对应免费在线书 [Deep Learning for Coders with fastai & PyTorch](https://course.fast.ai/Resources/book.html)。

![Textbooks to learn more about PyTorch as well as deep learning in general.](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/extras-002-books-for-pytorch.jpeg)

*学习 PyTorch 与深度学习的优质书籍。*

## 🏗 机器学习工程（MLOps）资源

机器学习工程（也常称 MLOps）关注的是：如何把你训练好的模型真正交付给别人使用（例如线上服务或业务决策系统）。

下面这些资源有助于你补齐“训练模型之外”的工程能力。

- **[Designing Machine Learning Systems by Chip Huyen](https://www.amazon.com/Designing-Machine-Learning-Systems-Production-Ready/dp/1098107969)** - 更偏“系统视角”，覆盖数据工程、训练、部署（在线/离线）、监控等全流程。
- **[Made With ML by Goku Mohandas](https://madewithml.com)** - 我常用来查 MLOps 主题，尤其是 [madewithml.com/mlops](https://madewithml.com/#mlops)。内容既讲原理也讲端到端实践。
- **[The Machine Learning Engineering book by Andriy Burkov](http://www.mlebook.com)** - 很精炼，适合当工程实践参考手册。
- **[Full Stack Deep Learning course](https://fullstackdeeplearning.com)** - 系统讲解如何规划 ML 项目、准备数据、排障以及构建 ML 产品。

![Resources to improve your machine learning engineering skills (all of the steps that go around building a machine learning model).](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/extras-003-places-to-learn-ml-ops.jpeg)

*提升机器学习工程能力的学习资源。*

## 🗃 去哪里找数据集

机器学习项目从数据开始。

没有数据，就没有 ML。

下面这些资源非常适合查找开源且可直接使用的数据集。

- [**Paperswithcode Datasets**](https://paperswithcode.com/datasets) - 查常见 benchmark 数据集，了解来源、内容和当前最优模型。
- [**HuggingFace Datasets**](https://huggingface.co/docs/datasets) - 既是数据集平台也是工具库，几行代码就能下载使用。
- **[Kaggle Datasets](https://www.kaggle.com/datasets)** - 覆盖面非常广，很多数据来自真实业务场景。
- **[Google Dataset search](https://datasetsearch.research.google.com)** - 类似 Google 搜索，但专门用于数据集。

这些资源足够你起步。但在很多真实任务里，你最终仍需要自建数据集。

![Places to find existing and open-source datasets for a variety of problem spaces.](https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/extras-004-places-to-find-datasets.jpeg)

*查找开源数据集的常用入口。*

## 深度学习领域工具

下面按任务领域给出常用库和预训练模型资源。

### 😎 计算机视觉

我们在 [03. PyTorch Computer Vision](https://www.learnpytorch.io/03_pytorch_computer_vision/) 已介绍视觉任务。若你的数据是图片、X 光片、生产线视频、手写文档等，通常属于计算机视觉问题。

- **[TorchVision](https://pytorch.org/vision/stable/index.html)** - PyTorch 官方视觉库，含数据加载工具和大量预训练模型。
- [**timm (Torch Image Models)**](https://github.com/rwightman/pytorch-image-models) - 非常全面的视觉模型库，很多最新研究都会用到。
- **[Yolov5 for object detection](https://github.com/ultralytics/yolov5)** - 做目标检测时常见且高效的入门路径。
- **[VISSL (Vision Self-Supervised Learning)](https://github.com/facebookresearch/vissl)** - 自监督视觉学习工具库，便于快速试验相关范式。

### 📚 自然语言处理（NLP）

NLP 关注从文本中发现模式，比如信息抽取、文本分类等。

如果你的任务涉及大量文本，建议优先看：

- **[TorchText](https://pytorch.org/text/stable/index.html)** - PyTorch 官方文本库，提供数据处理和预训练模型支持。
- [**HuggingFace Transformers**](https://huggingface.co/docs/transformers/index) - NLP 事实标准库之一，提供大量 SOTA 预训练模型和配套工具。
- **Bonus:** HuggingFace 团队提供了 [免费在线课程](https://huggingface.co/course/chapter1/1)。

### 🎤 语音与音频

如果任务是音频分类、语音识别、语音转文本等，可重点看：

- [**TorchAudio**](https://pytorch.org/audio/stable/index.html) - PyTorch 官方音频库，含数据处理与模型组件。
- **[SpeechBrain](https://speechbrain.github.io)** - 基于 PyTorch 的语音开源库，覆盖识别、增强、TTS 等，且许多模型可在 [HuggingFace Hub](https://huggingface.co/speechbrain) 直接体验。

### ❓ 推荐系统

互联网平台几乎都依赖推荐：YouTube 推荐视频、Netflix 推荐影视、Amazon 推荐商品。

如果你在做电商或内容平台，推荐系统通常是核心能力。

- **[TorchRec](https://pytorch.org/torchrec/)** - PyTorch 官方推荐系统库，提供数据集与模型组件。若不自建，也可考虑云厂商推荐服务。

### ⏳ 时间序列

如果你的数据带时间维度，并希望“用过去预测未来”（如电力需求预测），可参考时间序列工具库。

下面两个库不一定是 PyTorch 专属，但时间序列太常见，值得纳入这份清单。

- [**Salesforce Merlion**](https://github.com/salesforce/Merlion) - 提供时间序列预测与异常检测的完整工具链（含 AutoML 能力）。
- [**Facebook Kats**](https://github.com/facebookresearch/Kats) - Meta 开源时间序列工具库，覆盖预测、检测与数据处理。

## 👩‍💻 如何找工作

学完 ML 课程后，下一步通常就是把技能用起来，最好还能变成职业机会。

下面这些资源能帮助你更务实地走向岗位。

- **["How can a beginner data scientist like me gain experience?"](https://www.mrdbourke.com/how-can-a-beginner-data-scientist-like-me-gain-experience/) by Daniel Bourke** - 很多人卡在“经验要求”。一个有效策略是：在拿到岗位前，就先做岗位会做的事（项目、作品、公开输出）。
- **[You Don’t Really Need Another MOOC](https://eugeneyan.com/writing/you-dont-need-another-mooc/) by Eugene Yan** - 课程学到一定阶段会出现边际收益递减。与其无止境刷课，不如开始做项目、构建真实能力并展示出来。
- **Bonus:** 机器学习面试可参考 Chip Huyen 的免费书 [Introduction to Machine Learning Interviews](https://huyenchip.com/ml-interviews-book/)。
