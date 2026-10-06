
`mean(y_hat == test_set$sex)`

# [1] 0.819

我们看到这个数值比训练集上观察到的准确率略低，但仍然优于随机猜测。通过在没有训练过的数据集上进行测试，我们知道结果并不是由于刻意挑选了一个良好的结果得到的。

#### 28.4.3 混淆矩阵

上一节开发的预测规则是：如果学生身高超过 65 英寸，则预测为男性。考虑到平均女性约为 65 英寸，这个预测似乎是错误的。发生了什么？如果一个学生的高度与平均女性相同，我们不应该预测为女性吗？

总而言之，总体准确率可能是一个误导性的指标。为了观察这一点，我们将开始构建所谓的“混淆矩阵”，这是一个汇总了预测值和实际值每种组合的基本表格。我们可以在 R 中使用以下表格来实现：

```
table(predicted = y_hat, actual = test_set$sex)
```

#>
# predicted Female Male
# Female 69 45
# Male 50 361

# 第 28 章 机器学习导论

如果我们仔细观察这个表，它它揭示了一个问题。如果我们分别计算每个性别的准确率，会得到：

```
test_set %>%
  mutate(y_hat = y_hat) %>%
  group_by(sex) %>%
  summarize(accuracy = mean(y_hat == sex))
```

# A tibble: 2 × 2
# sex accuracy
# <fct> <dbl>
# 1 Female 0.580
# 2 Male 0.889

男性和女性的准确率存在不平衡：太多的女性被预测为男性。我们几乎把一半的女性预测成了男性！我们的总体准确率怎么能这么高？这是因为这个数据集中男性比例很高。这些身高是从三门科学课程收集的，其中两门课程男性学生较多：

```
prev <- mean(y == "Male")
prev
# [1] 0.73
```

因此，在计算准确率时，男性错误的高昂成本被男性预测正确的收益所抵消了。这在机器学习中实际上可能是一个大问题。如果你的训练数据在某些方面存在偏差，我们很可能会开发出同样有偏差的算法。使用测试集这一事实并不重要，因为它也源于原始的偏偏数据集。这就是为什么在评估机器学习算法时，我们关注的指标远多于总体准确率。

我们可以使用几种指标来评估算法，使患病率不会遮盖我们的评估，而所有这些都可以从混淆矩阵推导出。使用准确率的一种通用改进方法是专门研究灵敏性和特异性。

#### 28.4.4 敏感性与特异性

为了定义敏感性和特异性，我们命名一个二分类结果。当结果是分类的，我们可以为特定类别定义这些术语。在数字中，我们可以询问在正确预测 2 而非其他数字的情况下的特异性。一旦我们指定了感兴趣的类别，我们就可以讨论正性结果（Y = 1）和负性结果（Y = 0）。

通常，敏感性定义为算法在实际结果为正时预测为正的能力：即当 Y = 1 时 $\hat{Y} = 1$。因为一个分类所有内容（无论如何 $\hat{Y} = 1$）的算法具有完美的敏感性，因此该指标本身不足以判断算法。因此，我们还解释了特异性，它通常定义为算法在实际结果不是正性（Y = 0）时不预测为正性的能力。我们可以总结如下：

- 敏感性 (Sensitivity): Y = 1 => $\hat{Y}$ = 1
- 特异性 (Specificity): Y = 0 => $\hat{Y}$ = 0

另一种定义特异性的方法是实际为正的预测正结果的比例：

- 特异性: Y = 1 => Y = 1。

为了提供精确的描述，我们命名混淆矩阵的四个条目：

| | 实际正性 (Actually Positive) | 实际负性 (Actually Negative) |
| :--- | :--- | :--- |
| 预测正性 (Predicted positive) | 真正性 (TP) | 假正性 (FP) |
| 预测负性 (Predicted negative) | 假负性 (FN) | 真负性 (TN) |

敏感性通常通过 TP/(TP + FN) 量化，即实际正性（第一列 TP + FN）被分类为正（TP）的比例。这个数量被称为真阳率 (TPR) 或召回率 (recall)。

特异性通常量化为 TN/(TN+FP)，即负性（第二列 = FP+TN）中预测为负的（TN）的比例。这个数量也称为真负率 (TNR)。另一种量化特异性的方法是 TP/(TP+FP)，即预测为正（第一行 TP+FP）中实际为正（TP）的比例。这个数量被称为精确率 (precision)，与召回率不同，精确率取决于患病率，因为较高的患病率意味着即使是随机猜测也能获得较高的精确率。

多个名称可能会让人困惑，因此我们使用表格来帮助记忆这些术语。表格包含一列，如果我们把比例视为概率，它显示了定义。

