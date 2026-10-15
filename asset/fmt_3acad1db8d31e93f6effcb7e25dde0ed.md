
| 结果 |
| :--- |
| Normal, John |
| Peck, Sally |
| Cross, Chris |

![](img/6e977c6eee8c1535039c864d41da5ccf_124_0.png)

## 在数组中查找值

- 输入 `index = Array.BinarySearch(myArray, "Megan")`，将 `Index` 替换为整数变量名，将 `myArray` 替换为数组名，将 `"Megan"` 替换为键字符串。
- `Array` 对象修改并搜索你的数据。
- 示例打印所找到项的索引。
- 按 `F5` 运行你的项目。

![](img/6e977c6eee8c1535039c864d41da5ccf_124_1.png)

# VISUAL BASIC .NET

## 使用文件流

大多数应用程序提供保存和加载用户文件的功能。其他应用程序使用文件存储配置数据。你可以使用 `FileStream` 类读取或修改现有文件并创建新文件。`FileStream` 类没有提供支持读写文件内容的必要函数。你必须使用读取器和写入器类访问流。要读取文件，请查看“从文件流读取”部分；要写入文件流，请查看“写入文件流”部分。

访问级别、文件共享模式：`FileStream(path, mode, access, share)`。`FileMode` 常量决定流如何打开或创建文件。`FileAccess` 常量决定对文件的读取或写入权限。`FileShare` 常量决定其他进程是否可以读取或写入该文件。当你处理它时，使用构造函数，`FileStream` 或 VB.NET 会在系统中创建文件。完成文件操作后，使用 `Close` 方法关闭流。

要设置文件，你必须在声明行中使用 `New` 关键字创建 `FileStream` 类的的新实例。使用构造函数进行设置。有关如何实例化类和使用构造函数的更多信息，请参第 7 章。

要指定 `FileShare` 常量，请使用枚举中的常量：`None`、`Read`、`ReadWrite` 和 `Write`。如果你同时指定了所需的访问权限，`Read` 允许其他程序在你在使用时从文件中读取，而 `ReadWrite` 允许其他程序写入文件。

你可用的构造函数之一需要文件名和模式，

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
