
# 第11 章 为你的应用程序添加帮助支持

```cpp
// 列表 11-5 包含一个 application_message
// 类。它定义了生成 QMessageBox
// 对象的方法。
#include <application.h>
#include <map>
#include <qmessagebox.h>
#include <string>

class application_messages
{
public:
    application_messages(void);
    ~application_messages(void);
    void displayMessage(int X);
protected:
    map<int, QMessageBox*, less<int>> HelpCategories;
    map<int, string, less<int>> HelpText;
    QMessageBox *Information;
    QMessageBox *Warning;
    QMessageBox *Critical;
    QMessageBox *Critical2;
};
application_messages::application_messages(void)
{
    Information = new QMessageBox("About Your Email Message",
        0, QMessageBox::Ok,
        0,0,0,0,FALSE,0);
        // 非模态消息框
    Warning = new QMessageBox("Caution", 0, QMessageBox::Warning,
        QMessageBox::Ok,
        QMessageBox::Cancel,0);
    Critical1 = new QMessageBox("Warning", 0,
        QMessageBox::Critical,
        QMessageBox::Ok,0,0);
    Critical2 = new QMessageBox("Warning", 0,
QMessageBox::Critical,
QMessageBox::Retry,
QMessageBox::Cancel(0);
string EmailSentMessage;
EmailSentMessage.append("Your email message has been sent.");
string EmailReceivedMessage("You have received Email.");
EmailReceivedMessage.append("\nRead now?");

HelpCategories.insert(pair<int,QMessageBox*>(pair(100,Information)));
HelpCategories.insert(pair<int,QMessageBox*>(pair(200,Warning)));
HelpCategories.insert(pair<int,QMessageBox*>(pair(300,Critical1)));
HelpCategories.insert(pair<int,QMessageBox*>(pair(400,Critical2)));
HelpText.insert(pair<int,string>(pair(110,EmailSentMessage)));
HelpText.insert(pair<int,string>(pair(120,EmailReceivedMessage)));
HelpText.insert(pair<int,string>(pair(210,DeleteEmailMessage)));
HelpText.insert(pair<int,string>(pair(310,BadAddressMessage)));
HelpText.insert(pair<int,string>(pair(420,EmailSentMessage)));
}
```

![](img/859df50987094e32dd2f5bb576f82bce_421_0.png)

图 11-15：列表 11-6 的额外输出。

## 需要记住的重要点

在本章中，你学习了：

* 帮助的目的是指导或作为参考。指导性帮助可以是定位或引导材料。参考性帮助向用户显示可使用的允许值、参数、选项和开关。帮助可以有多种形式：在线文档、上下文相关帮助、关键词搜索、在线教程和演示、命令行帮助以及帮助消息。
* 如果已经存在纸质手册，那么在线文档是非常友好的。它们可以被扫描并作为静态文本在在线文档中使用。但它们会重复纸质手册中的相同错误，并且对用户几乎没有帮助。`HTML` 文档可以使用颜色和字体来格式化手册的内容。可以使用 `HTMLWidget` 和 `HTML` 类来显示 `HTML` 文档。
* 上下文帮助是本地化的。这种帮助对于用户当前正在交互的组件是局部的。本地帮助可以显示在状态或信息区域或气泡帮助中。`QToolTips` 类用于为组件显示气泡帮助，它包含组件的单行描述。当用户将光标悬停在组件的活动区域时，提示将显示在组件下方。使用 `QWhatsThis` 类显示回答“这是什么？”问题的信息。这个气泡可以包含多个句子。当用户点击工具栏中的“这是什么？”按钮然后点击组件时，它就会显示。

## 第11 章 为你的应用程序添加帮助支持

* 关键词搜索允许用户从列表中选择关键词，或在编辑框中输入关键词。在显示帮助信息时会执行搜索。如果给用户提供了关键词可能列出的章节或区域，可以缩小搜索范围。用户必须足够熟悉应用程序，以便知道所需的帮助存储在哪里。
* 在线教程用于指导用户完成某个过程；它们不作为参考材料。它们也被初学者用于熟悉应用程序，或被经验用户用于学习新技巧。教程给用户提供在应用程序副本上执行的操作。演示向用户展示如何执行某个过程或任务。它们通常用于展示应用程序的特殊功能。
* 命令行帮助是参考性帮助。它在用户请求时或当选项或开关被错误使用时显示。这种帮助在命令行显示。
* 应用程序根据用户执行的操作生成帮助消息，或者代表应用程序、系统或硬件自动显示消息。消息有几种类型：信息、错误、警告和操作。每种消息类型都有关联的图标用于识别。错误和确认消息是操作消息的一种。状态消息是信息消息的一种。通过创建一个编码方案来管理和组织你的消息，创建一个适用于任何应用程序的消息框架。你可以使用 `map` 在文件或数据库中存储消息和消息类型对象。`KMsgBox` 和 `QMessageBox` 类显示模态和非模态消息。
* 企鹅原则 #11：如果起初没有成功，就寻求一点帮助。

# 第12 章 应用程序安装注意事项

与测试和文档一样，应用程序的安装过程往往是事后考虑的。就像糟糕的测试和不的文档一样，糟糕的应用程序安装会导致你的软件被拒绝。如果安装过程过于复杂，你的应用程序可能会被。如果安装过程导致安装异常，用户可能会感到沮丧，你的软件可能无法被使用。如果安装过程以任何方式损坏了用户的系统，即使你生产了高质量且实用的应用程序，如果安装程序糟糕，你的用户可能永远不知道这一点。

安装程序和流程包含在 Linux 应用程序开发者的清单中。记住，该清单包含了开发 Linux 应用程序时需要执行的最少任务。开发高质量程序必须包含创建有效的安装程序和流程。在应用程序开发过程早期创建安装程序和流程是一个好主意。这样，应用程序安装就可以成为增量应用程序测试的一部分。

## 本章内容

* 确定应用程序是否可以安装
* 确定应用程序将安装在何处
* 确定安装应用程序的哪些组件
* 确定安装应用程序所需的权限
* 确定应用程序将如何安装

### 五个关键应用程序安装问题

在安装应用程序之前，你必须回答五个问题：

1. 应用程序可以在用户的环境中安装吗？
2. 应用程序将安装在哪些目录？
3. 应用程序的哪些组件将安装？
4. 安装应用程序需要哪些权限？
5. 应用程序将如何安装？

在尝试安装之前未能获取并妥善处理这些问题的答案是应用程序安装失败的主要原因。另一方面，回答这些问题并准备你的安装流程以有效处理它们，将确保人们能够使用你的高质量 Linux 应用程序。

> **注意** 企鹅原则 #12：第一印象是持久的。

### 确定应用程序是否可以安装

安装流程中的要工作应该是检查硬件兼容性和软件兼容性。用户的系统必须拥有运行应用程序的物理资源。例如，如果你的应用程序需要 128MB 的 `RAM`，用户经过安装过程后发现由于系统中没有足够的 `RAM`，你的应用程序无法运行。

在将应用程序复制到用户系统之前，你应该验证你的应用程序所需的每种硬件资源。如果你的应用程序需要某种类型的打印机，程序必须验证该打印机是否存在。如果你的应用程序需要 500MB 的磁盘空间，应验证系统空间充足。如果你的应用程序要求显示器支持千万色，则不要安装应用程序。表 12-1 列出了安装应用程序前必须检查的常见硬件要求。

### 表 12-1 常见硬件要求
