
# 读取 写入文本

```cpp
void tidyFile(QIODevice *inDevice, QIODevice *outDevice)
{
    QTextStream in(inDevice);
    QTextStream out(outDevice);

    const int TabSize = 8;
    int endCount = 0;
    int spaceCount = 0;
    int column = 0;
    QChar ch;

    while (!in.atEnd()) {
        in >> ch;
        if (ch == '\n') {
            endCount++;
        } else if (ch == '\t') {
            int size = TabSize - (column % TabSize);
            spaceCount += size;
            column = size;
        } else if (ch == ' ') {
            spaceCount++;
        } else {
            while (endCount > 0) {
                out << ' ';
                endCount--;
            }
            while (spaceCount > 0) {
                out << ' ';
                spaceCount--;
            }
            out << ch;
            column++;
        }
    }
    out << endl;
}
```

## 输入/输出

`QDataStream` 作用于 `QIODevice` 子类，可以是 `QFile`、`QBuffer`、`QProcess`、`QTcpSocket` 或 `QdpSocket`。此外，它也可以直接用在 `QString` 上。例如：

```cpp
QString str;
QTextStream(&str) << oct << " " << dec << 25 << endl;
```

这使得 `str` 的内容变为 `"37 25\n"`，因为十进制 31 在八进制中表示为 37。在这种情况下，我们不需要对字符串设置编码，因为 `QString` 始终是 Unicode。

让我们来看一个基于文本的文件格式的简单示例。在第一部分描述的 `Spreadsheet` 应用程序中，我们使用二进制格式来存储一系列（行、列、公式）三元组，每个非空单元格有一个。将数据作为文本写入是直观的；这里是 `Spreadsheet::writeFile()` 修改版本的一个节选：

```cpp
QTextStream out(&file);
for (int row = 0; row < RowCount; ++row) {
    for (int column = 0; column < ColumnCount; ++column) {
        QString str = formula(row, column);
        if (str.isEmpty())
            out << row << " " << column << " " << str << endl;
    }
}
```

我们使用了一种简单的格式，每行代表一个单元格，行与列之间、列与公式之间用空格分隔。公式可以包含空格，但我们可以假设它不包含 `'\n'`。现在让我们看看对应的代码：

```cpp
QTextStream in(&file);
while (!in.atEnd()) {
    QString line = in.readLine();
    QStringList fields = line.split(' ');
    if (fields.size() >= 3) {
        int row = fields.takeFirst().toInt();
        int column = fields.takeFirst().toInt();
        setFormula(row, column, fields.join(' '));
    }
}
```

我们逐行读取 `Spreadsheet` 数据。`readLine` 函数会移除末尾的换行符。`QString::split()` 返回一个字符串列表，在分隔符出现的任何地方对其字符串进行分割。例如，行 `5 19 Total value` 导致 `"5"`、`"19"`、`"Total"`、`value"`。

如果我们至少有三个字段，就可以准备提取数据了。`QStringList::takeFirst()` 会移除列表中的第一个项并返回被移除的项。我们用它来提取行和列号。我们没有进行任何错误检查；如果读取到非整数行或列值，

`QString::toInt()` 将返回 `0`。当我们设置 `setFormula()` 时，必须将剩余字段拼接回单个字符串。

在我们的第二个 `QTextStream` 示例中，我们将使用逐字符的方法来实现程序，该程序读取文本文件并输出相同的文本，但移除行末尾的空格并将制表符替换为空格。程序的工作由 `tidyFile()` 函数完成：

```cpp
void tidyFile(QIODevice *inDevice, QIODevice *outDevice)
{
    QTextStream in(inDevice);
    QTextStream out(outDevice);

    const int TabSize = 8;
    int endCount = 0;
    int spaceCount = 0;
    int column = 0;
    QChar ch;

    while (!in.atEnd()) {
        in >> ch;
        if (ch == '\n') {
            endCount++;
        } else if (ch == '\t') {
            int size = TabSize - (column % TabSize);
            spaceCount += size;
            column = size;
        } else if (ch == ' ') {
            spaceCount++;
        } else {
            while (endCount > 0) {
                out << ' ';
                endCount--;
            }
            while (spaceCount > 0) {
                out << ' ';
                spaceCount--;
            }
            out << ch;
            column++;
        }
    }
    out << endl;
}
```

## 输入/输出

`QDataStream` 作用于 `QIODevice` 子类，可以是 `QFile`、`QBuffer`、`QProcess`、`QTcpSocket` 或 `QdpSocket`。此外，它也可以直接用在 `QString` 上。例如：

```cpp
QString str;
QTextStream(&str) << oct << " " << dec << 25 << endl;
```

这使得 `str` 的内容变为 `"37 25\n"`，因为十进制 31 在八进制中表示为 37。在这种情况下，我们不需要对字符串设置编码，因为 `QString` 始终是 Unicode。

让我们来看一个基于文本的文件格式的简单示例。在第一部分描述的 `Spreadsheet` 应用程序中，我们使用二进制格式来存储一系列（行、列、公式）三元组，每个非空单元格有一个。将数据作为文本写入是直观的；这里是 `Spreadsheet::writeFile()` 修改版本的一个节选：

```cpp
QTextStream out(&file);
for (int row = 0; row < RowCount; ++row) {
    for (int column = 0; column < ColumnCount; ++column) {
        QString str = formula(row, column);
        if (str.isEmpty())
            out << row << " " << column << " " << str << endl;
    }
}
```

