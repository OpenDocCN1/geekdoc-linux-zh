
现在我们准备好拟合一些模型。在开始之前，我们需要为特征矩阵添加列名，因为 `caret` 需要这些：

```r
colnames(x) <- 1:ncol(mnist$train$images)
colnames(x_test) <- colnames(mnist$train$images)
```

让我们从 `knn` 开始。第一步是针对 K 进行优化。记住，当我们运行算法时，我们必须计算测试集中每个观测值与训练集中每个观测值之间的距离。这是一项大量的计算工作。我们将使用 k 折交叉验证来提高速度。

如果我们运行代码，在标准笔记本电脑上的计算时间将是几分钟。

```r
control <- trainControl(method = "cv", number = 10, p = .9)
train_knn <- train(x[,,col_index], y,
  method = "knn",
  tuneGrid = data.frame(k = c(3,5,7)),
  control = control)
```

通常情况下，最好用数据子集运行一次，以便对时间有个概念，在开始运行可能花费许多小时才能完成之前。我们可以这样做：

```r
n <- 1000
b <- 2
index <- sample(row(x), n)
control <- trainControl(method = "cv", number = b, p = .9)
train_knn <- train(x[index, col_index], y,
  method = "knn",
  tuneGrid = data.frame(k = c(3,5,7)),
  control = control)
```

我们可以增加 `n` 和 `b` 以建立一个它们如何影响计算时间的模式，从而得到一个想法。

## 第 33 章
## 实践中的机器学习

现在我们已经学习了几种方法并并通过说明性示例对它们进行了探索，我们将在一个真实案例上尝试它们：MNIST 数字数据集。

我们可以使用以下 `dslabs` 包来加载这些数据：

```r
library(tidytverse)
library(dslabs)
mnist <- read_mnist()
```

该数据集包含两个部分：训练集和测试集：

```r
names(mnist)
# [1] "train" "test"
```

每个部分都包含一个列为特征的矩阵：

```r
dim(mnist$train$images)
# [1] 60000 784
```

以及一个类标签为整数的向量：

```r
class(mnist$train$labels)
# [1] "integer"
table(mnist$train$labels)
#
# 0 1 2 3 4 5 6 7 8 9
# 5923 6742 7958 6131 5842 5421 5918 6265 5851 5949
```

由于我们希望这个示例能在笔记本笔记本上运行并在一小时内完成，我们将考虑数据集的一个子集。我们将从训练集中采样 10000 行随机行，并从测试集中采样 1000 行随机行：

```r
set.seed(1990)
index <- sample(nrow(mnist$train$images), 10000)
x <- mnist$train$images[index,]
y <- factor(mnist$train$labels[index])
```

```r
index <- sample(nrow(mnist$test$images), 1000)
x_test <- mnist$test$images[index,]
y_test <- factor(mnist$test$labels[index])
```

### 33.1 预处理

在机器学习中，我们通常会在运行算法之前对预测器进行转换。我们还会移除显然无用的预测器。我们将这些步骤称为预处理。

预处理的示例包括标准化预测器、对某些预测器取对数变换、移除与其他高度相关的预测器，以及移除非唯一值非常少或方差接近零的预测器。我们在下面展示了一个示例。

我们可以运行 `caret` 包中的 `nearZero` 函数，可以看到某些特征在观测值之间变化不大。我们可以看到有大量特征的变异数为0：

```r
library(matrixStats)
sds <- colSds(x)
qplot(sds, bins = 256)
```

![](img/276727cd0f1f6fea60002e6d839d370a_561_0.png)

这是预之中的，因为图像的部分很少包含写入（黑色像素）。

`caret` 包包含一个函数，可以推荐由于近零方差而移除的特征：
```r
library(caret)
zv <- nearZeroVar(x)
```

我们可以看到建议移除的列：

```r
image(matrix(1:784 %in% nzv, 28, 28))
```

### 33.2 K近邻算法和随机森林

所以我们最终保留了这些列数：