| 指标 | 名称 1 | 名称 2 | 定义 | 概率表示 |
| :--- | :--- | :--- | :--- | :--- |
| 敏感性 (Sensitivity) | 真阳率 (TPR) | 召回率 (Recall) | TP/TP+FP | Pr($\hat{Y}=1|Y=1$) |
| 特异性 (Specificity) | 真负率 (TNR) | 1 - 假阳率 (1-FPR) | TN/TN+FP | Pr($\hat{Y}=0|Y=0$) |
| 特异性 (Specificity*) | 预测预测值 (PPV) | 精确率 (Precision) | TP/TP+FP | Pr(Y=1|Y=1) |

*\*注：原文表格最后一行误写为 Specificity，应为 Precision。* 

`caret` 函数 `confusionMatrix` 为我们计算所有这些指标。

## 28.4. 评估指标

![](img/276727cd0f1f6fea60002e6d839d370a_468_0.png)

我们看到它在 $F_1$ 值处达到最大：

```r
max(F_1)
# [1] 0.627
```

当我们使用以下截断值时，达到了这个最大值：

```r
best_cutoff <- cutoff.which.max(F_1)
best_cutoff
# [1] 65
```

截断值为65比64更意义意义。然而，它平衡了我们混淆矩阵的特异性（specificity）和灵敏度（sensitivity）：

```r
y_hat <- ifelse(test_set$height > best_cutoff, "Male", "Female") %>%
  factor(levels = test_set$sex)
sensitivity(data = y_hat, reference = test_set$sex)
# [1] 0.58
specificity(data = y_hat, reference = test_set$sex)
# [1] 0.89
```

我们现在看到我们的表现远好于猜测，灵敏度和特异性都相对较高，而且我们构建了第一个机器学习算法。它接受一个预测因子，如果你身高在65英寸或更短，则预测为女性。

### 28.4.6. 流行率在实践中的重要性

当流行率接近0或1时，灵敏度和特异性极高的机器学习算法在实践中可能并用。为了说明这一点，考虑一位研究罕见病的医生，他兴趣开发一个预测谁患病的算法。医生与你分享数据，你开发了一个灵敏度极高的算法。你解释说，如果患者患病，算法可能会预测正确。你告诉医生，根据分析的数据，你也很担心有两个患者患病：Pr($\hat{Y} = 1$)。医生既不担心也不惊讶，并解释重要的是测试的精确率（precision）：Pr($Y=1$|$\hat{Y}=1$)。使用贝斯定理，我们可以将两者联系起来：

```r
Pr($Y=1$|$\hat{Y}=1$) = Pr($\hat{Y}=1$|$Y=1$) / Pr($\hat{Y}=1$)
```

医生知道该病的流行率是每1000人5例，这意味着 Pr(Y = 1)/Pr(Y-1) = 1/100，因此你的算法的精确率小于0.01。医生觉得你的算法没有太大用。

### 28.4.7 ROC 精确率召回率曲线

在比较两种方法（猜测与身高截断）时，我们查看了准确率和 $F_1$。第二方法明显优于第一种。然而，虽然我们为第二方法考虑了几个截断值，但对于第一种，我们只考虑了一种方法：等概率猜测。注意，以较高概率猜测男性将由于样本中的偏差而给我们带来准确率：

```r
p <- 0.9
n <- length(test_index)
y_hat <- sample("Male", "Female"), n, replace = TRUE, prob=c(p, 1-p)) %>%
  factor(levels = levels(test_set$sex))
mean(y_hat == test_set$sex)
# [1] 0.726
```

但是，如上所述，这将以较低灵敏度为代价。我们在本节描述的曲线将帮助我们看到这一点。

记住，对于这些参数中的每一个，我们都可以获得不同的灵敏度和特异性。由于这个原因，评估方法的一种常用方法是通过绘图进行图形比较。

一种广泛使用的图表是*受试者工作*（ROC）曲线。如果你好奇这个名字来自哪里，可以咨询 ROC 的维基百科。

ROC曲线绘制了灵敏度（TPR）与1 - 特异性或假阳性率（FPR）的关系。这里是使用不同概率概率猜测的ROC曲线：

```r
probs <- seq(0, length.out = 10)
guessing <- map_df(probs, function(p){
  y_hat <- sample("Male", "Female"), n, replace = TRUE, prob=c(p, 1-p)) %>%
    factor(levels = c("Female", "Male"))
  list(method = "Guessing",
           FPR = 1 - specificity(y_hat, test_set$sex),
           TPR = sensitivity(y_hat, test_set$sex))
})
guessing %>% qplot(FPR, TPR, data = , xlab = "1 - Sensitivity", ylab = "Sensitivity")
```

## 28.4. 评估指标

![](img/276727cd0f1f6fea60002e6d839d370a_470_0.png)

猜测的所有ROC曲线看起来像一条直线。我们的第二种方法如何？我们可以为基于身高的方法构建一条曲线：