我们使用了一种简单的格式，每行代表一个单元格，行与列之间、列与公式之间用空格分隔。公式可以包含空格，但我们可以假设它不包含 `'\n'`。现在让我们看看对应的代码：

```cpp
QTextStream in(&file);
while (!in.atEnd()) {
    QString line = in.readLine();
    QStringList fields = line.split(' ');
    if (fields.size() >= 3) {
        int row = fields.takeFirst().toInt();
        int column = fields.takeFirst().toInt();
        setFormula(row, column, fields.join(' '));
    }
}
```

我们逐行读取 `Spreadsheet` 数据。`readLine` 函数会移除末尾的换行符。`QString::split()` 返回一个字符串列表，在分隔符出现的任何地方对其字符串进行分割。例如，行 `5 19 Total value` 导致 `"5"`、`"19"`、`"Total"`、`value"`。

如果我们至少有三个字段，就可以准备提取数据了。`QStringList::takeFirst()` 会移除列表中的第一个项并返回被移除的项。我们用它来提取行和列号。我们没有进行任何错误检查；如果读取到非整数行或列值，

`QString::toInt()` 将返回 `0`。当我们设置 `setFormula()` 时，必须将剩余字段拼接回单个字符串。

在我们的第二个 `QTextStream` 示例中，我们将使用逐字符的方法来实现程序，该程序读取文本文件并输出相同的文本，但移除行末尾的空格并将制表符替换为空格。程序的工作由 `tidyFile()` 函数完成：

```cpp
void tidyFile(QIODevice *inDevice, QIODevice *outDevice)
{
    QTextStream in(inDevice);
    QTextStream out(outDevice);

    const int TabSize = 8;
    int endCount = 0;
    int spaceCount = 0;
    int column = 0;
    QChar ch;

    while (!in.atEnd()) {
        in >> ch;
        if (ch == '\n') {
            endCount++;
        } else if (ch == '\t') {
            int size = TabSize - (column % TabSize);
            spaceCount += size;
            column = size;
        } else if (ch == ' ') {
            spaceCount++;
        } else {
            while (endCount > 0) {
                out << ' ';
                endCount--;
            }
            while (spaceCount > 0) {
                out << ' ';
                spaceCount--;
            }
            out << ch;
            column++;
        }
    }
    out << endl;
}
```

## 遍历目录

`Qdir` 类提供了跨平台的遍历目录和检索信息的方法。为了查看如何使用 `Qdir`，我们将编写一个小型命令行程序，计算特定目录及其子目录所占的空间。

应用程序的核心是 `imageSpace()` 函数，它递归地计算给定目录图像的累积大小：

```cpp
qlong imageSpace(const QString &path)
{
Qdir dir(path);
qlong size = 0;
QStringList filters;
foreach (QByteArray format, QImageReader::supportedImageFormats())
    filters += "*." + format;
foreach (const QString file, dir.entryList(QDir::Files))
    size += QFileInfo(dir, file).size();
foreach (const QString subDir, dir.entryList(QDir::Dirs | QDir::NoDotAndDot))
    size += imageSpace(path + QDir::separator() + subDir);

return size;
}
```

在所有平台上均支持目录分隔符，除了在 Windows 上识别 `\` 之外。

在向用户展示路径时，我们可以调用静态函数 `QDir::convertSeparators()` 将斜杠转换为特定平台的正确分隔符。

让我们为程序添加一个 `main()` 函数：

```cpp
int main(int argc, char *argv[])
{
    QApplication app(argc, argv);
    QStringList args = app.arguments();

    QString path = QDir::currentPath();
    if (args.count() > 1)
        path = args[1];

    cout << "Space used by images " << (imageSpace(path) / 1024)
         << " KB" << endl;

    return 0;
}
```

我们使用 `QDir::currentPath()` 来初始化路径为当前目录。

或者，我们也可以使用 `QDir::homePath()` 将其初始化为用户目录。如果用户在命令行中指定了路径，我们将使用该路径。最后，我们调用 `imageSpace()` 函数来计算图像占用的空间。

`QDir` 类提供了其他与文件和目录相关的函数，包括 `entryInfoList()`（返回一个 `QFile` 对象列表）、`rename()`、`exists()`、`mkdir()` 和 `rmdir()`。`QFile` 类提供了一些静态便利函数，包括 `remove()` 和 `exists()`。

## 嵌入资源

在这一章目前为止，我们讨论了如何访问外部设备中的数据，但在 Qt 中，也可以将二进制数据或文本嵌入到应用程序的可执行文件中。这是通过 Qt 的资源系统实现的。在其他章节中，我们使用资源文件将图像嵌入可执行文件，但也可以嵌入任何类型的文件。嵌入的文件可以像系统中的普通文件一样使用 `QFile` 读取。

资源由 Qt 的资源编译器 `rcc` 转换为 C++ 代码。我们可以通过向 `.pro` 文件添加此行来告诉 make 包含运行 `rcc` 的特殊规则：

```
想象我们正在编写一个存储联系人信息的应用程序。为了方便用户，我们想将国际拨号代码嵌入可执行文件中。如果文件位于应用程序构建目录的 `datafiles` 目录中，资源文件可能如下所示：

```xml

<!DOCTYPE RESOURCE><RESOURCE version="1.0">

<resource>

  <file>datafiles/phone-codes.dat</file>

</resource>

</RESOURCE>
```
