## 摘要
+ 本文重点研究了协同过滤算法的推荐原理，对其推荐的流程做出了详细分析。
+ + 发现协同过滤算法没有考虑共同评价的项目的个数因素对推荐结果的影响，但论文[\[1\]][1]中有考虑到该因素，且是2017.8.2被期刊接收。
##### 因此本文对皮尔逊相关系数进行改进，通过引入惩罚因子，吧共同评价的项目的个数因素考虑进来，对共同评价项目少的用户或者商品采用惩罚因子降低其相似度，通过实验对比，验证了改进后的皮尔逊相关系数公式能明显提高推荐的准确率。

## 第一章 绪论
### 1.1 推荐系统的研究背景及意义
#### 1.1.1 推荐系统的兴起
#### 1.1.2 推荐系统研究意义

### 1.2 推荐系统国内外研究现状
#### 1.2.1 国外研究现状
数据稀疏性和冷启动问题
#### 1.2.2 国内研究现状
### 1.3 本文研究内容
+ 针对CF算法中存在的推荐准确率不够高，评分信息的稀疏性以及系统的“冷启动”等问题提出一些改进思路及解决方案。

## 第二章 相关技术
### 2.1 传统推荐算法概述
#### 2.1.1 基于人口统计学的推荐
+ 核心思想
+ + 根据用户基本信息来发现信息相近的用户，进而推荐这些用户喜欢的物品。
+ + ![基于人口统计学原理图](assets/markdown-img-paste-20190324160510889.png)

#### 2.1.2 基于内容的推荐
+ 核心思想
+ + 根据用户的喜好的历史数据，找到用户喜欢的物品，通过物品的本质内容（也称元数据），来找到物品的类似物品进而对用户进行推荐。
+ + ![基于内容的原理图](assets/markdown-img-paste-20190324160856384.png)
+ + 基于内容的推荐不需要其他用户的数据，可以很好（在一定程度上吧！！！）地避免数据稀疏性问题。

#### 2.1.3 基于关联规则地推荐
+ <big>是一个经典的数据挖掘问题 </big>
+ + 主要挖掘数据间的一些依赖关系
+ 核心思想
+ + 挖掘出不同商品间的关联性，以此来进行推荐。

#### 2.1.4 基于协同过滤的推荐
+ <big>凭借着出色的速度和健壮性取得了非常大的成功，无论它推荐的个性化程度还是自动化程度都非常地高，并且具有强大地处理非结构化对象的能力和发现兴趣的能力，这使得协同过滤算法成为目前应用最成功最广泛的推荐算法之一 </big>

#### 2.1.5 基于组合模型的推荐
+ 常见的组合方法
+ + 混合加权
+ + 混合切换
+ + 混合分区
+ + 混合分层

### 2.2 卷积神经网络相关理论
#### 2.2.1 局部连接和权值共享
+ （1）局部连接
+ + 在卷积神经网络中，每层的神经元只与其输入层的神经元相连接
+ + ![神经元局部连接](assets/markdown-img-paste-20190324163046802.png)
+ + 在一定程度上减少过拟合
+ （2）权值共享
+ + 指同层神经元，在对输入层的数据进行特征提取的时候，虽然神经元与输入层连接的区域不同，但对于各自连接的区域，所有的升级元共享一组权重。
+ + ![权重共享](assets/markdown-img-paste-20190324163637120.png)

#### 2.2.2 卷积神经网络模型训练
<big>一般情况下使用***有监督***的方式进行训练，其训练过程就是使用大量带有标签的数据经过反向传播对网络中的权值进行更新。</big>
+ CNN核心思想
+ + 根据一定的方式对网络中的权值进行初始化，比如按照平均分布对模型中的权值进行随机的赋值，然后利用输入数据在神经网络中的前向传播，获得一个预期的结果，假如这一个预期的结果和数据的真实标签不一样，那么就通过误差反向逐层的传递来使各层的神经元对网络中的权值进行学习。

### 2.3 本章小结

## 第三章 协同过滤推荐算法研究
### 3.1.1 数据介绍
### 3.1.2 数据分析处理
<big>**数据预处理**原因是想要数据的价值得到进一步的提升，这样才能使数据的准确度更高，进而提高算法的准确率，使数据挖掘的过程变得顺利</big>
+ 数据处理技术
+ + 1.数据清洗
+ + + 空缺值得填充、数据重复去除、无效数据得清理、异常值得识别与纠正
+ + 2.数据变换
+ + + ？？？？？？