```r
col_index <- setdiff(1:ncol(x), nzv)
length(col_index)
# [1] 249
```

现在我们准备好拟合一些模型。在开始之前，我们需要为特征矩阵添加列名，因为 `caret` 需要这些：

```r
colnames(x) <- 1:ncol(mnist$train$images)
colnames(x_test) <- colnames(mnist$train$images)
```

让我们从 `knn` 开始。第一步是针对 K 进行优化。记住，当我们运行算法时，我们必须计算测试集中每个观测值与训练集中每个观测值之间的距离。这是一项大量的计算工作。我们将使用 k 折交叉验证来提高速度。

如果我们运行代码，在标准笔记本电脑上的计算时间将是几分钟。

```r
control <- trainControl(method = "cv", number = 10, p = .9)
train_knn <- train(x[,,col_index], y,
  method = "knn",
  tuneGrid = data.frame(k = c(3,5,7)),
  control = control)
```

通常情况下，最好用数据子集运行一次，以便对时间有个概念，在开始运行可能花费许多小时才能完成之前。我们可以这样做：

```r
n <- 1000
b <- 2
index <- sample(row(x), n)
control <- trainControl(method = "cv", number = b, p = .9)
train_knn <- train(x[index, col_index], y,
  method = "knn",
  tuneGrid = data.frame(k = c(3,5,7)),
  control = control)
```

我们可以增加 `n` 和 `b` 以建立一个它们如何影响计算时间的模式，从而得到一个想法。

## 33.5. 集成

- Pr(7)=1 但实际为 2
- Pr(1)=1 但实际为 7
- Pr(3)=1 但实际为 8
- Pr(1)=1 但实际为 6

![](img/276727cd0f1f6fea60002e6d839d370a_566_0.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_1.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_2.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_3.png)

- Pr(1)=1 但实际为 7
- Pr(7)=1 但实际为 8
- Pr(6)=1 但实际为 9
- Pr(9)=1 但实际为 4

![](img/276727cd0f1f6fea60002e6d839d370a_566_4.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_5.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_6.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_7.png)

- Pr(7)=1 但实际为 9
- Pr(1)=1 但实际为 4
- Pr(1)=1 但实际为 9
- Pr(9)=1 但实际为 4

![](img/276727cd0f1f6fea60002e6d839d370a_566_8.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_9.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_10.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_11.png)

这些是随机森林的错误：

- Pr(9)=0.63 但实际为 4
- Pr(5)=0.59 但实际为 3
- Pr(2)=0.57 但实际为 7
- Pr(0)=0.56 但实际为 9

![](img/276727cd0f1f6fea60002e6d839d370a_566_12.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_13.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_14.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_15.png)

- Pr(9)=0.49 但实际为 4
- Pr(9)=0.48 但实际为 4
- Pr(6)=0.46 但实际为 9
- Pr(2)=0.45 但实际为 7

![](img/276727cd0f1f6fea60002e6d839d370a_566_16.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_17.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_18.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_19.png)

- Pr(1)=0.44 但实际为 2
- Pr(9)=0.44 但实际为 4
- Pr(7)=0.43 但实际为 2
- Pr(0)=0.42 但实际为 6

![](img/276727cd0f1f6fea60002e6d839d370a_566_20.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_21.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_22.png)
![](img/276727cd0f1f6fea60002e6d839d370a_566_23.png)

## 33.5 集成

集成（ensemble）的思想类似于结合来自不同投票者的数据，以对每个候选人的真实支持率获得更好的估计。在机器学习中，通过结合不同算法的结果可以大幅提高最终结果。这是一个简单的示例，我们通过取随机森林和 KNN 的平均值来计算类别概率。我们可以看到准确率提高到了 0.96：

```r
p_rf <- predict(fit_rf, x_test[,col_index])
p_rf <- p_rf / rowSums(p_rf)
p_knn <- predict(fit_knn, x_test[,col_index])
p <- (p_rf + p_knn)/2
y_pred <- factor(apply(p, 1, max))
_confusionMatrix(y_pred, y_test)$["Accuracy"]
# 0.96
```

