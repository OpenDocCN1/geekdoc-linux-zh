

点击“播放”按钮，然后等待观看一个酷炫的动画。请注意最右侧的输出。经过一段时间后，会出现如下内容：

![](img/e34dde0654d255bebea353c553e965ac_64_0.png)

![](img/e34dde0654d255bebea353c553e965ac_64_1.png)

连接线的清晰度以及其他特征都在增加。请记住，输出中有一个清晰的蓝色区域。

这可能是一个分类问题，其中蓝色点属于 A 类，而橙色点属于 B 类。

当 ANN（人工神经网络）运行时，请记住 A 类和 B 类之间的界限变得更加清晰。这是因为该技术不断从训练样本中学习。随着学习的增强，分类变得更加准确。

通过更多地了解 TensorFlow 游乐场，它为理解神经网络如何工作提供了最简单的方式。即使它不是 100% 准确的表示，它也是一种快速的可视化。

因此，我们可以理解隐藏层、特征和输出。

我们仍然可以引入一些变化，例如学习率、训练数据和测试数据的比例以及隐藏层的数量。例如，我们可以将隐藏层的数量设置为 3，并将学习率调整为 1。你会看到类似这样的结果：

![](img/e34dde0654d255bebea353c553e965ac_65_0.png)

如果你按下播放按钮并让它运行一段时间，图像将保持如下所示：

![](img/e34dde0654d255bebea353c553e965ac_65_1.png)

密切观察输出。你应该会看到分类变得更差。然而，在黄色区域下的大多数黄色点周围，似乎有很多错误。这是由于参数更改导致的。

例如，学习率对准确度和达到正确的收敛性有很大影响。如果你使学习率变得很低，收敛可能需要很长时间。然而，如果学习率非常高，我们可能无法达到收敛，因为我们已经超过了它并错过了它。

有不同的方法可以在适当的时间达到收敛。学习率仅仅只是正确的方向，许多隐藏层，也许应用更少或更多的特征。然而，过度优化一切可能没有经济意义。在开始时设定一个明确的目标并坚持下去是正确的。

如果出现巨大的机会，你可能希望增强参数以提高模型的性能。

但是，如果你想要了解 Python 中 ANN 的外观，可以查看以下代码：

```python
X = np.array([[0,0,1],[0,1,1],[1,0,1],[1,1,1]])
y = np.array([[0,1,1,0]]).T
syn0 = 2*np.random.random((3,4)) - 1
syn1 = 2*np.random.random((4,1)) - 1
for j in xrange(60000):
    l1 = 1/(1+np.exp(-(np.dot(X,syn0))))
    l2 = 1/(1+np.exp(-(np.dot(l1,syn1))))
    l2_delta = (y - l2)*(l2*(1-l2))
    l1_delta = l2_delta.dot(syn1.T) * (l1 * (1-l1))
    syn1 += l1.T.dot(l2_delta)
    syn0 += X.T.dot(l1_delta)
```

这是一个简单的例子。当涉及到现实世界时，如果从头开始设计，ANN 会变得冗长且复杂。幸运的是，你与它们合作的方式正在变得更加“民主化”，这意味着技术背景有限的人也能利用它们。

## 第 9 章：如何使用 Scikit-Learn

现在你已完成安装，你可以开始使用这些库。我们将以 Scikit-Learn 库开始。

为了能够在代码中使用 scikit-learn，你应该首先通过运行以下语句来导入它：

**import sklearn**

### 加载数据集

机器学习完全在于分析数据集合。在此之前，我们首先应将数据集加载到我们的工作区中。该库自带许多我们可以加载并处理的数据集。我们将通过使用一个名为 *Iris* 的数据集来演示这一点。这是一个花卉数据集。以下代码展示了如何使用 scikit-learn 加载数据集：

```python
# Import scikit-learn library
from sklearn import datasets
# Load iris dataset
iris = datasets.load_iris()
# Confirm by printing the shape of the data
print(iris.data.shape)
```

