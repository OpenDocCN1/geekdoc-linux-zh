
```cpp
class UI::MainWindow {
public:
    QMenuBar * menuBar;
    QToolBar toolBar;
    QWidget *centralWidget;
    QStatusBar statusBar;
    void setupUi(MainWindow *MainWindow)
{
        if (MainWindow->objectName() == nullptr)
            MainWindow->setObjectName("MainWindow");
        MainWindow->resize(480, 300);
    }
}
};
```

```cpp
#include <Application>
#include "mainwindow.h"

int main(int argc, char *argv[]) {
    Application a(argc, argv);
    MainWindow w;
    w.show();
    return a.exec();
}
```

第一个由两个文件组成。`C++` 类包含一个默认的构造函数，该构造函数调用 `ui` 对象的 `setupUi` 方法。也就是说，它并不包含多少意义：

```cpp
#include "mainwindow.h"
#include "ui_mainwindow.h"

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent), ui(new Ui::MainWindow)
{
    ui->setupUi(this);
}
```

每当头文件更改时，文件就会自动生成。不建议以任何方式修改它们，否则将导致不可引导且不可预测的行为。此外（以及大多数版本控制系统），频繁的更改倾向于更新服务器。

头文件中表单的实际内容。在这里，它包含一个指向上述 `ui` 对象的指针。

此外，所有派自 `QObject` 派生类的类都需要这个最近完成的 `Q_OBJECT` 宏声明——将在系列的后续部分进行讨论。目前，只需说明必须避免编译器错误即可。

# 编码，目前

让我们看看源代码。入口点在一个名为 `main.cpp` 的文件中。那里的方法是一个标准结构。它开始实例化 `QApplication`，该类处理程序运行和操作系统所需的事件循环和集成。在下一步中，实例化 `MainWindow` 实例。

# 跨平台之旅

控制原生操作系统。使用 `QML` 语言来描述界面及其行为。

尽管关于 `QtGui` 的问题偶尔会提到，但 Qt 已经多次表示，强烈建议避免它。使用 `QtGui` 会带来不可预见的未来。因此，我们用 `Qt.pro` 创建的基础在教程的剩余部分将继续使用。

基于 Qt 的表单是在源代码中创建的。然而，Qt 提供了用户界面的管理。双击项目视图中的 `ui` 文件以访问可视化编辑器。

`.ui` 文件包含了一个字段设置列表，这些设置用于构建控件。Qt 由多个模块组成——`Qt-Target` 需要的模块以及模板语句定义了二进制文件的类型。`SOURCES` 和 `FORMS` 块列出了每个类型的列表。当添加新文件时，`Qt Creator` 会自动更新这些部分。

左侧工具栏包含各种小控件，可以在表单模式下进行调整。右下角的列表显示属性。控件树视图是用户界面的结构概览。

## 来自文件的 GUI

Qt 目前包含两个不同的 GUI 集合，可以协作使用。`QtGui`（Qt 5 重命名为此方式）使用了一组

# 特色

## PyConUK 2013

Alan O'Donohee（左侧）向美国银行的员工和 Python 开发者介绍了他在 Raspberry Jam 配方项目方面的工作，该项目完全是非营利性的。

![](img/4c82285250803e975d41cda3a51d081f_63_0.png)

![](img/4c82285250803e975d41cda3a51d081f_63_1.png)

我们一直在使用像树莓派（Raspberry Pi）这样的设备和 Minecraft Pi 等游戏，通过帮助孩子们学习 Python 来改变计算教育。

去年的活动中，我们设立了教师分会，规模虽小但非常成功。我们在 Python 旅程中遇到的一些老师，直接受到了去年发生的事情的启发。

Tollervey 指的是与 Mike Sanderson 和 Simon Gaby 进行的两次 Turtle 演讲，这两位老师都采取了不同的方法来改进 Python 如今再次用于教育的库，并且都取得了巨大的成功。

去年的活动后，他们与教师合作，并创建了一些更具吸引力的材料，以便在学校使用。

