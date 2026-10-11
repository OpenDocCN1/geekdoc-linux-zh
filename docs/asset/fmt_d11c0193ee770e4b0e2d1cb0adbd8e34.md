
`permissions := S_IRUSR or S_IXUSR or S_IRGRP or S_IXGRP;`

`end;`

```
注意，表中的最后三个常量是由其他常量构建的。它们不是严格必须的，但有时非常方便。例如，如果你想给所有者所有权限，可以这样做：
```

```
permissions := S_IRUSR or S_IWUSR or S_IXUSR;
```

使用 `S_IRWXU` 要简单得多：

```
permissions := S_IRWXU;
```

## I/O 调用

Kylix 的开发是为了与 Delphi（一种 Windows 开发工具）兼容。为了确保跨平台兼容，Kylix 的文件/O 调用与 Delphi 的调用相匹配。Kylix 的开发者并不是傻瓜，他们当然知道上面介绍的 Linux 所有权和权限。在许多情况下，他们重载了或创建了多个版本的文件/O 方法以包含 Linux 特色。例如，`fstream` 的 `Create` 方法定义是重载的。你已经看了一个版本。另一个版本有一个参数允许你为新创建的文件设置权限。构造函数的第二个定义如下：

```
constructor(const filename: string; Mode: Word; Rights: Cardinal);
```

要设置 `Rights` 参数，可以使用之前介绍的技术。`Cardinal` 是一种整数类型。让我们看看这种能力如何使用。列表 12.2 显示了一个控制台应用程序，创建一个名为 `listall` 的 BASH 脚本文件。脚本文件创建时具有所有用户的读取和执行权限。你可以从终端执行脚本文件来返回 `ls -la` 命令的结果。它列出了当前目录下的所有文件（包括以点开头的文件）。它还显示了所有者和权限。

### 列表 12.2 使用 Tfstream 编写简单的 BASH 脚本

```
program MakeScript;
```

```
{$APPTYPE CONSOLE}

uses SysUtils,Classes,Libc;
```

```
var

aString: string;

afstream: Tfstream;

Rights: Cardinal;

begin

  // 首先，让我们设置权限。

  Rights := S_IRWXU or S_IRGRP or S_IXGRP or S_IROTH or S_IXOTH;

  // 使用我们定义的权限创建文件。

  afstream := Tfstream.Create('listall',fCreate or fmShareExclusive,Rights);

  // 现在设置执行工作的行。

  aString := '#!bin/bash'#10;

  // 写入脚本的第一行。

  afstream.WriteBuffer(PChar(aString)^,Length(aString));

  // 组合脚本的行。

  aString := 'ls -la'#10;

  // 写入脚本的第二行。

  afstream.WriteBuffer(PChar(aString)^,Length(aString));

  // 完成！关闭文件。

  afstream.Free;

end.
```
