## 深度学习模型的典型例子
>前馈深度网络或多层感知机（multilayer perceptron, MLP）
>> 多层感知机仅仅是一组输入值映射到输出值的数学函数。该函数由许多较简单的函数组合构成。

## 学习数据正确表示的想法是解释深度学习的一个视角
## 另一个视角是深度能够让计算机学习一个多步骤的计算机程序

## 深度学习软件库
> Theano
>>(Bergstra et al. 2010a;Bastien et al,2012a)

> PyLearn2
>>(Goodfellow et al,2013e)

> Torch
>>(Collobert et al, 2011b)

> DistBelief

> Caffe

> MXNet

> TensorFlow

## 范数
> $L^p$ 范数
>> $$ \|x\|_p = (\sum_i|x_i|^p)^{\frac{1}{p}}$$
>>
> 其中 $p \in R,p \geq 1$

## 要把最小化或最大化的函数称为
> 目标函数 objective function
>
> 准则 criterion
### 要对其进行最小化时，把它称为
> 代价函数 cost function
>
> 损失函数 loss function
>
> 误差函数 error function

### 传统地
#### 监督学习
> 回归、分类、结构化输出问题
#### 无监督学习
> 其他任务地密度估计
