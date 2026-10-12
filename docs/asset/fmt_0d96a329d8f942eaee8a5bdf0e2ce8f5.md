
# 260 第7章 • 控制中断 (Control Breaks)

![](img/cad5396e3e49a03edb322ef333cfad40_267_0.png)

此类程序的 `closeDown()` 例程比初看起来看起来要复杂得多。似乎你应该打印 `grandTotal`，关闭文件并返回主逻辑。然而，当你读取记录时，主逻辑的 `eof` 决策会将逻辑流引导到 `closeDown()` 例程。你还没有打印 `categoryTotal`，也没有将类别的计数加到 `grandTotal` 中。在打印 `grandTotal` 之前，你必须处理这两项任务。你可以在 `closeDown()` 中将这两个任务作为独立的步骤执行，但最简单的方法是最后再记住控制中断例程 `categoryChange`。`categoryChange()` 模块在每个之前的类别完成后执行——也就是说，在程序执行期间每遇到一个新类别时都会执行。你也可以在最后一个类别完成后、在文件末尾创建此模块。找到文件末尾实际上是另一种形式的中断；它标志着最后一个类别已完成。`categoryChange()` 模块打印类别并将汇总汇总到 `grandTotal`。

当你从 `closeDown()` 调用 `categoryChange()` 模块时，它会执行你需要的任务，例如设置 `previousCategory` 的值。你必须权衡调用已写的 `categoryChange()` 模块（执行几条不必要的语句）的便利性，与花时间编写一个仅执行绝对必要语句的新模块之间的关系。

非常重要的一点是，这个控制中断程序无论是有三类书籍还是300类书籍都有效。注意，书籍的类别类型并不重要。例如，程序询问 `bookCategory = "fiction"`。相反，程序的控制在类别字段发生变化时会中断，这与该变化的具体内容没有任何依赖关系。

## 执行多层级控制中断

假设你上一个例子中的书店非常成功，你在全国范围内建立了一系列连锁店。每当有一笔交易，就创建一个包含 `bookTitle`、`bookPrice`、`bookCity` 和 `bookState` 字段的记录。你希望有一份报告，提供每个类别和每个州销售书籍摘要，类似于 7-16 所示。这样的报告不包含任何单独记录的信息，而是包含分组总计，这是一种汇总报告。

此程序包含一个多层级控制中断——也就是说，正常的控制流（读取记录并包含销售额）会响应于多个条件的变化而偏离以打印总计。在这份报告中，控制中断响应于条件之一（或两者）而发生：当 `bookCategory` 变量的内容变化以及 `bookState` 变量发生变化时。

正如用于创建单层级控制中断报告的文件必须准备好一样，用于创建多层级控制中断报告的输入文件也必须准备好。用于销售报告的输入文件必须在 `bookState` 内部按 `bookCity` 排序，正如一个州的所有记录一样，例如，来自 IA 的记录在前；然后是来自另一个州（如 IL）的所有记录在后。在任何一个州内，所有一个城市的记录在前，然后是下一个城市的记录在后。例如，产生图 7-16 所示报告的输入文件包含 200 条 IA 州 Ames 的书籍销售记录，随后是 814 条 IA 州 Des Moines 的销售记录。基本处理涉及读取一条书籍销售记录、计数器加 1，然后读取下一条书籍销售记录。在任何城市记录的末尾，你打印该市的总计；在任何州记录的末尾，你打印该州的总计。

### 图 1-1b：按城市和州划分的书籍销售报告示例运行

| 按城市和州划分书籍销售 |
| :--- |
| Ames | 200 |
| Des Moines | 814 |
| Iowa City | 291 |
| IA 总计 | 1305 |
| Chicago | 1093 |
| Crystal Lake | 564 |
| McHenry | 213 |
| Springfield | 365 |
| IL 总计 | 2235 |
| Springfield | 289 |
| Worcester | 100 |
| MA 总计 | 389 |
| 总计 | 3929 |

按城市和州划分书籍销售报告的 `housekeeping()` 模块与上一个控制中断程序中的 `housekeeping()` 模块相似，在该程序中，类别变化有一个单一控制中断。在每个程序中，你都声明变量、打开文件并读取第一条记录。这一次，有多个字段需要保存并与旧字段比较。在这里，你声明了两个特殊变量 `prevCity` 和 `prevState`，如图 7-17 所示。此外，书籍销售报告显示了三种总计，因此你声明了三个新变量作为书籍销售报告中总计的容器：`cityCounter`、`stateCounter` 和 `grandTotal`，它们都初始化为零。

此程序同时打印 `bookState` 和书籍总计，因此你需要两个控制中断例程：`cityBreak()` 和 `stateBreak()`。每当城市字段发生变化时，`cityBreak()` 例程执行这些标准的控制中断任务：

- 它对上一个组进行任何必要的处理——在本情况下，它打印上一个城市的总计。
- 它将当前层的总计汇总到更高级别——在本情况下，它将城市计数加到州计数中。
- 它将当前层的总计重置为零。
- 它对新组进行任何必要的处理——在本情况下，没有操作。
- 它更新控制字段——在本情况下，它设置 `bookCity`。

### 图 1-1b：按城市和州划分书籍销售报告的流程图和 `housekeeping()` 模块代码

```
housekeeping()
    char bookTitle
    char bookPrice
    char bookCity
    char bookState
    char prevCity
    char prevState
    int cityCounter
    int stateCounter
    int grandTotal
    BOOK SALES BY CITY AND STATE
    
 BY CITY AND STATE
    prevCity = ""
    prevState = ""
    cityCounter = 0
    stateCounter = 0
    grandTotal = 0
```

```
cityBreak()
    if bookCity != prevCity
        print bookCity, cityCounter
        stateCounter += cityCounter
        cityCounter = 0
    prevCity = bookCity
```

```
stateBreak()
    if bookState != prevState
        print bookState, stateCounter
        grandTotal += stateCounter
        stateCounter = 0
    prevState = bookState
```

## 271 第7章 • 控制中断

```
mainLoop()
    housekeeping()
    while not eof
        read
        if bookState != prevState
            stateBreak()
        if bookCity != prevCity
            cityBreak()
        cityCounter++
    cityBreak()
    stateBreak()
    print "Grand Total", grandTotal
    closeFiles()
```