## 附带 PI 的配菜

更进一步，教育分会以 Raspberry Jam 达到了高潮，在那里，Python 程序员和老师齐力合作，通过游戏来教育和娱乐对游戏探索计算机科学感兴趣的特定年龄段儿童。对于老师们来说，这是一个极佳的方法，他们前一天刚刚向英国一些顶尖的程序员请教了，现在可以测试新的想法。去年我们有老师参加，那么……那么呢，我们需要什么？Python 在教育领域的下一步是什么？我们还不确定，但这也是寻找答案的绝佳方式。

我们这里有大约 35 个孩子和他们的父母，我们正和朋友 Alan O'Donohee 一起举办 Raspberry Jam。

O'Donohee（也被称为“大使”）一直是推动树莓派作为教育工具的关键人物。在与 Nicholas、Alan 以及活动的一些老师坐在一起之后，显而易见，有许多原因让教育者相信 Python 和树莓派可以提供一个独特的机会，展示开发者在培养下一代计算机科学家方面发挥的内在作用。

活动展示了各种游戏，包括 Minecraft Pi、四旋翼机（通过 Minecraft Pi 控制）以及树莓派项目，这些项目提供了关于他们可以实现内容的清晰简报，将 Raspberry Jam 与 Python UK 联系起来，并证明了其在教育中的重要性。

O'Donohee 说，许多开发者看到孩子们正在面对的高水平挑战感到鼓舞。值得注意的是，我们在 Jam 的参与者中存在性别平衡——这说明不仅仅是社区的问题。

虽然对于今天的年轻专业人士来说为晚了，但英国政府最近宣布了新的 ICT（信息通信技术）。

## 让教育回归正轨

教育是今年 PyCon UK 活动的重点。

## 特稿

![](img/4c82285250803e975d41cda3a51d081f_64_0.png)

Zeth Green 在 Raspberry Jam 的展示环节中展示了他的编程技能

![](img/4c82285250803e975d41cda3a51d081f_64_1.png)

## 恐惧因素

## 我的女儿正在学习如何用 Python 和 Minecraft 构建火箭

Nicholas Tollevery，PyCon UK 组织委员会成员。

我们询问了 Tollevery 对拟议变化的愿景，这些变化将挑战年仅五岁的儿童构建他们的第一个算法。我欢迎对计算机科学、编程和计算思维的强调。我上学时是什么样的呢——我有一台笨重的电脑，用 BASIC 学习编程；ICT 教育已经比那时落后很多，所以看到课程中这种迫切的改变太棒了。

在学校实际上放弃计算机教育 20 多年后，计算机教育正在回到学校课程。如果你处于三十出头，你可能可能是“微软代”的一员——这是一个我们都应该害怕的胆寒的想法。现在是时候看到底层计算机科学的复兴（这对 Python 来说是一个福音）了，因为目前没有足够的预算或培训来支持老师。当一名小学的 IT 老师参加了 PyCon UK 的教育分会时，她指出了各地面临的挑战和问题。

这也直接影响了 Tollevery，他有各种年龄的孩子参加了 Raspberry Jam。我的女儿正在学习如何用 Python 和 Minecraft 构建火箭。她并没有意识到，但她正在用其中一个玩具进行编程，这非常不起。我的一个儿子正在构建某东西，他正在与一位 Python 开发者合作。他们都有自己的目标，我们有一些计算领域最聪明的脑在帮助他们。

“老师必须了解算法、逻辑和某种形式的迭代，”他们告诉我们。我们在与学校的采访中注意到，小学教师缺乏培训——许多人没有计算机或 ICT 资质。

在简短的采访结束后，Tollevery 迅速传达了对明年 PyCon UK 活动日益宏大的计划。

“一些老师正在带回课程，但没有正式的培训，而且学校提供的时间极少。去年我们整个计算机部门的预算只有 1500 英镑。从那里，我不得不尝试寻找资金来继续这个项目。”

“我们希望获得更多老师。策略是程序员不是老师，所以我们没有与孩子们交流的专业知识。
