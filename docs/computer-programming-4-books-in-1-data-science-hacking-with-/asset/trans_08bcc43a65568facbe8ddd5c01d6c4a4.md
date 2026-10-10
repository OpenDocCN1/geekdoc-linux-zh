

如果您想在 Windows 操作系统上安装上述 Python 库，这是一个简单的过程，我们将详细介绍。您只需下载一个安装程序，向导会引导您完成安装步骤。我们将提供安装 Numpy 的步骤。安装其余库的步骤是相同的。使用说明如下：

1. 从 SourceForge 网站或其他合法网站获取 Windows 安装程序。当前版本可能会变化，因此请选择最适合您配置的一个。
2. 从可用列表中选择正确的版本。
3. 接下来，双击打开 EXE 安装程序。
4. 接下来，您将看到 Numpy 及其特性的描述。现在，单击“下一步”按钮。

### Numpy 数组

当您完成 Numpy 的安装后，现在是时候探索 Numpy 数组了。在数值运算方面，Numpy 数组比 Python 列表更高效。Numpy 数组是经过广泛优化的专门对象。与等价的 Python 代码相比，Numpy 代码需要更少的显式循环。

如果我们回顾一下您在高中学过的一些数学主题，我相信您能记得标量和向量。例如，数字 2 是一个标量。当您向 2 加上 3 时，您进行的是标量加法。我们可以由一组标量组成一个向量。在 Python 编程中，您将有一个一维数组。这个概念还可以扩展到更高的维度。在两个数组上执行操作，如加法，可以归结为一组标量计算。

总之，Numpy 比纯 Python 代码更快。有一点很清楚，无论您是否使用 NumPy，都可以获得相同的结果。但是，显示的结果在呈现方式上有所不同。请记住，Numpy 的 sum() 函数的结果没有很多逗号。这是因为您处理的不是 Python 列表，而是 NumPy 数组。

### 使用 IPython 作为 Shell

数据分析师、工程师和科学家喜欢实验。IPython 是由科学家构建的，其目标是实验。IPython 提供的交互式环境被许多人视为 MATLAB 的直接替代方案。

以下是 IPython shell 的特性列表：

- 历史记录机制
- pylab 开关
- Tab 补全，帮助您识别命令
- 访问 Python 调试器和性能分析器

## 使用 Python 库进行网络抓取

在本节中，您将抓取“Rate My Professor”网站。简要描述一下 Rate My Professor 网站，它是一个包含学校、教授和大学评分的网站。在这个网站上，您可以搜索任何教授或学校，并在注册他们的课程之前查看他们的评分。这是一个很好的功能，帮助您更多地了解您希望加入的教授或大学。在本节中，您将学习如何抓取和提取重要的教授标签。虽然这不是非法过程，但从该网站大规模抓取数据可能会导致您的 IP 地址被列入黑名单。因此，您应该只尝试一次或两次，但不要盲目地做。

## 网络抓取

也称为抓取、数据收集或数据提取，是一种从网站挖掘数据的机制。在某些情况下，当您直接从网页上获取所需的数据时，网络抓取可能至关重要，但有时，这是一种糟糕的处理方式，因为它就像在未获得许可的情况下从网站窃取昂贵数据一样。然而，您应该将抓取过程减少到只有一次或两次，以免惹上麻烦。

最重要的网络抓取库包括：

1. Beautiful Soup
2. Requests

以下是我们将遵循的步骤。

1. 首先，我们导入相关的库
2. 找到 URL 并将其存储在变量中
3. 使用 requests 库向网站发送请求
4. 应用 Beautiful Soup 库从网站查找 HTML 数据。
5. 使用 soup 识别所有方法来获取我们搜索的必要标签。
6. 移除所有 HTML 标签并将其转换为纯文本格式。

您可能想知道要提取哪种类型的标签，好吧，在 Rate My Professor 网站上，每位教授都有他们受尊敬的标签。我们将尝试提取这些标签。

在开始之前，确保您以较低的速度抓取数据，您可以使用 VPN 服务更改您的 IP 地址。这可以防止您的 IP 地址被阻止。希望您能遵循说明。

有一件事您应该注意，没有必要解释每一行代码，因为 Python 代码是自解释的。但是您不会感到困惑，因为所有内容都会以简单的格式阐明。因此，本指南的编写方式使得无论您的编程水平如何，每个人都能理解。

您可能会找到许多在线教程，但本指南易于理解，因为代码都有解释。然而，某些部分是机械化的过程，您需要遵循它们。

让我们深入其中！

### 1. 首先，导入必要的库

让我们导入几个库，如 Beautiful Soup 和 Requests。

```python
import requests
from bs4 import BeautifulSoup
```

### 2. 找到 URL 并将其存储在变量中

让我们将教授的 URL 存储在名为“url”的变量中。网站 URL 是 Rate_My_Professor。

### 3. 使用 requests 库向网站发送请求

在以下案例中，我们通过传递“url”作为参数来应用 requests 库。请注意不要多次运行此操作。如果您收到类似 Response 200 的响应，那么它是成功的。如果您发现其他情况，那么可能是代码或您的浏览器出现了问题。

### 4. 应用 Beautiful Soup 库从网站获取原始 HTML 数据。

在这里，我们应用 BeautifulSoup，通过传递 page.text 作为参数并应用 HTML 解析器。您可以尝试输出 soup，但显示 soup 不会为您提供响应。相反，它包含了大量的 HTML 数据。

这是一个代码片段。

```python
soup = BeautifulSoup(page.text, "html.parser")
```

### 5. 应用 soup.findAll 方法查找您正在搜索的特定标签。

在这里，您将添加您正在搜索的标签。要找到标签名称，您需要做的是在网页上的相关标签上右键单击，或点击标签内的 Ctrl-Shift-I。接下来，一个包含所需标签的网页将在您的右侧打开。

接下来，您可以复制 HTML 标签和类（如果可用），然后将其放置在 soup.findAll 方法中。在以下案例中，HTML 标签是“span”，类是“tag-box-choosetags”。

```python
proftags = soup.findAll("span", {"class": "tag-box-choosetags" })
proftags
```

### 6. 消除所有 HTML 标签并将其更改为纯文本格式

在以下步骤中，您需要移除所有 HTML 标签并将其更改为文本格式。这可以通过使用 for 循环中的 get_text 方法来完成。这将 HTML 更改为文本格式。

```python
for mytag in proftags:
    print(mytag.get_text())
```

**Hilarious (11)**

1. **Caring (9)**
2. **Accessible outside class (8)**
3. **Amazing lectures (5)**
4. **Clear grading criteria (4)**
5. **Inspirational (4)**
6. **Group projects (3)**
7. **Respected (3)**
8. **Gives good feedback (2)**
9. **EXTRA CREDIT (2)**
10. **Participation matters (1)**
11. **Lecture heavy (1)**
12. **Test heavy (1)**
13. **So many papers (1)**

因此，您得到了上述您正在寻找的信息。您获得了教授的所有标签。这就是如何使用 Requests 和 Beautiful Soup 库从互联网抓取数据。

总之，Python 有三个核心数据科学库，许多其他库都是基于它们构建的：