```r
offs <- c(50, seq(60, 75), 80)
height_cutoff <- map_df(cutoffs, function(x){
  y_hat <- ifelse(test_set$height > x, "Male", "Female") %>%
    factor(levels = c("Female", "Male"))
  list(method = "Height cutoff",
         FPR = 1 - specificity(y_hat, test_set$sex),
         TPR = sensitivity(y_hat, test_set$sex))
})
```

通过绘制两条曲线，我们可以比较不同特异性值的灵敏度：

```r
bind_rows(guessing, height_cutoff) %>%
  ggplot(aes(FPR, TPR)) +
  geom_point() +
  xlab("1 - Sensitivity") +
  ylab("Sensitivity")
```

![](img/276727cd0f1f6fea60002e6d839d370a_470_1.png)

| method |
|---|
| Guessing |
| Height cutoff |

我们可以看到这种方法在所有情况下获得更高的灵敏度，这实际上意味着更好的方法。在制作ROC曲线时，添加截断值到点上：

```r
library(ggplot2)
map_df(cutoffs, function(x) {
  y_hat <- ifelse(test_set$height > x, "Male", "Female") %>%
    factor(levels = c("Female", "Male"))
  list(method = "Height cutoff",
       cutoff = x,
       FPR = 1-specificity(y_hat, test_set$sex),
       TPR = sensitivity(y_hat, test_set$sex))
}) %>%
  ggplot(aes(FPR, TPR)) +
  geom_line() +
  geom_point(nudge_x = 0.01, nudge_y = -0.01)
```

ROC曲线有一个缺点，即指标依赖于流行率。在流行率重要的情况下，我们应该绘制精确率-召回率图。思路是类似的，但我们改为绘制精确率相对于：

```r
guessing <- map_df(probs, function(p){
  y_hat <- sample("Male", "Female"), length(test_index),
    replace = TRUE, prob=c(p, 1-p)) %>%
    factor(levels = c("Female", "Male"))
  list(method = "Guess",
    recall = sensitivity(y_hat, test_set$sex),
    precision = precision(y_hat, test_set$sex))
})
height_cutoff <- map_df(cutoffs, function(x){
  y_hat <- ifelse(test_set$height > x, "Male", "Female") %>%
    factor(levels = c("Female", "Male"))
  list(method = "Height cutoff",
    recall = sensitivity(y_hat, test_set$sex),
    precision = precision(y_hat, test_set$sex))
})
```

## 28.4. 评估指标

```r
bind_rows(guessing, height_cutoff) %>%
  ggplot(aes(recall, precision, color = method)) +
  geom_line() +
  geom_point()
```

![](img/276727cd0f1f6fea60002e6d839d370a_472_0.png)

从这张图中我们可以看到猜测的精确率并不高。这是因为流行率很低。

如果我们位置更改为男性而不是女性，ROC曲线保持不变，但精确率-召回率曲线：

```r
guessing <- map_df(probs, function(p){
  y_hat <- sample("Male", "Female"), length(test_index),
  replace = TRUE, prob=c(p, 1-p)) %>%
    factor(levels = c("Male", "Female"))
  list(method = "Guess",
    recall = sensitivity(y_hat, test_set$sex),
    precision = precision(y_hat, test_set$sex))
})
height_cutoff <- map_df(cutoffs, function(x){
  y_hat <- ifelse(test_set$height > x, "Male", "Female") %>%
    factor(levels = c("Male", "Female"))
  list(method="Height cutoff",
    recall = sensitivity(y_hat, test_set$sex),
    precision = precision(y_hat, test_set$sex))
})
bind_rows(guessing, height_cutoff) %>%
  ggplot(aes(recall, precision, color = method)) +
  geom_line() +
  geom_point()
```

## 第 28 章 机器学习导论

![](img/276727cd0f1f6fea60002e6d839d370a_473_0.png)

#### 28.4.8 损失函数

为止现在，我们描述了特别适用于分类数据的评估指标。具体来说，对于二分类结果，我们描述了灵敏度、准确率和 $F_1$ 如何用于定量。然而，这些指标对于连续结果没有用。在本节中，我们描述机器学习中定义“最佳”的通用方法是定义一个*损失函数*，它可以应用于分类数据和连续数据。

最常用的损失是平方函数。如果 $\hat{y}$ 是你的预测因子，$y$ 是观测结果，那么平方损失函数简单为：

$(\hat{y} - y)^2$

由于我们经常有一个包含许多观测值的测试集（例如 $N$），我们使用均方误差（MSE）：

$MSE = \frac{1}{N}RSS = \frac{1}{N}\sum_{i=1}^{N}(\hat{y}_i - y_i)^2$

在实践中，我们报告均方根误差，因为它与结果的单位相同：

$RMSE = \sqrt{\frac{1}{N}\sum_{i=1}^{N}(\hat{y}_i - y_i)^2}$

## 28.5. 练习
