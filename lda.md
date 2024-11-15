# 线性判别分析（LDA, Linear Discriminant Analysis）

## 1. 概述
线性判别分析 (LDA) 是一种**监督学习**算法，用于解决**分类问题**。它旨在通过找到数据在特征空间中最佳的**投影方向**，使得不同类别之间的可分性最大化。LDA 假设各类样本服从相同方差的正态分布，并且不同类别之间的**均值不同**。它不仅可以用于降维，也可以用于分类任务。

## 2. 工作原理
LDA 通过寻找**线性组合**，使得：
- **类间方差（Between-class variance, Sb）最大化**，即不同类之间的分离度最大化；
- **类内方差（Within-class variance, Sw）最小化**，即同类内部的样本尽可能聚集。

具体来说，LDA 寻找一个投影方向，使得投影后**类内散布矩阵(Sw)** 最小，而**类间散布矩阵（Sb）** 最大。

### 2.1 类内散布矩阵 Sw
类内散布矩阵描述的是同一类样本的散布情况。计算公式为：

\[
S_w = \sum_{i=1}^C \sum_{x \in D_i} (x - \mu_i)(x - \mu_i)^T
\]

其中：
- \( C \) 是类别的数量；
- \( D_i \) 是类别 \( i \) 的样本集；
- \( \mu_i \) 是类别 \( i \) 的均值向量；
- \( x \) 是类别 \( i \) 中的样本。

### 2.2 类间散布矩阵 Sb
类间散布矩阵描述的是不同类的均值之间的分布情况。计算公式为：

\[
S_b = \sum_{i=1}^C N_i (\mu_i - \mu)(\mu_i - \mu)^T
\]

其中：
- \( N_i \) 是类别 \( i \) 的样本数量；
- \( \mu_i \) 是类别 \( i \) 的均值向量；
- \( \mu \) 是所有样本的全局均值向量。

### 2.3 优化目标
LDA 的优化目标是通过投影找到一个方向 \( w \)，使得以下准则最大化：

\[
J(w) = \frac{w^T S_b w}{w^T S_w w}
\]

这个目标函数表明，LDA 通过最大化类间距离（分子）和最小化类内散布（分母）来找到最优的投影方向。

## 3. 分类过程
LDA 分类器通过以下步骤进行分类：
1. **计算各类别的均值向量** \( \mu_i \)。
2. **计算类内散布矩阵** \( S_w \) 和 **类间散布矩阵** \( S_b \)。
3. 通过求解广义特征值问题，找到最佳的投影方向 \( w \)，即：

\[
S_w^{-1} S_b w = \lambda w
\]

4. **投影数据**：将数据点投影到找到的线性方向上，通常投影到 \( k-1 \) 个维度（\( k \) 是类别数）。
5. **进行分类**：基于投影后的距离或概率密度估计，对新的数据进行分类。

## 4. 与 PCA 的比较
LDA 与主成分分析 (PCA) 都是常用的**降维方法**，但它们有以下主要区别：
- **目标不同**：PCA 的目标是找到使得数据方差最大化的方向，而 LDA 的目标是找到能够最大化类别可分性的方向。
- **监督信息**：PCA 是无监督的，只关注特征间的方差；LDA 是监督的，利用了类别标签信息。
- **降维能力**：LDA 最多将数据降维到 \( k-1 \) 维（其中 \( k \) 是类别数），而 PCA 可以降到任意维数。

## 5. LDA 的假设
LDA 基于以下几个假设：
1. **特征是正态分布的**：每个类别的特征都服从多元正态分布。
2. **类别具有相同的协方差矩阵**：不同类别的样本具有相同的协方差矩阵。
3. **各类别的先验概率相同**：LDA 假设所有类别的样本数量大致相等。

## 6. LDA 的优缺点
### 优点：
- **简单有效**：在类别之间差异较大且数据满足正态分布的情况下，LDA 表现非常好。
- **降维与分类结合**：LDA 既可以用于降维，也可以用于分类。
- **对少量数据有良好表现**：LDA 在小数据集上往往表现优异。

### 缺点：
- **对正态性要求较高**：如果数据不满足正态分布假设，LDA 的性能会下降。
- **类别的协方差矩阵不同**：如果不同类别的协方差矩阵差异较大，LDA 的表现会变差。
- **无法处理非线性数据**：LDA 是一种线性模型，对于复杂的非线性数据，它的分类效果较差。

## 7. LDA 的扩展
除了传统的 LDA，还有一些常见的扩展版本：
- **QDA（Quadratic Discriminant Analysis）**：放松了 LDA 中类别共享同一协方差矩阵的假设，允许不同类别有不同的协方差矩阵。
- **核 LDA（Kernel LDA）**：通过核技巧将 LDA 扩展到非线性分类问题。



## 线性判别函数（Linear Discriminant Function）
线性判别分析（LDA）用于将数据点分到不同的类别。线性判别函数的形式为：
\[
f(\mathbf{x}) = \mathbf{w}^T \mathbf{x} + b
\]
其中：
- \( \mathbf{w} \) 是权重向量；
- \( \mathbf{x} \) 是输入特征向量；
- \( b \) 是偏置。

### 应用
主要用于二分类问题，通过寻找一个超平面来最大化两类之间的间隔。

## 二次判别函数（Quadratic Discriminant Function）
与线性判别函数不同，二次判别分析（QDA）允许使用二次函数来描述类别之间的关系，模型形式为：
\[
f(\mathbf{x}) = \mathbf{x}^T \mathbf{A} \mathbf{x} + \mathbf{b}^T \mathbf{x} + c
\]
其中 \( \mathbf{A} \) 是一个矩阵，允许非线性分割。

### 应用
适用于更复杂的分类问题，特别是当不同类别具有不同协方差矩阵时。

---

# 降秩线性判别分析（Reduced Rank Linear Discriminant Analysis）

## 定义
降秩线性判别分析是一种扩展的线性判别分析方法，通过降低特征空间的维度来提高计算效率和模型的可解释性。

## 目标
它试图在保留最大类间差异的同时，减少输入特征的数量。降秩方法通过最小化类内协方差和最大化类间协方差来实现。

## 应用
常用于高维数据集，例如基因表达数据或图像数据的分类，适用于特征数量大于样本数量的情况。

---