### 简单线性回归

我们需要使用我们之前的示例，即根据学生为考试学习的时长来预测学生在考试中会获得的分数。由于我们只有两个变量，这是一个简单的线性回归任务。

### 导入库

运行以下 Python 语句以导入所有必要的库：

```python
import numpy as np
import pandas as pd

import matplotlib.pyplot as plt
```

该文件保存在一个名为 *student_marks.csv* 的 MS Excel 文件中。它位于存放我 Python 脚本的目录中，因此无需提供指向该文件的路径。文件名中的 .csv 扩展名表明它是一个逗号分隔值文件。

以下语句将帮助我们导入数据集到工作区。我们使用 Pandas 库（我们将其导入为 *pd*）来执行此操作：

```python
dataset = pd.read_csv('student_marks.csv')
```

我们现在可以探索数据集以了解更多信息，看看它有什么。直接转到 Python 终端并输入以下内容：

```python
dataset.shape
```

这意味着数据集有 25 行和 2 列。要查看数据的前五行，调用 *head()* 函数。

然而，当你尝试打印数据时可能会遇到错误。错误的原因可能是 Pandas 正在寻找要显示的信息量，因此你应该提供 sys 输出信息。可以通过修改代码为以下内容来解决该错误：

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import sys
sys.stdout = sys.stdout
dataset = pd.read_csv('student_marks.csv')
print(dataset.head())
```

我们只是向 sys 库提供了信息。要查看数据集的统计详情，我们按如下方式调用 *describe()* 函数：

```python
dataset.describe()
```

我们现在可以将数据点绘制在 2-D 图上，看看它们的分布情况。你可能现在已经意识到为什么我们要导入 *Matplotlib* 库。以下代码将帮助你绘制数据点：

```python
dataset.plot(x='Hours', y='Marks', style='o')
plt.title('Hours vs Marks(%)')
plt.xlabel('Hours')
plt.ylabel('Marks (%)')
plt.show()
```

代码返回如下绘图：

![](img/e34dde0654d255bebea353c553e965ac_69_0.png)

我们调用了 Pandas 库提供的 *plot()* 函数。我们将列名传递给该函数，它能够创建并显示绘图。*show()* 函数帮助我们显示绘图。

### 数据准备

数据准备应涉及将其划分为标签和 *attributes*（属性）。属性应创建自变量，而标签创建因变量。

我们的数据集只有两列。我们基于 Hours（时间）预测 Marks（分数）。这意味着 Hours 将形成属性，而 Marks 将形成标签。可以通过运行以下代码提取属性和标签：

```python
X = dataset.iloc[:, :-1].values
y = dataset.iloc[:, 1].values
```

X 变量将存储属性。注意，我们使用了 -1，因为我们需要将所有列分配给属性，除了最后一列，即 Marks。y 变量将存储标签。这里，我们使用了 1，因为 Marks 列的索引为 1。请记住，列索引从 0 开始。此时，我们拥有了数据集的属性和标签。我们需要将数据划分为两个集合，即 *training*（训练）和 *test*（测试）集合。Scikit-Learn 库提供了一种名为 “train_test_split()” 的方法，可用于此目的。

### 训练算法

我们将使用 *LinearRegression* 类来训练算法，该类必须从 Scikit-Learn 中导入。导入可以按如下方式进行：

```python
from sklearn.linear_model import LinearRegression
```

现在我们已导入该类，我们需要实例化它并给实例命名为 *linear_regressor*。演示如下：

```python
linear_regressor = LinearRegression()
```

让我们现在调用 *fit()* 方法并将训练数据传递给它：

```python
linear_regressor.fit(X_train, y_train)
```

正如我们之前所述，线性回归通过找到斜率和截距的最佳值来工作。我们在上面做的就是这件事。这两个值已经被计算出来，所以我们只需要查看它们的值。

要查看截距，运行以下命令：

```python
print(linear_regressor.intercept_)
```

### 预测

