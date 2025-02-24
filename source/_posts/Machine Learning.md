---
title: Machine Learning
date: 2025-02-07 21:31
categories: Machine Learning and AI Studies
tags:
    - "Machine Learning"
excerpt: false
---

### Data is crucial in ML.

Finding the right data is challenging!!!

#### Popular ML datasets

* MNIST: **digits written** by employees of the US Census Bureau
* ImageNet: millions of **images** from image search engines 
* AudioSet: YouTube sound clips for **sound classification** 
* LibriSpeech: 1000 hours of English speech from **audiobook** 
* Kinetics: YouTube videos clips for **human actions** classification 
* KITTI:  traffic scenarios recorded by cameras and other sensors 
* Amazon Review: customer reviews and from Amazon online shopping 
* SQuAD: question-answer pairs derived from Wikipedia

#### Where to find Datasets

* Paperswithcodes Datasets: academic datasets with leaderboard 
* Kaggle Datasets: ML datasets uploaded by data scientists 
* Google Dataset search: search datasets in the Web 
* Various toolkits datasets: tensorflow, huggingface 
* Various conference/company ML competitions 
* Open Data on AWS: 100+ large-scale raw data 
* Data lakes in your own organization

|                      | Pros                           | Cons                                                 |
| -------------------- | ------------------------------ | ---------------------------------------------------- |
| Acadamic datasets    | Clean,proper difficulty        | Limited choices, too simplified, usually small scale |
| Competition datasets | Closer to real ML applications | Still simplified, and only available for hot topics  |
| Raw Data             | Great flexibility              | Needs a lot of effort to process                     |

Generate Synthetic Datasets

* Use GANs (This is a picture generate app.)
* Simulation
* Data augmentations (such as PS operate)

#### Data Labeling

##### Semi-Supervised Learning (SSL) -- 半监督学习

Focus on the scenario where there is a **small amount of labeled data**, along with **large amount of unlabeled data**

Make assumptions on data distribution to use unlabeled data 

* Continuity assumption（连续性）: examples with similar features are more likely to have the same label 。-- 相似样本相同标注
* Cluster assumption（聚类）: data have inherent cluster structure, examples in the same cluster tend to have the same label 
* Manifold assumption（流形假设）: data lie on a manifold of much **lower dimension** than the input space。尽管数据可能存在于一个高维空间中，但它们的本质结构可以用一个低维空间来描述。例如，尽管一张图片可能有数千个像素（高维），但这些像素之间的关系可能可以用一个低维的流形来表示。

###### Self-training

Purpose:Generate labels for unlabeled data using a self-training model.

![self-training](img/img-ML/1.png)

现在更广泛的做法是外包（Crowdsourcing）进行数据标注。可以使用Active Learning方法选择出最不确性的样本进行外包标注（不确性采样）

![Mix model](img/img-ML/2.png)

#### Weak supervision

Less accurate than manual ones, but good enough for training

##### Data programming

Domain specific heuristics to assign labels（人为的设定标准进行启发式标注）

#### Data clean

##### Data Errors

* Consequences: 
  * The training may still converge, but slower 
  * Accuracy degradation, could be hard to detect 
  * Deploying these models may impact the quality of the new collected data 

* Types of Data Errors

  * Outliers（离散）: data values that significantly deviate from other observations 

  ![Outliers](img/img-ML/3.png)

  * Rule violations: data values violate integrity constraints such as “Not Null” and “Must be unique” and “Non negative” 
    * Rule-based Detection. x -> y的对应关系被打破
    * Denial constraints.基于规则的检测。一些数据必须满足的某些规则
  * Pattern violations: data values violate syntactic and semantic constraints such as formatting, misspelling
    * Syntactic patterns（句法） 。e.g. eng, en, english -> English
    * Semantic patterns（语义）。e.g.  Values in column “Country” need have capitals, so a value “Stanford” is invalid

#### Data Transformation

Normalization 归一化处理

| Normalization Technique   | Formula                                                      |
| ------------------------- | ------------------------------------------------------------ |
| **Min-max Normalization** | $$x_i' = \frac{x_i - \min_x}{\max_x - \min_x}(b-a) + a$$     |
| **Z-score Normalization** | $$x_i' = \frac{x_i - \text{mean}(\mathbf{x})}{\text{std}(\mathbf{x})}$$ |
| **Decimal Scaling**       | $$x_i' = \frac{x_i}{10^j} \quad \text{smallest } j \text{ s.t. } \max(\|\mathbf{x}'\|) < 1$$ |
| **Log Scaling**           | $$x_i' = \log(x_i)$$                                         |

**Z-score 归一化（Z-score normalization）** 后，数据会转换为一个均值为 **0**、标准差为 **1** 的分布。这种分布通常被称为 **标准正态分布**（Standard Normal Distribution），也称为 **Z 分布**。

