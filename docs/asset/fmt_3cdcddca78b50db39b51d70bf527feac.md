
- 创建新项目或打开现有项目。在方法中或需要打开文件的地方输入 `dim myfileStream`，将 `myfileStream` 替换为分配给流的变量名。
- 输入 `As New IO.IO.FileStream("C:\test.txt",`，将 `C:\test.txt` 替换为你想要打开的文件名）。
- 出现 IntelliSense 框，列出可用常量。
- 输入或点击一个常量并在后面跟一个逗号，

## 额外

你可以使用 `FileMode` 和 `FileAccess` 枚举来指定流如何打开文件。

## FILEMODE 枚举：

| 名称 | 说明 |
| :--- | :--- |
| Append | 如果文件存在则打开并跳转到文件末尾，或创建一个新文件。仅与 `FileAccess.Write` 配合使用。 |
| Create | 指定操作系统创建一个新文件。如果文件存在则覆盖该文件。 |
| CreateNew | 指定操作系统创建一个新文件。如果文件存在则会发生错误。 |
| Open | 指定操作系统打开一个现有文件。 |
| OpenOrCreate | 指定如果文件存在则打开新文件；否则创建一个新文件。 |

## FILEACCESS 枚举：

| 名称 | 说明 |
| :--- | :--- |
| Read | 打开文件进行读取。允许你从文件中读取数据。与 `Write` 结合用于读/写权限。 |
| ReadWrite | 打开文件进行读写。 |
| Write | 打开文件进行写入。 |

![](img/6e977c6eee8c1535039c864d41da5ccf_126_0.png) 你可以使用 `FileMode` 和 `FileAccess` 枚举来指定流如何打开文件。
- 你可用的构造函数之一需要文件名和模式，
- 访问级别、文件共享模式：`FileStream(path, mode, access, share)`。
- `FileMode` 常量决定流如何打开或创建文件。
- `FileAccess` 常量决定对文件的读取或写入权限。
- `FileShare` 常量决定其他进程是否可以读取或写入该文件。
- 当你处理它时，使用构造函数，`FileStream` 或 VB.NET 会在系统中创建文件。
- 完成文件操作后，使用 `Close` 方法关闭流。
- 要设置文件，你必须在声明行中使用 `New` 关键字创建 `FileStream` 类的的新实例。
- 使用构造函数进行设置。有关实例化类和使用构造函数的更多信息，请参第 7 章。
- 要指定 `FileShare` 常量，请使用枚举中的常量：`None`、`Read`、`ReadWrite` 和 `Write`。
- 如果你同时指定了所需的访问权限，`Read` 允许其他程序在你在使用时从文件中读取，而 `ReadWrite` 允许其他程序写入文件。

# VISUAL BASIC .NET

## 使用文件流

| 名称 | 说明 |
| :--- | :--- |
| Append | 如果文件存在则打开并跳转到文件末尾，或创建一个新文件。仅与 `FileAccess.Write` 配合使用。 |
| Create | 指定操作系统创建一个新文件。如果文件存在则覆盖该文件。 |
| CreateNew | 指定操作系统创建一个新文件。如果文件存在则会发生错误。 |
| Open | 指定操作系统打开一个现有文件。 |
| OpenOrCreate | 指定如果文件存在则打开新文件；否则创建一个新文件。 |

| 名称 | 说明 |
| :--- | :--- |
| Read | 打开文件进行读取。允许你从文件中读取数据。与 `Write` 结合用于读/写权限。 |
| ReadWrite | 打开文件进行读写。 |
| Write | 打开文件进行写入。 |

![](img/6e977c6eee8c1535039c864d41da5ccf_126_0.png)
- 你可以使用 `FileMode` 和 `FileAccess` 枚举来指定流如何打开文件。
- 你可用的构造函数之一需要文件名和模式，
- 访问级别、文件共享模式：`FileStream(path, mode, access, share)`。
- `FileMode` 常量决定流如何打开或创建文件。
- `FileAccess` 常量决定对文件的读取或写入权限。
- `FileShare` 常量决定其他进程是否可以读取或写入该文件。
- 当你处理它时，使用构造函数，`FileStream` 或 VB.NET 会在系统中创建文件。
- 完成文件操作后，使用 `Close` 方法关闭流。
- 要设置文件，你必须在声明行中使用 `New` 关键字创建 `FileStream` 类的的新实例。
- 使用构造函数进行设置。有关实例化类和使用构造函数的更多信息，请参第 7 章。
- 要指定 `FileShare` 常量，请使用枚举中的常量：`None`、`Read`、`ReadWrite` 和 `Write`。
- 如果你同时指定了所需的访问权限，`Read` 允许其他程序在你在使用时从文件中读取，而 `ReadWrite` 允许其他程序写入文件。

# VISUAL BASIC .NET

## 从流读取

大多数应用程序提供保存和加载用户文件的功能。其他应用程序使用文件存储配置数据。你可以使用 `FileStream` 类读取或修改现有文件并创建新文件。`FileStream` 类没有提供支持读写文件内容的必要函数。你必须使用读取器和写入器类访问流。要读取文件，请查看“从文件流读取”部分；要写入文件流，请查看“写入文件流”部分。

访问级别、文件共享模式：`FileStream(path, mode, access, share)`。`FileMode` 常量决定流如何打开或创建文件。`FileAccess` 常量决定对文件的读取或写入权限。`FileShare` 常量决定其他进程是否可以读取或写入该文件。当你处理它时，使用构造函数，`FileStream` 或 VB.NET 会在系统中创建文件。完成文件操作后，使用 `Close` 方法关闭流。

要设置文件，你必须在声明行中使用 `New` 关键字创建 `FileStream` 类的的新实例。使用构造函数进行设置。有关实例化类和使用构造函数的更多信息，请参第 7 章。

要指定 `FileShare` 常量，请使用枚举中的常量：`None`、`Read`、`ReadWrite` 和 `Write`。如果你同时指定了所需的访问权限，`Read` 允许其他程序在你在使用时从文件中读取，而 `ReadWrite` 允许其他程序写入文件。

你可用的构造函数之一需要文件名和模式，

## 使用文件流

![](img/6e977c6eee8c1535039c864d41da5ccf_125_0.png)

![](img/6e977c6eee8c1535039c864d41da5ccf_125_1.png)

```vb
class Module1
{
    static void Main()
    {
        FileStream fs = new FileStream("test.txt", FileMode.Create, FileAccess.Write);
        fs.Close();
    }
}
```
