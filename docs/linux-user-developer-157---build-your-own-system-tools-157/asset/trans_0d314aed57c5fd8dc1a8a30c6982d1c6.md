

# D3.js 教程

04 绘制更高级的图形

file:///Users/mtsous/docs/article/working/D3js_LUD/code/advExample.html

![](img/e7f197876caa0b235fb5da2d16a578ea_41_0.png)

+ - **上方** 更改条形图的颜色和方向，以创建更复杂的图表

请记住，数据是从上到下绘制的，且默认颜色为黑色。此外请注意，为了在条形之间留出一点空间，你需要在 `.attr("height", 20)` 这行代码中使用一个比在 `return (index*25);` 这行代码中乘以索引的数值更小的数值作为高度。`.data(myData)` 命令用于从 myData 数组中读取所有数据。你会经常使用这个命令。

## 04 绘制更高级的图形

这一步将通过添加颜色并使用不同的方向来绘制，从而增强之前生成的条形图。然而，第一个更改将使得现有代码读取一个对象数组，而不是普通的数字。myData 表格的格式现在将如下所示：

```javascript
var myData = [{key:"key1", value: 5},
{key:"key2", value: 32}];
```

你需要对代码其余部分做的唯一更改是在宽度属性中使用 **element.value**，而不是仅仅使用 **element**。这是合理的，因为程序需要知道哪个对象部分持有期望的值。现在是时候给条形图添加一些颜色了。你可以轻松地使用 `.style("background", "#CFCFCF")` 命令更改图表的背景颜色。`.style("fill", "blue")` 命令还会将每个单独条形的颜色设置为蓝色。你也可以从输出中看到，代码还进行了其他附加更改，使得每个条形都是从左到右绘制的，而不是从上到下。此外，条形现在位于网页的底部而不是顶部，这对于条形图的格式来说感觉更自然。

![](img/e7f197876caa0b235fb5da2d16a578ea_41_1.png)

## 05 缩放数据

大多数时候，你并不知道将要绘制多少元素，尤其是当你从外部源读取数据时。如果输出比你的画布大，那么一些数据将根本不会显示。这一步将向你展示如何解决这种棘手的情况。`d3.scale.linear()` 函数创建一个线性比例尺，它是一个以域（值范围）为输入，并以不同的范围作为输出的函数。下一行代码定义了输入域的可能值：

```javascript
domain([0, d3.max(myData, function(element){
    return element.value; })])
```

如你所理解的，可能的值是从零到在数组中找到的对象的 value 部分的最大值。程序员将不得不使用下一行代码定义输出范围：

```javascript
.range([0, myWidth])
```

Y 轴的值缩放考虑了 myData 中找到的元素总数以及输出高度。请注意，条形再次是从上到下绘制的。尝试作为练习将它们从左到右绘制。

## 06 读取外部数据

上一步开发的 scalingData.html 文件将作为本步骤使用的 externalData.html 文件中编程代码的起点。

首先，你将学习如何为图表的列添加文本标签，这在从外部源读取数据时极其实用。技巧是通过选择所有属于类 **bar-label** 的 SVG 元素来完成的。`enter()` 命令进入接口，使你能附加文本元素。`attr()` 命令将文本放置在期望的位置，即在条形的末端中间位置。然而，你需要一些 CSS 代码才能正确地将文本精确地放置在条形的末端。简单的 CSS 代码可以在 main.css 文件中找到。

通常，数据不会来自互联网或你的硬盘。这部分将向你展示如何读取外部文本文件以使用并可视化其数据。正如你猜测的那样，你需要编写一些 JavaScript 代码来完成任务。程序假设你的外部数据保存在一个名为 dataFile.txt 的文本文件中。

D3 提供五个函数来加载外部数据：`d3.text()`、`d3.xml()`、`d3.json()`、`d3.csv()` 和 `d3.html()`。`d3.text()` 函数将用于读取 dataFile.txt。

数据将像之前一样保存在同名的数组中，程序将继续执行，没有其他更改。

重要提示：出于安全原因，加载文本文件需要一个正在运行的 Web 服务器。如果你使用的是 Google Chrome，你可以通过使用 --allow-file-access-from-files 命令行参数执行 Chrome 来绕过对 Web 服务器的需求。

## 07 读取外部数据

dataFile.txt 文件的格式如下：

```
key1,150
...
```

JavaScript 代码解析 dataFile.txt 的方式如下：

```javascript
d3.text("dataFile.txt", function(error, unparsedData){
 if (error) {
 document.write("Error reading file!");
 return;
 }
 var data = d3.csv.parseRows(unparsedData);
 for (key in data)
 {
 var newValue = parseInt(data[key][1]);
 var object = {key: data[key][0], value: newValue};
 myData.push(object);
}
}
```

这里最重要的一点是要意识到 `d3.text()` 函数封装了完整的 JavaScript 代码 - 因此 `d3.text()` 函数调用的结束也是整个程序的结束。所使用的 error 参数是强制性的，每次都应包含在内。

![](img/e7f197876caa0b235fb5da2d16a578ea_42_0.png)

dataFile.txt 的内容最初在 `d3.text()` 函数的帮助下存储在 unparsedData 变量中。

然后使用 `d3.csv.parseRows()` 函数解析 unparsedData；这简化了整个解析过程。需要做一些额外的工作才能将数据放入 myData 变量中。默认情况下，所有值都作为字符串读取。由于每条记录的第二个值是整数，你需要使用 `parseInt()` 函数将字符串值转换为整数，该值临时保存在 new value 变量中。接下来，你构造一个具有正确字段的对象，并将该对象推入 myData 数组。

## 08 创建单独的图表函数

这一步将教你如何创建一个单独的函数来绘制图表。这是一个巨大的节省时间的方法，因为如果你想绘制多个图表，你不需要多次拥有相同的代码。为了简单起见，myData 数组中找到的数据是硬编码的。

由于 `plot()` 函数是使用 `plot.call()` 调用的，你可以使用著名的 `this` 关键字替换 `plot()` 函数内部所有对 `svg` 的引用。同样，`plot()` 实现内部所有对 myData 变量的引用都被 `parameters.data` 参数所替代。因此 `plot()` 与 svg 或 myData 变量都没有直接连接。阅读 chartFunction.html 以获取更多细节。

你现在可以使用任何你想要的数据集来调用 `plot()`！

## 09 使图表具有交互性

这一步将向你展示如何通过让条形在鼠标悬停在内部时每次改变颜色来创建交互式条形图！

一般想法是向每个条形添加一个或多个事件来执行你想要做的操作。首先，你在 `this.selectAll("bar")` 命令之后添加 mouseover 事件的代码，以影响所有条形。当鼠标离开条形时，颜色应该恢复到其先前值，这是借助 mouseout 事件完成的。

本文的第 2 部分将展示更多使用 D3.js 生成的令人印象深刻的图表，敬请期待！

## 布局

布局是 D3.js 中一种帮助你将数据格式化以便使用流行图表方法展示的函数变体。使用布局，你不仅可以显示图表、环形图、线条等，你还可以下载实现新布局的 D3.js 插件。本文的第 2 部分将更多地讨论布局以及它们可以生成的令人印象深刻的点。

> “最重要的一点是要意识到 `d3.text()` 函数封装了完整的 JavaScript 代码”