### 3.2 基于用户得协同过滤推荐算法
#### 3.2.1 算法原理
+ ![UserCF原理](assets/markdown-img-paste-20190324165517821.png)
<big>计算相似度的方法</big>
+ + 1）余弦相似度/性
+ + + 通过两个空间向量之间的夹角来判断两者之间的相似程度。其夹角越小表示相似度越高
+ + 2）皮尔逊相关系数
+ + + 判断两组数据与某一直线拟合程度的一种度量。皮尔逊相关系数将用户的评分值也考虑进去，而余弦相似度并没有。
+ + 3）欧式距离向量

#### 3.2.2 算法实现
![UserCF流程图](assets/markdown-img-paste-20190324170834293.png)
+ 根据用户相似度矩阵，出去user1本身，找到相似度最高的用户作为邻居，根据邻居的评价列表生成推荐列表，在相似用户评价过的电影中去掉看过的电影，剩下的就是推荐给用户的列表。
+ 将评分信息文件按一定比例比如3：1分训练集rating_train.csv和测试集rating_test.csv。利用训练集数据计算用户相似度，并对用户进行推荐，将推荐列表在测试集上进行比较，一次计算出具体的推荐的准确率。

<big>***推荐结果量化指标***</big>
+ 1）准确率
+ + 用来对检索或者分类结果的质量做一个评价。
+ + 准确率通常指使搜索出的有关结果的数量与搜索出的结果总数量的比值。
+ 2）召回率
+ + 通常以推荐的商品列表中的商品在测试集中存在的个数与测试集中商品的总数量的比值作为召回率。
+ 3）覆盖率
+ + 表示推荐列表L中不一样的影片数量与训练集影片库中影片总个数的比值。

#### 3.2.3 算法改进

### 3.3 基于物品的协同过滤推荐算法
#### 3.3.1 算法原理
#### 3.3.2 算法实现
#### 3.3.3 算法改进


## 第四章 基于VGG16卷积神经网络特征提取的推荐
### 4.1 数据介绍及数据处理
利用CGG16卷积神经网络们模型对商品的图像信息进行特征提取，根据提取到的图像特征找到类似的商品，以此对用户进行推荐。
### 4.2 VGG16 模型结构
#### 4.2.1 卷积层
+ 卷积过程使将输入数据相应的位置与卷积核相应的位置相乘并将结果相加。

#### 4.2.2 池化层
+ 平均池化和最大池化两种方式
+ 核心功能是降维、线性不变性
+ 利用池化的方式可以将卷积层提取到的特征压缩并尽量保留重要特征。

#### 4.2.3 全连接层
+ 通常出现在卷积层和池化层之后，在整个网络中用于对提取到的特征进行分类。
+ + 全连接，即上层的任意一个神经元都和其下层的所有神经元相连

#### 4.2.4 softmax层
+ 末尾是一个softmax回归分类器。

### 4.3 VGG16特征提取
+ 由于仅用VGG16模型进行特征提取而不需要进行分类，故舍弃模型后面的全连接层和softmax层。

#### 4.3.1 数据输入
+ 该模型是以张量的形式作为输入数据的，张量，其实是n维矩阵的抽象，一维的张量其实和平时常用的向量概念相同，二位张量则类似于矩阵的形式，一次类推。

#### 4.3.2 卷积

#### 4.3.3 池化

### 4.4 相似计算并推荐

### 4.5 本章小结

## 第五章 基于卷积神经网络图像分类的推荐
+ 在训练的过程中，网络会自动提取所需要的特征数据

### 5.1 数据介绍及数据处理

### 5.2 建立模型
#### 5.2.1 模型选取
+ ![深度卷积神经网络模型信息表](assets/markdown-img-paste-20190325095654195.png)
+ ![续上表](assets/markdown-img-paste-20190325095741775.png)

#### 5.2.2 过拟合问题

#### 5.2.3 激活函数
+ 是一个卷积神经网络模型必不可少的一部分

### 5.3 模型训练
+ 在训练时采用随机梯度下降法（SGD，Stochastic Gradient Descent)
+ 大多数监督学习模型，为了得到最优权值，需对模型创建代价损失函数，然后选择合适的优化算法以得到最小的函数损失值[33]。

### 5.4 结果与分析
### 5.5 本章小结


# <big>**补充知识**:</big>
### 1.倒排表



[1]: https://www.sciencedirect.com/science/article/pii/S0020025517308629
