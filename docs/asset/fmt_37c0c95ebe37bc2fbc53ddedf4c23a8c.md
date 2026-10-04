
# 室内导航机器学习实战

## 列表 1：数据准备

```python
# 读取数据
import numpy as np
import pandas as pd

fn = "https://archive.ics.uci.edu/machine-learning-databases/0022/wifi_localization.txt"
columns = [0, 1, 2, 3, 4, 5, 6, 'Target']
df = pd.read_csv(fn, header=None, names=columns, comment='#', sep='\t')

mapping = {1: 'Kitchen', 2: 'Hallway', 3: 'Livingroom', 4: 'Patio'}
df['Target'] = df['Target'].map(mapping)

print(df)
df.describe()
```

在分配房间时查找任何错误。本文介绍了如何基于 Python 工具，使用无监督和有监督机器学习进行室内导航。通过关注机器学习技术，我们将详细介绍本研究中使用的 Python 库。

为了演示目的，我们使用了加利福尼亚大学欧文分校（UCI）网站提供的免费数据集 [1]。UCI 无线定位数据集由使用手机测量的七个 WLAN 热点信号以及测量位置组成。在进行 500 次测量后，所有测试条目都是可靠的。在我们的场景中，所有坐标最初都是未知的，包括发射信标的位置。测量了信号衰减。我们可以定义任意两列之间的距离。然而，过度估计会破坏估计的准确性。请记住，我并不期望找到 Tom 在地理经纬上的精确位置——我只想找到正确的房间。

## 探索性数据分析

开始之前，我需要准备数据（列表 1）。此前，UCI 数据集是平衡的，但包含无效值或零值。列表 1 列出了第一个 pandas 数据库，它支持数据处理。`read_csv()` 函数读取本地文件，或如列表所示的互联网资源。

## 列表 2：绘制信号强度分布

```python
dh = df[df['Target'] == 'Kitchen']
df.drop(columns=['Target'], axis=1)
df.plot.hist(bins=50)
df.show()
```

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | Target |
|---|---|---|---|---|---|---|---|---|
| 0 | -64 | -56 | -61 | -66 | -72 | -81 | -82 | Kitchen |
| 1 | -68 | -57 | -61 | -66 | -77 | -81 | -85 | Kitchen |
| 2 | -63 | -60 | -60 | -67 | -76 | -85 | -84 | Kitchen |
| 3 | -68 | -63 | -60 | -62 | -72 | -79 | -80 | Kitchen |
| 4 | -63 | -65 | -60 | -63 | -73 | -77 | -81 | Kitchen |

## 图 3：pandas DataFrame 的前四行。

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | |
|---|---|---|---|---|---|---|---|---|
| mean | -52.23050 | 2000.00000 | 2000.00000 | 2000.00000 | -53.94650 | -54.98400 | -62.42650 | -80.98599 | -81.72600 | 2500.00000 |
| std | 11.32172 | 3.41768 | 5.51616 | 11.41792 | 9.50950 | 6.51672 | 11.81142 | 19.18123 | | | |
| 25% | -55.00000 | -58.00000 | -58.00000 | -56.00000 | | | | | | |

*(注：提示中的剩余 OCR 文本包含大量的伪影和乱码数据。已对源文本中的连贯部分进行了处理。)*

## 列表 3：准备分类器

```python
# 01 将数据划分为特征和目标
# 02 (列号)
# 03
# 04 X = df.iloc[:, 0:-1].to_numpy()
# 05 y = df.iloc[:, -1].to_numpy()
# 06
# 07 划分为训练集和测试集
# 08
# 09 from sklearn.model_selection import train_test_split
# 10
# 11 X_train, X_test, y_train, y_test = train_test_split(X, y)
# 12
# 13 选择模型和行
# 14 # (更改行号)
# 15
# 16 from sklearn.ensemble import RandomForestClassifier
# 17
# 18 classifier = RandomForestClassifier()
# 19 classifier.fit(X_train, y_train)
```

## 列表 4：评估分类器性能

```python
# 预测并评估
from sklearn.metrics import confusion_matrix

y_pred = classifier.predict(X_test)
labels = classifier.classes_
cm = confusion_matrix(y_test, y_pred, labels=labels)
print(np.trace(cm)/cm.shape[0])
pd.DataFrame(cm, index=labels, columns=columns)
```

作为输入值。我们用它来寻找 Tom。为了确定测量的质量，我们将目标与 `y_pred` 进行比较，后者是 `predict()` 函数预测的值。偏差是衡量分类器质量的指标。

混淆矩阵（图 7）显示了目标值。它从类属性获取名称顺序。属性遵循 scikit-learn 库中类结尾的常用惯例，以这种方式映射所有值。事实上，Tom 被错误地识别为客厅有 14 次（其中 8 次），客厅被误认为是 Tom 有 2 次。

## 列表 5：Tom 在哪里？

```python
ptom = [-85, -52, -58, -49, -62, -79, -85]
print('Tom is here:', 'Living Room')
array = predict(ptom)
print('Error ', classifier.predict_proba(ptom))
```

