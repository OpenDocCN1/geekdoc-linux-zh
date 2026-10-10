

### 训练算法

借助 Scikit-Learn 库，我们很容易训练 KNN 算法。首先，让我们从 Scikit-Learn 库中导入 `KNeighboursClassifier`：

```python
from sklearn.neighbors import KNeighboursClassifier
```

以下代码将帮助我们训练该算法：

```python
knn_classifier = KNeighboursClassifier(n_neighbors=5)
knn_classifier.fit(X_train, y_train)
```

请注意，我们创建了该类的一个实例，并将该实例命名为 `knn_classifier`。我们在实例化过程中使用了一个参数，即 `n_neighbors`。我们将该参数的值设为 5，这基本上代表 K 的值。需要注意的是，K 没有特定的固定值，它是在测试和评估之后选择的。不过，作为起步，5 是大多数 KNN 应用中最常用的值。

然后，我们可以使用测试数据来进行预测。这可以通过运行下面的脚本来实现：

```python
pred_y = knn_classifier.predict(X_test)
```

### 评估准确率

KNN 算法的评估方式与线性回归算法准确度的评估方式不同。之前我们使用过诸如 RMSE、MAE 等指标。在这种情况下，我们将使用混淆矩阵、精确率、召回率和 f1 分数等指标。我们可以使用 `classification_report` 和 `confusion_matrix` 方法来计算这些指标。让我们首先从 Scikit-Learn 库中导入这些方法：

```python
from sklearn.metrics import confusion_matrix, classification_report
```

运行以下脚本：

```python
print(confusion_matrix(y_test, pred_y))
print(classification_report(y_test, pred_y))
```

上述结果表明，KNN 算法在分类我们测试数据集中的 30 条记录时表现良好。结果显示，该算法在数据集上的平均准确率约为 90%。这并不是一个糟糕的比例。

### K-Means 聚类

让我们在 Scikit-Learn 中实现该算法之前，先手动演示一下该算法是如何工作的：

假设我们有一个名为 D 的二维数据实例，如下所示：

```python
D = ((2,3), (10,12), (12,13), (5,8), (30,42), (82,30), (1,80), (80,3), (2,25), (80,81))
```

我们的目标是根据数据点之间的相似度对数据进行分类。

我们应该首先初始化两个簇的质心值，并且这应该是随机进行的。簇 C1 和 C2 的质心分别命名为 c1 和 c2，我们将用前两个数据点的值进行初始化，即 (5,3) 和 (10,15)。在这之后，你应该开始迭代。每当计算欧几里得距离时，应将该数据点分配给欧几里得距离最短的簇。

让我们以数据点 (5,3) 为例：

```text
与簇质心 c1 = (5,3) 的欧几里得距离 = 0
与簇质心 c2 = (10,15) 的欧几里得距离 = 13
```

该数据点相对于质心 c1 的欧几里得距离比相对于质心 c2 的距离更短。这意味着该数据点将被分配到簇 C1。

如果数据点相对于质心 c2 的距离更短，那么它将被分配到簇 C2。

现在数据点已经被分配到正确的簇中，下一步应该涉及计算新的质心值。这些值应通过确定属于某个簇的数据点坐标的均值来计算。

例如，假设对于 C1，我们向该簇分配了以下两个数据点：

(5, 3) 和 (24, 10)。

新的 x 坐标值将是这两个值的均值：

x = (5 + 24) / 2
x = 14.5

新的 y 值将是：

y = (3 + 10) / 2
y = 13/2
y = 6.5

c1 的新质心值将是 (14.5, 6.5)。

对 c2 也应执行相同操作，并重复整个流程。迭代应重复进行，直到质心值不再更新为止。这意味着，例如，如果你进行了三次迭代，你可能会发现第四次迭代中质心 c1 和 c2 的更新值与第三次迭代中的值相等。这意味着你的数据无法进一步聚类。

你现在已经熟悉 K-Means 算法的工作方式了。让我们讨论一下如何在 Scikit-Learn 库中实现它。让我们首先导入我们需要使用的所有库：

```python
import matplotlib.pyplot as plt
import numpy as np
from sklearn.cluster import KMeans
```

#### 数据准备

我们现在需要准备要使用的数据。我们将创建一个总共包含 10 行和 2 列的 numpy 数组。那么，我们为什么选择使用 numpy 数组呢？这是因为 Scikit-Learn 库可以直接处理 numpy 数组数据输入，而无需预处理。

#### 可视化数据

现在我们有数据了，我们可以创建一个图表，查看数据点的分布情况。这样我们就能知道目前是否存在任何簇：

```python
plt.scatter(X[:,0], X[:,1], label="True Position")
plt.show()
```

该代码生成了以下图表：

![](img/e34dde0654d255bebea353c553e965ac_79_0.png)

如果我们用肉眼观察，我们可能会从上述数据中划分出两个簇，一个在底部包含五个点，另一个在顶部包含五个点。现在我们需要调查 K-Means 聚类算法是否也会这样做。

#### 创建簇

我们已经看到可以从数据点中形成两个簇，因此 K 的值现在为 2。可以通过运行以下代码创建这两个簇：

```python
kmeans_clusters = KMeans(n_clusters=2)
kmeans_clusters.fit(X)
```

我们创建了一个名为 `kmeans_clusters` 的对象，并将 2 用作参数 `n_clusters` 的值。然后，我们对该对象调用了 `fit()` 方法，并将我们在 numpy 数组中拥有的数据作为参数传递给该方法。

现在我们可以查看算法为最终簇创建的质心值：

```python
print(kmeans_clusters.cluster_centers_)
```

这返回以下内容：

上面的第一行给出了第一个质心的坐标，即 (16.8, 17)。第二行给出了第二个质心的坐标，即 (70.2, 74.2)。如果你遵循了手动计算这些值的过程，它们应该是相同的。这表明 K-Means 算法运行良好。

以下脚本将帮助我们查看数据点标签：

```python
print(kmeans_clusters.labels_)
```

这返回以下内容：

上述输出显示了一个包含 10 个元素的一维数组，这些元素对应分配给 10 个数据点的簇。你可以清楚地看到，我们首先有一系列零，这表明前 5 个点被聚为一类，而后 5 个点也被聚为一类。请注意，0 和 1 没有数学意义，它们只是用来表示簇 ID。如果我们有三个簇，那么最后一个簇将用 2 来表示。

现在我们可以绘制数据点，查看它们是如何被聚类的。我们需要将数据点及其分配标签一起绘制，以便能够区分簇。只需执行下面给出的脚本：

```python
plt.scatter(X[:, 0], X[:, 1], c=kmeans_clusters.labels_, cmap='rainbow')
plt.show()
```

该脚本返回以下图表：

![](img/e34dde0654d255bebea353c553e965ac_80_0.png)

我们仅仅将名为 X 的数组的第一列与第二列进行了绘制。同时，我们将 `kmeans_clusters.labels_` 作为参数 c 的值传入，该参数对应于标签。请注意参数 `cmap='rainbow'` 的使用。该参数帮助我们选择不同数据点的颜色类型。

