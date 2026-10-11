
```cpp
1 /* * askwilbur.cpp */
2 #include <kapp.h>
3 #include <qstring.h>
4 #include <dcclient.h>

int main(int argc, char *argv)
{

KApplication app(argc,argv,"askwilbur");
DCOClient *client = app.dcpClient();
QString dccopID = client->registerAs(app.name());

QByteArray params;
QByteArray reply;
QString replyType;
QDataStream stream(params,IO_WriteOnly);
stream << (double)888.0;
if(client<double>("call","wilbur","receiver",params,
replyType,reply)) {
qDebug("Well, that didn't work!");
} else {
QDataStream inStream(reply,IO_ReadOnly);
if(replyType == "double") {
double root;
inStream >> root;
QString str;
str.sprintf("The return value is %g",root);
qDebug(str);
}
}

client->detach();
return(0);
```

此示例与上一个相同，但它会等待并显示结果。

第 18 行的 `call()` 调用发送消息并等待结果。与之前示例中的 `send()` 调用相同，除了第 20 行的返回值参数外。`replyType` 参数返回返回值的类型，`reply` 参数返回实际值。

### 362 第二部分 + 逐步阶

如果 `call()` 调用成功，第 23 行创建 `QDataStream` 以从返回的 `ByteArray` 中读取值。返回值的类型在第 24 行进行验证，并提取到局部变量 `root` 中。它被用于构建字符串 `str`，然后显示。输出如下：

返回值为 9.61179

图 15 显示了在收到来自 wilbur 和 askwilbur 的两条消息后显示的窗口。

图 15-1：接收两条消息后的 Wilbur

![](img/c47d54674a4d92abc6eebed0dd05f5fb_381_0.png)

#### 命令行参数

`KCmdLineArgs` 类不仅处理验证和解析命令行参数的大部分工作，还确保 KDE 应用程序的命令行参数是一致的。以下简单程序演示了使用 `KCmdLineArgs` 的最佳实践。

##### 命令行

```cpp
1 /* commandline.cpp */
2 #include <kcmdlineargs.h>
3 #include <iostream.h>

static KCmdLineOptions options[] = (
   "x","A binary option.",
   "name","An option with data",
   "longbin","A binary option",
   "longdata <name>","An option with data",
   "t","0",
11

  "twoforms","Two forms of a binary option",
13

  (0,0,0)
14);

int main(int argc, char **argv)
(
  QString option:
  KCmdLineArgs::init(argc,argv,
    "commandline.",
```

### 第15章 进程通信与小部件 363

```cpp
20 "Example of command line parsing"
21 "Version 0.0";
22 KCmdLineArgs::addCmdLineOptions(options);
23 KCmdLineArgs *pargs = KCmdLineArgs::parsedArgs();

if(pargs->IsSet("
```

可用的命令行参数定义为第 5 行的 `KCmdLineOptions` 数组。每个选项定义由三个字符串组成：第一个字符串是命令行上的字母（或字母），第二个是选项的简要描述，第三个是可选的初始值。选项数组由第 12 行包含三个字符串结束。静态方法 `init()` 初始化 `KCmdLineArgs` 类的静态数据。前两个参数是来自 C++ 命令行的标准 `argc` 和 `argv` 变量。后面是程序的名称、简要描述以及程序的当前版本号。

第 22 行的 `addCmdLineOptions()` 调用验证 `KCmdLineArgs` 类内部的 `KCmdLineOptions` 表信息。此选项列表结合 `KCmdLineArgs` 类内部预定义的选项，是确定所有可能的选项设置所需的所有信息。

第 23 行的静态方法 `parseArgs()` 根据定义的选项验证命令行。如果没有错误，该方法返回一个指向 `KCmdLineArgs` 对象的指针，其参数值已准备好供程序检索。如果在命令行上发现无效参数，程序将显示错误消息并停止。

第 6 行定义的 `-x` 选项是一个二进制标志位。也就是说，它除了是否出现在命令行上之外，不携带任何信息。第 25 行的 `IsSet` 调用如果值出现在行上将返回 `TRUE`，如果未出现则返回 `FALSE`。

### 第15章 ✦ 进程间通信与小程序 365

通用选项：

`--help`

`--help-qt`

`--help-kde`

`--help-all`

`--author`

`-V.` `--version`

显示选项帮助信息

显示 Qt 特有选项

显示 KDE 特有选项

显示所有选项

显示作者信息

显示版本信息

选项结束

选项：

`-o <name>`

`--longbin`

`--longdata <name>`

`--twoforms`

- 一个二进制选项
- 一个带有数据的选项 [/dev/null`]
- 一个二进制选项
- 一个带有数据的选项 [/dev/null`]
- 二进制选项的两种形式

#### 独特的应用程序

某些应用程序需要防止在任何时候都有多个自身的副本在执行。这是通过让应用程序尝试向 DCOP 服务器注册来实现，如果发现自己已经注册，则假设另一个副本已经在运行。以下示例使用了 `KUniqueApplication` 代替 `KApplication`，以保证程序永远不会有多个实例：

```cpp
1 /* unique.cpp */

2

#include <uniqueapp.h>
#include <kabdata.h>
#include <cmdlineargs.h>
#include <qlabel.h>
#include <iostream.h>

static CMdLineOptions options[] = {
"x", "Binary option",
{0,0}
};

int main(int argc, char *argv)
{
KAboutData about("unique");
"Example of unique application",
"0.1",
CMdLineArgs::init(argc, argv, &about);
CMdLineArgs::addCMdLineOptions(options);
KUniqueApplication::addCMdLineOptions(options);

if(!KUniqueApplication::start())
cout << "Unique is already running" << endl;
exit(0);

KUniqueApplication kuapp;
QLabel *label = new QLabel("Unique",0);
label->setAlignment(Qt::AlignCenter);
label->show();
kuapp.setWidget(label);
return(kuapp.exec());
}
```
