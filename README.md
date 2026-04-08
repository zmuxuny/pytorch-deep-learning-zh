# Learn PyTorch 深度学习课程

欢迎来到 [Zero to Mastery Learn PyTorch for Deep Learning 课程](https://dbourke.link/ZTMPyTorch)。这里是全网第二好的 PyTorch 学习入口（第一名当然是 [PyTorch 官方文档](https://pytorch.org/docs/stable/index.html)）。

* **2023 年 4 月更新：** 全新 [PyTorch 2.0 教程](https://www.learnpytorch.io/pytorch_2_intro/) 已上线。由于 PyTorch 2.0 是增量且向后兼容版本，课程此前的大多数内容依然可用。

<div align="center">
    <a href="https://learnpytorch.io">
        <img src="https://raw.githubusercontent.com/mrdbourke/pytorch-deep-learning/main/images/misc-pytorch-course-launch-cover-white-text-black-background.jpg" width=750 alt="pytorch deep learning by zero to mastery cover photo with different sections of the course">
    </a>
</div>

## 本页内容

* [课程资料/大纲](https://github.com/mrdbourke/pytorch-deep-learning#course-materialsoutline)
* [关于本课程](https://github.com/mrdbourke/pytorch-deep-learning#about-this-course)
* [进度状态](https://github.com/mrdbourke/pytorch-deep-learning#status)（课程制作进展）
* [更新日志](https://github.com/mrdbourke/pytorch-deep-learning#log)（课程材料制作记录）

## 课程资料/大纲

* 📖 **在线书版本：** 所有课程材料都可在 [learnpytorch.io](https://learnpytorch.io) 阅读。
* 🎥 **YouTube 前五章：** 通过 [前 25 小时内容](https://youtu.be/Z_ikDlimN6A) 一天速学 PyTorch。
* 🔬 **课程重点：** 写代码、做实验、反复验证。
* 🏃‍♂️ **教学风格：** [https://sive.rs/kimo](https://sive.rs/kimo)。
* 🤔 **提问交流：** 可在 [GitHub Discussions](https://github.com/mrdbourke/pytorch-deep-learning/discussions) 查找或提问。

| **章节** | **涵盖内容** | **练习与进阶** | **Slides** |
| ----- | ----- | ----- | ----- |
| [00 - PyTorch Fundamentals](https://www.learnpytorch.io/00_pytorch_fundamentals/) | 深度学习和神经网络常用的 PyTorch 基础操作。 | [前往练习与进阶](https://www.learnpytorch.io/00_pytorch_fundamentals/#exercises) | [查看 Slides](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/slides/00_pytorch_and_deep_learning_fundamentals.pdf) |
| [01 - PyTorch Workflow](https://www.learnpytorch.io/01_pytorch_workflow/) | 给出用 PyTorch 构建模型、解决深度学习问题的标准流程。 | [前往练习与进阶](https://www.learnpytorch.io/01_pytorch_workflow/#exercises) | [查看 Slides](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/slides/01_pytorch_workflow.pdf) |
| [02 - PyTorch Neural Network Classification](https://www.learnpytorch.io/02_pytorch_classification/) | 按照 01 章流程完成一个神经网络分类任务。 | [前往练习与进阶](https://www.learnpytorch.io/02_pytorch_classification/#exercises) | [查看 Slides](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/slides/02_pytorch_classification.pdf) |
| [03 - PyTorch Computer Vision](https://www.learnpytorch.io/03_pytorch_computer_vision/) | 使用与 01 和 02 相同的流程解决计算机视觉问题。 | [前往练习与进阶](https://www.learnpytorch.io/03_pytorch_computer_vision/#exercises) | [查看 Slides](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/slides/03_pytorch_computer_vision.pdf) |
| [04 - PyTorch Custom Datasets](https://www.learnpytorch.io/04_pytorch_custom_datasets/) | 讲解如何加载自定义数据集，并为 05 章模块化打基础。 | [前往练习与进阶](https://www.learnpytorch.io/04_pytorch_custom_datasets/#exercises) | [查看 Slides](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/slides/04_pytorch_custom_datasets.pdf) |
| [05 - PyTorch Going Modular](https://www.learnpytorch.io/05_pytorch_going_modular/) | 把 notebook 代码转成 Python 脚本模块（真实项目常见写法）。 | [前往练习与进阶](https://www.learnpytorch.io/05_pytorch_going_modular/#exercises) | [查看 Slides](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/slides/05_pytorch_going_modular.pdf) |
| [06 - PyTorch Transfer Learning](https://www.learnpytorch.io/06_pytorch_transfer_learning/) | 使用高性能预训练模型并适配到自己的任务。 | [前往练习与进阶](https://www.learnpytorch.io/06_pytorch_transfer_learning/#exercises) | [查看 Slides](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/slides/06_pytorch_transfer_learning.pdf) |
| [07 - Milestone Project 1: PyTorch Experiment Tracking](https://www.learnpytorch.io/07_pytorch_experiment_tracking/) | 我们已经训练了很多模型，如何追踪每个实验表现？ | [前往练习与进阶](https://www.learnpytorch.io/07_pytorch_experiment_tracking/#exercises) | [查看 Slides](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/slides/07_pytorch_experiment_tracking.pdf) |
| [08 - Milestone Project 2: PyTorch Paper Replicating](https://www.learnpytorch.io/08_pytorch_paper_replicating/) | 通过论文复现理解 PyTorch 为何在研究领域如此流行。 | [前往练习与进阶](https://www.learnpytorch.io/08_pytorch_paper_replicating/#exercises) | [查看 Slides](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/slides/08_pytorch_paper_replicating.pdf) |
| [09 - Milestone Project 3: Model Deployment](https://www.learnpytorch.io/09_pytorch_model_deployment/) | 模型训练好了，如何真正部署到互联网上供别人使用？ | [前往练习与进阶](https://www.learnpytorch.io/09_pytorch_model_deployment/#exercises) | [查看 Slides](https://github.com/mrdbourke/pytorch-deep-learning/blob/main/slides/09_pytorch_model_deployment.pdf) |
| [PyTorch Extra Resources](https://www.learnpytorch.io/pytorch_extra_resources/) | 课程覆盖很广，但机器学习世界更大，这里汇总 PyTorch、深度学习、ML 工程、NLP、时间序列与数据集等进阶资源。 | - | - |
| [PyTorch Cheatsheet](https://www.learnpytorch.io/pytorch_cheatsheet/) | 对 PyTorch 关键能力做极速速查，并附更多学习链接。 | - | - |
| [A Quick PyTorch 2.0 Tutorial](https://www.learnpytorch.io/pytorch_2_intro/) | PyTorch 2.0 超快速上手：新特性、入门方式与扩展资源。 | - | - |

## 进度状态

所有课程材料已完成，视频也已在 Zero to Mastery 发布。

项目看板见：https://github.com/users/mrdbourke/projects/1

* **视频总数：** 321
* **已完成骨架代码：** 00, 01, 02, 03, 04, 05, 06, 07, 08, 09
* **已完成注释文本：** 00, 01, 02, 03, 04, 05, 06, 07, 08, 09
* **已完成配图：** 00, 01, 02, 03, 04, 05, 06, 07, 08, 09
* **已完成 Keynote：** 00, 01, 02, 03, 04, 05, 06, 07, 08, 09
* **已完成练习与解答：** 00, 01, 02, 03, 04, 05, 06, 07, 08, 09

日常更新记录可见 [log](https://github.com/mrdbourke/pytorch-deep-learning#log)。

## 关于本课程

### 这门课适合谁？

**你：** 是机器学习或深度学习初学者，想系统学习 PyTorch。

**这门课：** 用大量实操、代码优先的方式教你 PyTorch 与关键机器学习概念。

如果你已有 1 年以上机器学习经验，这门课也可能有帮助，但它的定位是对新手友好。

### 先修要求是什么？

1. 3-6 个月 Python 编程经验。
2. 至少上一门机器学习入门课（也可边学边补，文中有大量资源链接）。
3. 有 Jupyter Notebook 或 Google Colab 使用经验（不会也能边做边学）。
4. 愿意持续学习（最重要）。

针对前两项，我推荐 [Zero to Mastery Data Science and Machine Learning Bootcamp](https://dbourke.link/ZTMMLcourse)，它会讲清机器学习与 Python 基础（我也参与授课，所以有点“主观推荐”）。

### 课程是怎么教的？

全部课程材料都可在 [learnpytorch.io](https://learnpytorch.io) 免费阅读。若你偏好文字学习，推荐从在线书直接开始。

若你更喜欢视频，课程也采用“学徒式”方式：我写 PyTorch 代码，你同步实操。

课程口号是 *if in doubt, run the code* 与 *experiment, experiment, experiment!*，因为机器学习最有效的学习方式就是亲手实践。

我的唯一目标是帮你做到一件事：通过写 PyTorch 代码真正学会机器学习。

课程代码主要在 [Google Colab Notebooks](https://colab.research.google.com) 编写（你也可以使用 Jupyter Notebooks），这是一个非常适合实验机器学习的免费工具。

### 学完整门课后我会收获什么？

看完视频会有证书等内容。

但证书不是核心价值。

你可以把这门课当作“机器学习加速器”。

到课程结束时，你会写下数百行 PyTorch 代码。

并接触到机器学习里很多关键概念。

这样当你构建自己的项目，或者阅读开源 PyTorch 项目时，会更有方向感；即使陌生，也知道该从哪里查起。

### 我会在课程里做什么项目？

我们从 PyTorch 与机器学习最基础内容开始，即便你是新手也能跟上。

然后会进入进阶主题，包括神经网络分类、PyTorch 工作流、计算机视觉、自定义数据集、实验追踪、模型部署，以及我最喜欢的迁移学习。

过程中你会围绕 FoodVision（食物图像分类模型）完成三个里程碑项目。

这些项目能帮助你练习重要概念，并沉淀一份可向雇主展示的作品集。

### 如何开始？

你可以在任意设备阅读，但最推荐在桌面浏览器中边看边敲代码。

课程使用免费工具 Google Colab。如果你没用过，建议先看 [Google Colab 入门教程](https://colab.research.google.com/notebooks/basic_features_overview.ipynb) 再回来继续。

开始步骤：

1. 点击上方任意章节链接，例如 "[00. PyTorch Fundamentals](https://www.learnpytorch.io/00_pytorch_fundamentals/)"。
2. 点击顶部的 "Open in Colab" 按钮。
3. 连按几次 SHIFT+Enter，观察执行结果。

### 我的问题没被覆盖怎么办？

欢迎在 [discussion](https://github.com/mrdbourke/pytorch-deep-learning/discussions) 留言，或邮件联系：daniel (at) mrdbourke (dot) com。

## Log

Almost daily updates of what's happening.

* 15 May 2023 - PyTorch 2.0 tutorial finished + videos added to ZTM/Udemy, see code: https://www.learnpytorch.io/pytorch_2_intro/
* 13 Apr 2023 - update PyTorch 2.0 notebook
* 30 Mar 2023 - update PyTorch 2.0 notebook with more info/clean code
* 23 Mar 2023 - upgrade PyTorch 2.0 tutorial with annotations and images
* 13 Mar 2023 - add starter code for PyTorch 2.0 tutorial 
* 18 Nov 2022 - add a reference for 3 most common errors in PyTorch + links to course sections for more: https://www.learnpytorch.io/pytorch_most_common_errors/ 
* 9 Nov 2022 - add PyTorch cheatsheet for a very quick overview of the main features of PyTorch + links to course sections: https://www.learnpytorch.io/pytorch_cheatsheet/ 
* 9 Nov 2022 - full course materials (300+ videos) are now live on Udemy! You can sign up here: https://www.udemy.com/course/pytorch-for-deep-learning/?couponCode=ZTMGOODIES7 (launch deal code valid for 3-4 days from this line)
* 4 Nov 2022 - add a notebook for PyTorch Cheatsheet in `extras/` (a simple overview of many of the most important functionality of PyTorch)
* 2 Oct 2022 - all videos for section 08 and 09 published (100+ videos for the last two sections)!
* 30 Aug 2022 - recorded 15 videos for 09, total videos: 321, finished section 09 videos!!!! ... even bigger than 08!!
* 29 Aug 2022 - recorded 16 videos for 09, total videos: 306
* 28 Aug 2022 - recorded 11 videos for 09, total videos: 290
* 27 Aug 2022 - recorded 16 videos for 09, total videos: 279
* 26 Aug 2022 - add finishing touchs to notebook 09, add slides for 09, create solutions and exercises for 09
* 25 Aug 2022 - add annotations and cleanup 09, remove TK's, cleanup images, make slides for 09
* 24 Aug 2022 - add annotations to 09, main takeaways, exercises and extra-curriculum done
* 23 Aug 2022 - add annotations to 09, add plenty of images/slides
* 22 Aug 2022 - add annotations to 09, start working on slides/images
* 20 Aug 2022 - add annotations to 09 
* 19 Aug 2022 - add annotations to 09, check out the awesome demos!
* 18 Aug 2022 - add annotations to 09 
* 17 Aug 2022 - add annotations to 09
* 16 Aug 2022 - add annotations to 09
* 15 Aug 2022 - add annotations to 09
* 13 Aug 2022 - add annotations to 09
* 12 Aug 2022 - add demo files for notebook 09 to `demos/`, start annotating notebook 09 with explainer text
* 11 Aug 2022 - finish skeleton code for notebook 09, course finishes deploying 2x models, one for FoodVision Mini & one for (secret)
* 10 Aug 2022 - add section for PyTorch Extra Resources (places to learn more about PyTorch/deep learning): https://www.learnpytorch.io/pytorch_extra_resources/ 
* 09 Aug 2022 - add more skeleton code to notebook 09
* 08 Aug 2022 - create draft notebook for 09, end goal to deploy FoodVision Mini model and make it publically accessible
* 05 Aug 2022 - recorded 11 videos for 08, total videos: 263, section 08 videos finished!... the biggest section so far
* 04 Aug 2022 - recorded 13 videos for 08, total videos: 252
* 03 Aug 2022 - recorded 3 videos for 08, total videos: 239
* 02 Aug 2022 - recorded 12 videos for 08, total videos: 236
* 30 July 2022 - recorded 11 videos for 08, total videos: 224
* 29 July 2022 - add exercises + solutions for 08, see live walkthrough on YouTube: https://youtu.be/tjpW_BY8y3g
* 28 July 2022 - add slides for 08
* 27 July 2022 - cleanup much of 08, start on slides for 08, exercises and extra-curriculum next
* 26 July 2022 - add annotations and images for 08
* 25 July 2022 - add annotations for 08 
* 24 July 2022 - launched first half of course (notebooks 00-04) in a single video (25+ hours!!!) on YouTube: https://youtu.be/Z_ikDlimN6A 
* 21 July 2022 - add annotations and images for 08
* 20 July 2022 - add annotations and images for 08, getting so close! this is an epic section 
* 19 July 2022 - add annotations and images for 08
* 15 July 2022 - add annotations and images for 08 
* 14 July 2022 - add annotations for 08
* 12 July 2022 - add annotations for 08, woo woo this is bigggg section! 
* 11 July 2022 - add annotations for 08 
* 9 July 2022 - add annotations for 08
* 8 July 2022 - add a bunch of annotations to 08
* 6 July 2022 - course launched on ZTM Academy with videos for sections 00-07! 🚀 - https://dbourke.link/ZTMPyTorch 
* 1 July 2022 - add annotations and images for 08 
* 30 June 2022 - add annotations for 08
* 28 June 2022 - recorded 11 videos for section 07, total video count 213, all videos for section 07 complete!
* 27 June 2022 - recorded 11 videos for section 07, total video count 202
* 25 June 2022 - recreated 7 videos for section 06 to include updated APIs, total video count 191
* 24 June 2022 - recreated 12 videos for section 06 to include updated APIs
* 23 June 2022 - finish annotations for 07, add exercise template and solutions for 07 + video walkthrough on YouTube: https://youtu.be/cO_r2FYcAjU
* 21 June 2022 - make 08 runnable end-to-end, add images and annotations for 07
* 17 June 2022 - fix up 06, 07 v2 for upcoming torchvision version upgrade, add plenty of annotations to 08
* 13 June 2022 - add notebook 08 first version, starting to replicate the Vision Transformer paper
* 10 June 2022 - add annotations for 07 v2
* 09 June 2022 - create 07 v2 for `torchvision` v0.13 (this will replace 07 v1 when `torchvision=0.13` is released)
* 08 June 2022 - adapt 06 v2 for `torchvision` v0.13 (this will replace 06 v1 when `torchvision=0.13` is released)
* 07 June 2022 - create notebook 06 v2 for upcoming `torchvision` v0.13 update (new transfer learning methods)
* 04 June 2022 - add annotations for 07
* 03 June 2022 - huuuuuuge amount of annotations added to 07 
* 31 May 2022 - add a bunch of annotations for 07, make code runnable end-to-end
* 30 May 2022 - record 4 videos for 06, finished section 06, onto section 07, total videos 186
* 28 May 2022 - record 10 videos for 06, total videos 182
* 24 May 2022 - add solutions and exercises for 06
* 23 May 2022 - finished annotations and images for 06, time to do exercises and solutions 
* 22 May 2202 - add plenty of images to 06
* 18 May 2022 - add plenty of annotations to 06
* 17 May 2022 - added a bunch of annotations for section 06
* 16 May 2022 - recorded 10 videos for section 05, finish videos for section 05 ✅
* 12 May 2022 - added exercises and solutions for 05
* 11 May 2022 - clean up part 1 and part 2 notebooks for 05, make slides for 05, start on exercises and solutions for 05
* 10 May 2022 - huuuuge updates to the 05 section, see the website, it looks pretty: https://www.learnpytorch.io/05_pytorch_going_modular/ 
* 09 May 2022 - add a bunch of materials for 05, cleanup docs
* 08 May 2022 - add a bunch of materials for 05
* 06 May 2022 - continue making materials for 05
* 05 May 2022 - update section 05 with headings/outline
* 28 Apr 2022 - recorded 13 videos for 04, finished videos for 04, now to make materials for 05
* 27 Apr 2022 - recorded 3 videos for 04
* 26 Apr 2022 - recorded 10 videos for 04
* 25 Apr 2022 - recorded 11 videos for 04
* 24 Apr 2022 - prepared slides for 04
* 23 Apr 2022 - recorded 6 videos for 03, finished videos for 03, now to 04 
* 22 Apr 2022 - recorded 5 videos for 03
* 21 Apr 2022 - recorded 9 videos for 03
* 20 Apr 2022 - recorded 3 videos for 03
* 19 Apr 2022 - recorded 11 videos for 03
* 18 Apr 2022 - finish exercises/solutions for 04, added live-coding walkthrough of 04 exercises/solutions on YouTube: https://youtu.be/vsFMF9wqWx0
* 16 Apr 2022 - finish exercises/solutions for 03, added live-coding walkthrough of 03 exercises/solutions on YouTube: https://youtu.be/_PibmqpEyhA
* 14 Apr 2022 - add final images/annotations for 04, begin on exercises/solutions for 03 & 04
* 13 Apr 2022 - add more images/annotations for 04
* 3 Apr 2022 - add more annotations for 04
* 2 Apr 2022 - add more annotations for 04
* 1 Apr 2022 - add more annotations for 04
* 31 Mar 2022 - add more annotations for 04
* 29 Mar 2022 - add more annotations for 04
* 27 Mar 2022 - starting to add annotations for 04
* 26 Mar 2022 - making dataset for 04
* 25 Mar 2022 - make slides for 03
* 24 Mar 2022 - fix error for 03 not working in docs (finally)
* 23 Mar 2022 - add more images for 03
* 22 Mar 2022 - add images for 03
* 20 Mar 2022 - add more annotations for 03
* 18 Mar 2022 - add more annotations for 03
* 17 Mar 2022 - add more annotations for 03 
* 16 Mar 2022 - add more annotations for 03
* 15 Mar 2022 - add more annotations for 03
* 14 Mar 2022 - start adding annotations for notebook 03, see the work in progress here: https://www.learnpytorch.io/03_pytorch_computer_vision/
* 12 Mar 2022 - recorded 12 videos for 02, finished section 02, now onto making materials for 03, 04, 05
* 11 Mar 2022 - recorded 9 videos for 02
* 10 Mar 2022 - recorded 10 videos for 02
* 9 Mar 2022 - cleaning up slides/code for 02, getting ready for recording
* 8 Mar 2022 - recorded 9 videos for section 01, finished section 01, now onto 02
* 7 Mar 2022 - recorded 4 videos for section 01
* 6 Mar 2022 - recorded 4 videos for section 01
* 4 Mar 2022 - recorded 10 videos for section 01
* 20 Feb 2022 - recorded 8 videos for section 00, finished section, now onto 01
* 18 Feb 2022 - recorded 13 videos for section 00
* 17 Feb 2022 - recorded 11 videos for section 00 
* 16 Feb 2022 - added setup guide 
* 12 Feb 2022 - tidy up README with table of course materials, finish images and slides for 01
* 10 Feb 2022 - finished slides and images for 00, notebook is ready for publishing: https://www.learnpytorch.io/00_pytorch_fundamentals/
* 01-07 Feb 2022 - add annotations for 02, finished, still need images, going to work on exercises/solutions today 
* 31 Jan 2022 - start adding annotations for 02
* 28 Jan 2022 - add exercies and solutions for 01
* 26 Jan 2022 - lots more annotations to 01, should be finished tomorrow, will do exercises + solutions then too
* 24 Jan 2022 - add a bunch of annotations to 01
* 21 Jan 2022 - start adding annotations for 01 
* 20 Jan 2022 - finish annotations for 00 (still need to add images), add exercises and solutions for 00
* 19 Jan 2022 - add more annotations for 00
* 18 Jan 2022 - add more annotations for 00
* 17 Jan 2022 - back from holidays, adding more annotations to 00 
* 10 Dec 2021 - start adding annotations for 00
* 9 Dec 2021 - Created a website for the course ([learnpytorch.io](https://learnpytorch.io)) you'll see updates posted there as development continues 
* 8 Dec 2021 - Clean up notebook 07, starting to go back through code and add annotations
* 26 Nov 2021 - Finish skeleton code for 07, added four different experiments, need to clean up and make more straightforward
* 25 Nov 2021 - clean code for 06, add skeleton code for 07 (experiment tracking)
* 24 Nov 2021 - Update 04, 05, 06 notebooks for easier digestion and learning, each section should cover a max of 3 big ideas, 05 is now dedicated to turning notebook code into modular code 
* 22 Nov 2021 - Update 04 train and test functions to make more straightforward
* 19 Nov 2021 - Added 05 (transfer learning) notebook, update custom data loading code in 04
* 18 Nov 2021 - Updated vision code for 03 and added custom dataset loading code in 04
* 12 Nov 2021 - Added a bunch of skeleton code to notebook 04 for custom dataset loading, next is modelling with custom data
* 10 Nov 2021 - researching best practice for custom datasets for 04
* 9 Nov 2021 - Update 03 skeleton code to finish off building CNN model, onto 04 for loading custom datasets
* 4 Nov 2021 - Add GPU code to 03 + train/test loops + `helper_functions.py`
* 3 Nov 2021 - Add basic start for 03, going to finish by end of week
* 29 Oct 2021 - Tidied up skeleton code for 02, still a few more things to clean/tidy, created 03
* 28 Oct 2021 - Finished skeleton code for 02, going to clean/tidy tomorrow, 03 next week
* 27 Oct 2021 - add a bunch of code for 02, going to finish tomorrow/by end of week
* 26 Oct 2021 - update 00, 01, 02 with outline/code, skeleton code for 00 & 01 done, 02 next
* 23, 24 Oct 2021 - update 00 and 01 notebooks with more outline/code
* 20 Oct 2021 - add v0 outlines for 01 and 02, add rough outline of course to README, this course will focus on less but better 
* 19 Oct 2021 - Start repo 🔥, add fundamentals notebook draft v0
