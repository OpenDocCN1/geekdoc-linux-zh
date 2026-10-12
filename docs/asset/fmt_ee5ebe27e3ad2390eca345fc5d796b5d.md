
当文件处于打开输出状态时，使用以下格式向其写入：

```
print $NAME "Message\n";
```

## 深入解析

### Perl 脚本

#### 即时解决方案

##### 安装 Perl

由于 Perl 不是 Linux 的自动组成部分，你需要在安装它之后才能使用它进行编程。如何安装 Perl 取决于你使用的发行版。以下说明特定于 Red Hat：

1. 以 root 身份登录。
2. 确保 Red Hat CD-ROM 在 CD-ROM 驱动器中。
3. 输入 `mount /mnt/cdrom` 来挂载 CD-ROM。
4. 输入 `cd /mnt/cdrom/RedHat/RPMS` 以更改到软件包目录。
5. 输入 `rpm -ihv perl` 并按 Tab 键展开文件名，然后按 Enter 键安装软件包。
6. 输入 `cd /` 以退出挂载点。
7. 输入 `umount /mnt/cdrom` 以从文件系统卸载 CD-ROM。

**注意：** 如果你的发行版没有附带 Perl 或者你想要更新版本，请尝试 `www.perl.com`、`www.perl.org` 或 `www.cpan.org`。你可以在 `www.perl.com/CPAN/latest.tar.gz` 获取最新版本的官方源代码。

##### 获取并安装 Perl 库模块

要安装 Perl 库，请执行以下操作：

1. 以 root 身份登录。
2. 使用 Web 浏览器访问 `www.perl.com/CPAN-local/CPAN.html`。综合 Perl 归档网络 (CPAN) 是获取 Perl 源代码和模块的权威地点之一。
3. 向下滚动到标题为 `PERL MODULES` 的部分。
4. 这就是变得棘手的地方，因为列出了数百个模块。CPAN 使用两种组织工具来帮助你找到所需内容。首先，模块按字母顺序分组。然而，第二个工具才是方便的。模块按子目录排列，对应于它们所服务的工具或功能。表 21.4 列出了部分模块组所代表的含义（现有的模块组数量过多，无法在此全部列出）。

###### 表 21.4

Perl 可用的部分模块组。

| 组 | 模块用途 |
| :--- | :--- |
| `Apache` | 与 Apache Web 服务器接口 |
| `Audio` | 操作声音文件 |
| `Business` | 处理现金交易 |
| `CGI` | 使 Perl 能够作为 CGI 脚本运行 |
| `Chart` | 图形化和绘制数据 |
| `Convert` | 格式转换 |
| `Crypt` | 处理某些常见的加密形式 |
| `Data` | 处理数据结构 |
| `Date` | 处理日历日期 |
| `DBD` | 与数据库格式接口 |
| `DBIx` | 操作数据库内容 |
| `Devel` | 提供 Perl 开发工具 |
| `ExtUtils` | 扩展 Perl，使其能够与其他代码类型协同工作 |
| `File` | 操作文件 |
| `Games` | 使用 Perl 编写游戏 |
| `Gimp` | 为 Gimp 图形程序编写扩展 |
| `HTML` | 将 Perl 与 HTML 代码集成 |
| `Image` | 使 Perl 能够处理图像 |
| `Lingua` | 使 Perl 能够解析和操作各种语言的文档 |
| `Log` | 创建和操作日志文件 |
| `Mail` | 使 Perl 能够解析并与多种邮件和邮件列表格式接口 |
| `Math` | 添加扩展，帮助 Perl 以特定方式处理数字 |
| `Net` | 与各种网络工具接口 |
| `Statistics` | 执行统计分析 |
| `String` | 解析和操作 ASCII 字符串 |
| `Win32` | 与 Windows 95 及更高版本的实用程序交互 |
| `WWW` | 与 Web 服务接口 |
| `XML` | 处理 XML 代码 |

**637**

单击你想检查的组中的任意模块。此操作将打开一个包含该组中所有模块的目录。