重新审视这个问题：混淆矩阵的值被用来创建一个数字。如果 500 个值被错误分配，根据准确率 $1-120/500 = 0.76$ 计算。如果有 13 个小数字不在那里，结果将是 8.74。决策的缺陷在具体案例中可能存在问题，但在统计学上是不确定的。最好，你可以将误差限制在。

我几乎找到 Tom 了。他的智能手机显示了他周围的 WiFi 网络字段（图 1）。决策树对该位置在客厅进行了分类（列表 5）。

不仅 `predict()` 函数揭示了程度，`predict_proba()` 还显示了整体的一致性。每种情况下都是 77%。在 `RandomForestClassifier` 的默认设置中，100 棵决策树相互计数，每种情况下有 77 个，露台 18 个。如果通过 `n_estimators=1000` 将计数增加到 1000，结果将是 789/1000 和 1663/1000。这种风格可能存在不确定性，但它比解析方法好得多（参见侧边栏示例“求解解析解”）。

## 评估属性

许多学习方法依赖决策树是有原因的。决策树对以下内容具有鲁棒性。

## 列表 6：分类器的属性

```python
fi = classifier.feature_importances_
print('Feature importance:', fi)
csel = np.where(fi>0.09)
df.drop(df.columns[csel], axis=1).drop(df)
```

图 7：混淆矩阵阐明了预测质量。

```python
# 输出：
# 特征重要性:
# array([0.25828451, 0.00111624, 0.09085321, 0.21282642, 0.24906961, 0.01037945, 0.07719417])
```

LINUX-MAGAZINE.COM | 期 255 | 2022年2月 | 41

## 深度机器学习

以 89% 的概率位于客厅。冗余数据不会影响机器学习的准确性，因为检测冗余是训练的一部分。如果冗余数据减慢了学习过程或属性中存在矛盾的数据，情况则不同。我将使用其他不仅简单选择属性，而是尝试组合它们的方法。

我将自己限制在 K-Means 分类器 [4]。字母 K 表示与 K-最近邻算法的相似性，该算法搜索 k 个最近邻。K 将数据划分并优化 k 个质心，使得点到其各自质心的平方距离保持最小。尽管这可以通过 sklearn 的几行代码即可进行编程实现 [5] (9)。

**图 8：** 多边定位的原理。

## 无监督学习

到为止，我假设我已知每个元素的位置。如果由于数据不足以推导出没有矛盾的陈述，导致我感到困惑该怎么办？在无监督学习中，我们将相似的房间和时间进行归类。

# 深度解析

## 机器学习

### 代码列表 11: K-Means 结果

```python
from sklearn.metrics import silhouette_score

print('Input data:', X.shape)
print('Inertia:', kmeans.inertia_, .1f)
print('Silhouette score:', silhouette_score(X, kmeans.labels_), .1f)
print('New labels:', np.unique(kmeans.labels_))
cluster_centers = kmeans.cluster_centers_
print('Center of gravity:', cluster_centers_)
```

### 代码列表 13: 寻找最佳聚类数量

```python
wcss = []
for i in range(2, 11):
    kmeans = KMeans(n_clusters=i, init='k-means++', max_iter=10, random_state=0)
    kmeans.fit(X)
    wcss.append(kmeans.inertia_)
plt.plot(range(2, 11), wcss)
plt.title('Elbow Method')
plt.xlabel('Number of clusters')
```

### 代码列表 12: K-Means 典型输出

```
Input data: (2000, 7)
Inertia: 246781.7
Silhouette: 0.410238827317094
New labels: [0 1 2 ...]
Center of gravity: [[25.39058824 ...]]
```

## 隐藏空间

代码列表 11 提供了关于分配质量的统计信息。代码列表 12 显示了典型的输出。输出中的惯性（inertia）反映了聚类的紧凑性。点应该紧密地聚集在聚类中心。距离越小，轮廓系数对相邻聚类的考虑就越理想。相邻聚类越远，聚类的边界就越清晰。

轮廓值介于 1（最优）和 -1 之间。第二行数据显示数据包含了四个聚类之外的大部分点。通过探索聚类数量（从 2 到 9），K-Means 识别了图 1 顶部的点集。无监督学习连接了在监督学习中看到的变量。代码列表 13 计算了不同聚类的惯性并进行了绘图。最佳值是最小聚类大小。肘部法（Elbow Method）是斜率开始变平缓的点。具有低肘部的线条聚类数量为 4 或 5。代码列表 14 显示了每个聚类的轮廓系数。

## 数据清洗

如果属性和目标之间存在关系，数据就是冗余的。使用无监督学习发现冗余（例如，在获取数据时出错）。行 4 显示输入为 pandas DataFrame，并将数据分配到四个聚类之一。但哪些是聚类？k=3 给出了子集。平均值由垂直线表示。每个数据集的轮廓值表示为水平条形。条形末端显示了值的波动。

### 代码列表 14: 寻找平均轮廓值

```python
from sklearn.metrics import silhouette_score
```