## 33.6 练习

在练习中，我们将使用 mnist27 数据来构建模型。

1. 使用 caret 包中的模型：
```r
models <- c("glm", "naive_bayes", "svmLinear", "gbboost", "qda", "knn", "cbf", "ranger", "svrf", "mlp", "adaboost", "gbm", "svmRadial")
```
2. 现在你有了模型列表，使用 apply 创建测试集的预测。你应该得到一个具有 `length(mnist27$test)` 行 `length(models)` 列的矩阵。

3. 计算每个模型在测试集上的准确率。

4. 通过多数投票构建一个集成。

5. 之前我们计算了训练集上的准确率。哪些方法比集成好？

6. 移除表现不佳的方法并重新集成。将这些估计保存到一个对象中。

7. 集成的准确率是多少？0.88

8. 高级：如果两个方法的结果相同，计算它们相同的百分比。然后使用 `method = "binary"` 参数通过热图函数可视化结果。

9. 高级：注意每个方法也可以产生估计概率。对于大多数方法，我们在调用 train 时可以使用 `type = "prob"`。但某些方法如果类别不是数字将无法工作。提示：这样修改 level：

```r
dat$trainy <- recode_factor(dat$trainy, "2"="two", "7"="seven")
dat$testy <- recode_factor(dat$testy, "2"="two", "7"="seven")
```

10. 在本章中，我们在 MNIST 的子集上演示了几个机器学习算法。尝试对整个数据集拟合模型。

# 第34 章 大型数据集

机器学习问题通常涉及与 MNIST 一大或更大的数据集。有很多计算技术和统计概念适用于分析大型数据集。在本章中，我们将通过描述矩阵代数、降维、正则化和矩阵分解来接触这些技术和概念。我们建议使用电影评分作为启发示例。

## 34.1 矩阵代数

在机器学习中，所有预测变量均为数值或可以以有意义的方式转换为数值的情况是非常常见的。数字数据集就是一个例子：每个像素记录 0 到 255 之间的数字。让我们加载数据：

在这些情况下，通常将预测变量存储在矩阵中，结果存储在向量中，而不是数据框。你可以看到是以矩阵形式存储的：

```r
class(mnist$images)
# [1] "matrix"
```

这个矩阵代表 60,000 个数字，对于本章中的示例，我们将采取更具操作性的子集。我们将选取前 1,000 个预测变量 x 和 y：

```r
x <- mnist.train.images[1:1000,]
y <- mnist.train.labels[1:1000]
```

## 第 34 章 大数据集

$\mathbf{X} = [X_1 X_2] = \begin{pmatrix} x_{1,1} & x_{1,2} \\ \vdots & \vdots \\ x_{N,1} & x_{N,2} \end{pmatrix}$

矩阵的**维度**是确保某些操作可以执行所需的的重要特征。维度是一个由两个数字组成的摘要，定义为行数 × 列数。在 R 中，我们可以使用 `dim` 函数提取矩阵的维度：

```
dim(x)
# [1] 1000 784
```

向量可以被看作 $N \times 1$ 矩阵。然而，在 R 中，向量没有维度：

```
dim(x_1)
# NULL
```

我们使用 `as.matrix` 函数将向量显式转换为矩阵：

```
as.matrix(x_1)
# [1] 5 1
```

我们可以使用这种表示法通过以下 $N \times p$ 矩阵来表示任意数量的预测变量，例如当 $p = 784$ 时：

$\mathbf{X} = \begin{pmatrix} x_{1,1} & \dots & x_{1,p} \\ x_{2,1} & \dots & x_{2,p} \\ \vdots & \vdots & \vdots \\ x_{N,1} & \dots & x_{N,p} \end{pmatrix}$

我们将其存储在 x 中：

```
dim(x)
# [1] 1000 784
```
