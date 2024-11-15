# Logistic 回归（Logistic Regression）

**This is used for classification.**
## 1. 定义
Logistic 回归是一种用于分类问题的统计方法，尤其适用于二分类问题。它通过对输入特征进行线性组合，并使用逻辑函数（Sigmoid 函数）将结果映射到 \( (0, 1) \) 的区间，从而预测某个事件发生的概率。

## 2. 逻辑函数（Sigmoid 函数）
Logistic 回归模型的核心是逻辑函数，其数学表达式为：
\[
h(\mathbf{x}) = \frac{1}{1 + e^{-\mathbf{x}^T \beta}}
\]
其中：
- \( \mathbf{x} \) 是输入特征向量；
- \( \beta \) 是模型参数向量。

## 3. 模型公式
Logistic 回归模型可以用以下公式表示：
\[
P(Y=1 | \mathbf{x}) = h(\mathbf{x}) = \frac{1}{1 + e^{-(\beta_0 + \beta_1 x_1 + \beta_2 x_2 + \ldots + \beta_n x_n)}}
\]
其中 \( P(Y=1 | \mathbf{x}) \) 是给定特征 \( \mathbf{x} \) 下事件 \( Y=1 \) 的概率。

## 4. 代价函数
Logistic 回归使用对数似然函数作为代价函数，目的是最大化给定数据的似然性。代价函数可以表示为：
\[
J(\beta) = -\frac{1}{m} \sum_{i=1}^{m} \left[ y^{(i)} \log(h(\mathbf{x}^{(i)})) + (1 - y^{(i)}) \log(1 - h(\mathbf{x}^{(i)})) \right]
\]
其中：
- \( m \) 是样本数量；
- \( y^{(i)} \) 是第 \( i \) 个样本的真实标签。

## 5. 优化算法
通常使用梯度下降法或其变种（如随机梯度下降）来最小化代价函数，进而估计模型参数 \( \beta \)。

## 6. 预测
使用训练好的 Logistic 回归模型进行预测时，通常设置一个阈值（例如 0.5）来判断类别：
- 如果 \( P(Y=1 | \mathbf{x}) \geq 0.5 \)，则预测为类 1；
- 如果 \( P(Y=1 | \mathbf{x}) < 0.5 \)，则预测为类 0。

## 7. 优点和缺点
### 优点
- 简单易懂，易于实现；
- 适用于线性可分的数据；
- 可以通过正则化来防止过拟合。

### 缺点
- 对于非线性问题表现不佳；
- 对异常值敏感。

## 8. 总结
Logistic 回归是一种强大的分类工具，适合处理二分类问题。通过合理的特征选择和参数调整，可以在许多实际应用中表现良好。