**Min-max 归一化（Min-max Normalization）** 是一种线性变换方法，将数据缩放到一个指定的范围（通常是 [a,b][*a*,*b*]，默认是 [0,1][0,1]）。归一化后的数据分布形状不变，但数值范围被限制在 [a,b][*a*,*b*] 之间。

**Decimal Scaling（十进制缩放）** 是一种数据归一化方法，通过将数据除以一个适当的 10j10*j* 值，将数据缩放到 [−1,1][−1,1] 区间。这种方法的核心思想是根据数据的最大值来确定缩放因子 10j10*j*，使得缩放后的数据绝对值小于 1。

##### Image Transformations

* cropping, downsampling, compression （Save storage cost, faster loading at training）
* **Be aware of lossy compression** 。高质量的图片会显著的影响模型精度

##### Video Transformations

* 权衡 Preprocessing to **tradeoff** storage, quality and loading speed。
* 有压缩算法，导致读取困难。

##### Text Transformations

* Stemming and lemmatization（词根化语法化）: a word -->a common base form.  E.g. am, are, is --> be；car, cars, car's, cars' --> car
* Tokenization: text string --> a list of tokens (smallest unit to ML algorithms)

#### Feature Engineering（特征工程）

抽取数据特征。旨在从原始数据中提取更具代表性和区分度的特征，以提升模型性能和降低计算复杂度。常见使用已经预训练好的神经网络模型进行训练，采用倒数第二层的向量作为特征。

### Machine Learning

#### Types of ML Algorithms

* Supervised ：完全依赖**有标签数据**（即每个样本都有对应的标签）进行模型训练。
  * self-supervised：通过数据的内在结构自动生成标签（即“伪标签”）
* Semi-supervised：**结合使用少量有标签数据 + 大量无标签数据**进行训练，通过无标签数据辅助提升模型性能。
* unsupervised：训练无标注的数据。为了聚类等目的
* Reinforcement learning：模型与环境交互，学习交互，进行奖励。常见，机器人

#### Components in Supervised Training

* Model：output predicts from inputs
  * Decision tree:Use trees to make decisions
  * Linear methods:Use trees to make decisions
  * Kernel machine:Use kernel functions to compute feature similarities
  * Neural Networks（神经网络）:Use neural networks to learn feature representations
* Loss：Measure difference between predicts and ground truth labels。
* Objective：minimize the sum of lossews over examples
* Optimization：The algorithm for solving the objective

#### Decision Tress models

Use a top-down approach, staring from the root node with the set of all features

* Pros
  * **Explainable**(可解释性！！！)
  * Can handle both numerical and categoricasl
* Cons
  * Very non-robust.(不稳定！换了数据节点可能改变)
  * Complex trees cause overfitting (过拟合)
  * Not easy to be parallelized（并行计算） in computing

提升树模型的效果：

1. Random Forest（随机森林）：训练多个树，多个树结果一起进行，稳定性提升。其中的随机来自于随机取样替换、随机特征集

2. Gradient Boosting Decision Trees：顺序训练多棵树（根据残差），多棵树合在一起组成一个大树

#### Linear Methods

$$y = w_1x_1+w_2x_2+\dots+w_3x_3+b$$,不同特点加权重加偏移b

问题如何用它进行分类，向量输出

模型求解方法：Mini-batch Stochastic gradient descent(SGD) -- 小梯度随机下降

#### Neural Networks

对原始数据进行特征提取

* Multilayer perceptions （多层感知机，MLP）-- 多层非线性变换来解决复杂问题
  * **输入层**：接收原始数据（例如图像的像素、文本的特征）。
  * **隐藏层**（至少一层）：每个神经元对输入进行加权求和，再通过**非线性激活函数**（如ReLU、Sigmoid）处理（拟合复杂函数），提取高层次特征。
  * **输出层**：根据任务类型输出结果（例如分类用Softmax，回归用线性输出）。
* Convolutional neural networks（卷积）
  * 将MLP的Dense layer（全连接层） --> Convolution layer 
  * 通过**局部感知**（并未对整个数据进行每层，而是从一个kXk的窗口进行线性计算）和**参数共享**（小范围窗口的权重保留用到平移窗口之后，底层设计：同一物体在不同位置能被识别）高效提取空间特征
  * 因为卷积操作对于位置是敏感，加入**池化层（Pooling Layer）**，降低特征图尺寸，增强平移不变性。
* Recurrent neural networks（循环）
  * **通过循环结构捕捉序列中的时序依赖关系**，常用于language model中的下一个词（时序）
  * 隐藏层
  * 需要有效的处理遗忘
* Transform
  * **自注意力机制（Self-Attention）**

### Evaluation Metrics

#### Underrating & Overfitting

* Training error: model error on the training data
* Generalization error: model error on new data。模型泛化能力

|                           | Low training error | High training error |
| ------------------------- | ------------------ | ------------------- |
| Low Generalization error  | Good               | Bug？               |
| High Generalization error | Overfitting        | Underfitting        |

* Model Complexity

模型可以拟合各种各样模型的能力

