

![](img/3b256f430f51c98f1315671f6e4eec19_154_0.png)

![](img/3b256f430f51c98f1315671f6e4eec19_154_1.png)

## 04 设置它

在代码中添加详细的注释很重要，因为它允许你记录下令人困惑的事情并记录复杂的流程。如果以后有另一位程序员需要使用你的代码，他们会非常感激。从添加一条包含程序将要做什么以及你姓名的注释开始。所有注释行都以井号（#）开头，并且不会被 Python 解释器解释为代码。我们导入 sys 库，以便以后可以使用 sys.exit 函数关闭程序。我们还从 decimal 库导入所有内容，因为我们想要使用 decimal 类型。

## 01 保持井然有序

我们不想让新 Pi 上出现杂乱的文件夹，所以让我们进入文件管理器并整理一下。点击屏幕左下角菜单图标旁边的图标打开文件管理器。通过右键单击并选择 New>Folder 创建一个新文件夹，然后输入名称并点击 OK。我们创建了一个名为 Python 的文件夹，并在其中创建了一个名为 Hello World v2 的文件夹。

![](img/3b256f430f51c98f1315671f6e4eec19_154_2.png)

![](img/3b256f430f51c98f1315671f6e4eec19_154_3.png)

## 03 保存你的工作

在编程时养成使用 Ctrl+S 不断保存工作的好习惯总是明智的，因为丢失你正在处理的内容会很可惜。要首次保存文件，请按 Ctrl+S 或转到 File 菜单并选择 Save。为文件取一个合理的名称并将其保存在之前创建的整洁文件夹结构中。编程时保持井然有序是一个好习惯，因为当你的项目变得更大、更复杂时，这会让事情变得容易得多。

## 02 启动 Geany

通过进入 LXDE 菜单并进入 Programs 来启动 Geany。从这里，选择 Geany。进入 Geany 界面后，通过选择 ‘New (with template)>main.py’ 从模板创建一个新的 Python 文件。删除此模板中的所有内容，只保留第一行： #!/usr/bin/env python。这行很重要，因为它意味着你可以从命令行运行代码，并且 Bash shell 会知道用 Python 解释器打开它。

```python
#!/usr/bin/env python

# An advanced Hello World program
# Programming in Python via
# for Linux User and Developer

# Import the sys library for
import sys
# Import everything from the
from decimal import *
```

## 05 变量

变量是存储在内存中并可通过名称访问的数据。我们的程序将首先询问你的名字，将其存储在变量中，然后打印出欢迎信息。我们将添加一条解释此操作的注释并创建一个名为 firstName 的变量。注意我们将第二个单词的首字母大写以使其更易读。我们希望 firstName 变量保存由一个名为 raw_input 的函数返回的值，该函数会提示用户输入。问题被传递到括号内的 print 函数中，并且由于这是一个字符串，所以用引号括起来。字符串类型基本上是字符的集合。请注意我们在冒号后添加的额外空格，因为用户会在此问题后直接输入。

```python
# Get the user's first name and output a message
# The string in quotation marks will be displayed
```

```python
print('Welcome ' + firstName + '\n')
```

## 06 打印一条信息

现在 firstName 中有了值，我们需要向屏幕输出欢迎信息。我们在 Python 中使用 print 函数向屏幕打印。print 函数后面跟着一对括号，其中包含要打印的值。使用加法运算符处理字符串时，它们会被连接起来。注意 firstName 不需要用引号括起来，因为它是变量名。如果它被括在引号中，文本 firstName 就会被输出。我们最后通过在输出中添加 ‘\n’ 字符（换行符）来在开始下一个示例前留出一个空白行。

> 当使用加法运算符
> 处理字符串时，它们会被连接起来