5. 每个模块由两个不同的文件表示。第一个是 `.readme` 文件，它讨论模块的功能并提供你可能需要的任何说明，包括关于该模块所依赖的其他模块的信息。务必在尝试使用它之前阅读 `.readme` 文件并获取该模块所依赖的任何其他模块。否则，你稍后必须回来做这件事。第二个文件是模块本身。
6. 选择你想要使用的模块后，单击它们的名称以进行下载。你或许会发现下载 `_readme` 文件也很有用。
7. 每个模块都存储为 tarball（tar 归档包）。请将其解包并解压到你首选的下载目录中。
8. 通常，下一步是键入以下命令序列：

```perl
perl Makefile.PL
make
make install
```

9. 然后要在 Perl 程序中引入此模块，你需要使用以下格式的一行代码：

```perl
use modname;
```

| 相关解决方案： | 位于页码： |
| :--- | :--- |
| 打开或创建 Tarball | 110 |

### 运行 Perl 程序

如果你有一个想要运行的 Perl 程序，请执行以下操作：

1. 要么切换到包含该程序的目录，要么将其添加到你的路径中。
2. 根据你的存储方式，可以通过两种方法之一运行该程序：
    - 如果文件是可执行的，请键入 `./_filename_`。
    - 如果文件是不可执行的，请键入 `perl _filename_`。

### 使用 Perl 编写 CGI 脚本

要在 Perl 中编写 CGI 脚本，请执行以下操作：

1. 确定你的 CGI 脚本必须具有什么文件扩展名，Web 服务器才能识别它。例如，虽然 Perl 程序的文件名通常以 `.pl` 结尾，但许多 Web 服务器不会识别 Perl CGI 程序，除非它以 `.cgi` 结尾。
2. 确定你的 CGI 脚本必须存储在哪里，Web 服务器才能识别它。通常，CGI 脚本必须包含在中央或单独用户的 `cgi-bin` 目录中。这允许系统管理员轻松定位 Web 站点中使用的脚本，以便进行安全控制。
3. 使用你喜欢的文本编辑器在 Web 服务器 CGI 目录或单独的测试目录中创建脚本。
4. 确保你已安装模块 `CGI.pl`。
5. 在脚本开头添加以下行：

```perl
use CGI;
```

6. 编写脚本。
7. 保存并退出文件。
8. 使文件可执行，根据需要放宽或收紧权限。
9. 测试脚本。

### 处理 Web 表单

Perl CGI 脚本最常见的用途之一是处理从 Web 表单传入的数据。以下是此用途的一个示例：

1. 键入 `vi ~/public_html/bin/info_form.cgi` 以创建并打开脚本文件。
2. 通过以下行告诉系统你正在编写一个 Perl 脚本：

```perl
#!/usr/bin/perl
```

3. 通过以下行告诉系统为此脚本包含 CGI 模块（本示例中已安装）：

```perl
use CGI;
```

4. 你需要一个表单来配合此示例。由于这不是一本关于 HTML 的书，我将只在这里给出表单代码：

```html
<FORM METHOD="POST" ACTION="http://www.domain.ext/~user/bin/info_form.cgi">  
<P>Please fill in the following information.</P>  
<P>First Name: <INPUT TYPE="text" NAME="fname" SIZE="20"></P>  
<P>Last Name: <INPUT TYPE="text" NAME="lname" SIZE="20"></P>  
<P>Gender: <INPUT TYPE="radio" VALUE="female" CHECKED NAME="gender">Female  
<INPUT TYPE="radio" NAME="gender" VALUE="male">Male</P>  
<P>Occupation: <SELECT SIZE="1" NAME="occupation">  
<OPTION>Consultant</OPTION>  
<OPTION>Programmer</OPTION>  
<OPTION>Student</OPTION>  
<OPTION>Writer</OPTION>  
</SELECT></P>  
<P><INPUT TYPE="submit" VALUE="Submit" NAME="B1">  
<INPUT TYPE="reset" VALUE="Reset" NAME="B2"></P>  
</FORM>
```

此表单生成图 21.1 中所示的页面。

5. 读取你从 Web 页面收集到的数据。你可以使用数组结合 `&ReadForm` 参数来执行此操作，格式如下：

```perl
&ReadForm(*forminput);
```