![Model_Complexity](img/img-ML/4.png)

* Data Complexity

Multiple factors matters

* Model Complexity vs Data Complexity

![model_vs_data](img/img-ML/5.png)

**Pick a model with a proper complexity for your data**

#### Estimiate Generalization Error

Approximated by the error on a holdout **test dataset**, which has never been seen by the model and can be only used once.

**Validation dataset**: 训练数据集一部分，可以使用多次

Split your data into “train” and “valid” sets (often calls “test”)

用验证数据集的指标代替泛化的指标

* 数据独立同分布才可以使用随机分
* 有时序等特征等信息的数据不能随机

**K-fold Cross Validation**

![k-fold](img/img-ML/6.png)

### Model Combination 

#### Bias & Variance（偏差、方差）

![Bias](img/img-ML/7.png)

![Bias](img/img-ML/8.png)

模型泛化误差：每次训练模型与真实值之间的差+每次训练出来的模型与平均模型的差别（方差）+噪音

![Bias](img/img-ML/9.png)

* Reduce bias
  * A more complex model
  * Boosting
    * **顺序训练多个弱模型**，每个模型专注于修正前一个模型的错误，每一个新模型都试图拟合前一个模型的残差（即真实值与当前集成模型的预测值之差），从而逐步减少偏差。
    * 策略类似于梯度下降
    * Gradient Boosting Decision Trees (GBDT)
* Reduce variance
  * A simpler model
  * Bagging -- \- Bootstrap AGGregatING
    * Bagging 主要针对高方差模型（如未剪枝的决策树，unstable model），通过集成降低方差，但对偏差影响较小。
    * 从原始数据集中有放回地抽取多个子集（每个子集大小与原始数据相同，但包含重复样本）。
    * 独立训练n个模型（权重不share）。

Stacking策略：串联多个模型，每个模型训练数据包括原始与前一层的模拟数据，最终用一个全连接层输出。

![Bias](img/img-ML/10.png)

### Model Tuning

* 调参，Start with a good baseline. Tune a value, retrain the model to see the changes. 每次调一个值，重新训练，看训练集情况。
* tenesorboard  and weights & bias看每一层的连接与调参记录

#### Automated Machine Learning

* Hyperparameter optimization (HPO): find a good set of hyperparameters through search algorithms

  * Black-box：一个超参数组合进去，一个模型评估值出来。不管什么优化。适用性强

  * Multi-fidelty：modifies the training job to speed up the search

  * Bayesian Optimization (BO)：Iteratively learn（迭代） a mapping from HP to objective function. Based on previous trials. Select the next trial based on the current estimation. 

    ![贝叶斯](img/img-ML/11.png)

  * Successive Halving（连续去半）：每次淘汰一半，仅继续训练高的一半。

    ![](img/img-ML/12.png)

  * Hyperband：跑多次SH

* Neural architecture search (NAS): construct a good neural network model 

  * NAS with Reinforcement Learning

### Deep Network Tuning

#### Normalization

数据进行标准化（均值为0，方差为1），缓解梯度消失/爆炸问题，加速模型收敛

- **批量归一化（Batch Normalization, BN）**：对每个批次的每个通道进行归一化，适用于CNN。精度的影响不大，影响训练速度
- **层归一化（Layer Normalization, LN）**：对单个样本的所有神经元归一化，适用于RNN/Transformer。

#### Residual Connection

引入跳跃连接（Skip Connection），将输入直接叠加到网络层的输出，解决深度网络的梯度消失和模型退化问题。典型应用如ResNet。

#### Attention Mechanism

注意力机制通过动态分配权重聚焦关键信息，增强模型对长距离依赖和重要特征的捕捉能力。核心是**查询（Query）、键（Key）、值（Value）**的三元组计算

### Transfer Learning

从一个地方学到的模型可以扩展到别的领域。

#### Fine-Tuning techniques

抽象地认为，多层神经网络过程是由小见大的抽象过程，我们想要从一个更大的神经网络完成一个小的任务的时候，认为权重、结构已经抽象出来蕴含在大任务中。因此，保留最后一层之外的所有层与权重，重新训练最后一层可以让大任务模型完成小任务。这也是称为微调。

![](img/img-ML/13.png)

### NLP fine-tuning

在自然语言处理（NLP）中，**微调（Fine-tuning）** 是指对预训练模型（如BERT、GPT等）进行针对性调整，使其适应特定下游任务（如文本分类、问答、命名实体识别等）的过程。

**BERT（Bidirectional Encoder Representations from Transformers）** 是一种基于Transformer架构的预训练语言模型，BERT支持的格式（如 `[CLS] + 文本A + [SEP] + 文本B + [SEP]`）

1. **双向上下文编码**：通过掩码语言模型（Masked Language Model, MLM）同时学习左右上下文信息。
2. **通用表征能力**：在大规模无标注语料（如Wikipedia）上预训练，捕捉通用的语言规律。

微调方法：与上面类似

![](img/img-ML/14.png)
