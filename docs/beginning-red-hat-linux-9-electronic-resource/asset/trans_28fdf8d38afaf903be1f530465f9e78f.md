

因此，请避免使用能在字典中找到的密码（任何语言均可），或这些词的变体（例如将 i 改为 1，或将 o 改为 0，或者添加数字）；避免使用认识你的人可能猜到的密码（如家庭成员或宠物的名字）；以及避免以系统化方式生成的任何内容。请包含标点符号和其他符号，并利用 Red Hat Linux 9 使用 MD5 密码哈希这一事实，该哈希允许密码长度最长为 15 个字符。

> 然而，某些字符不应包含在密码中，因为它们可能被误解释为终端控制字符，并在登录时导致问题。请避免使用 @、#、[退格] 以及其他控制字符。

例如，以下是一些弱密码：

- Fred123
- Asdfghj（键盘上的简单模式）
- B10n1c（对字典单词的琐碎修改）
- Nitsuob（宠物名字的反向拼写）

这些本应是强密码，除非它们被收录在这本书中发布：

- Xz$!q)_2+!
- 3#&-Aa&yTy?
- aP^Lj+~rZxp]

但是，请确保你能**记住**你的密码，这样你就不必把它写下来。一旦你那样做了，你就是在削弱它的安全性。键盘下面的一张纸条是致命破绽！

# 检查密码

对黑客有用的密码破解程序对我们同样有用，我们可以使用它们来识别系统中的弱密码。然后，我们可以在黑客破解之前让违规用户更改密码。其中最著名的程序之一 simply 被称为 Crack。构建和安装它需要做一些工作，因此我们将在这里逐步进行。这一次，我们会随做随解释，而不是等到完成后再说。

Crack 是一个 2.5MB 的下载文件。如果你不想下载它，可以跳至“运行 Crack”部分，我们稍后会在那里与你汇合。

## 为 Crack 程序创建存放处

在我们开始设置 Crack 程序之前，我们需要为它创建一个存放处。最好为我们自己构建和安装的程序创建独立的目录（而不是从 RPM 包安装），以免它们与系统安装的包发生冲突。

> Crack 运行不需要 root 权限（但我们必须是 root 才能访问 shadow 密码以便稍后供 Crack 使用），因此我们将以普通无特权用户身份下载、配置和构建它。

1. 我们首先要做的是为 Crack 创建一个存放处。打开一个终端窗口（主菜单 | 系统工具 | 终端），并在提示符下输入以下命令：

```bash
% cd
% pwd
% mkdir crack
```

单独使用 cd 命令会将当前工作目录设置为运行该命令用户的**主目录**。对于新打开的终端会话，这通常就是当前目录，但我们在此包含它以防你在现有窗口中尝试此操作。pwd 命令显示当前工作目录，以确认我们身处预期的位置，然后 mkdir 命令创建一个名为 crack 的目录。我们将在此安装 Crack 程序。

2. 通过 Mozilla 网页浏览器下载 Crack 程序是最简单的方法。启动浏览器，然后指向 ftp://ftp.cert.dfn.de/pub/tools/password/Crack/，你应该会看到一个目录中的文件列表。点击名为 Crack_5.0a.tar.gz 的文件，当出现对话框询问你要做什么时，选择“保存到磁盘”并点击“确定”。浏览至你刚刚创建的 crack 目录并点击“确定”。

> 如果连接到上述 FTP 站点遇到困难，你可以尝试使用 ftp://ftp.cerias.purdue.edu/pub/tools/unix/pwutils/crack/ 作为替代。

3. 下一步是解包下载的文件。文件末尾的 .tar.gz 表明它是一个**TAR**（Tape **AR**chive，磁带**归档**）格式文件，且经过 GNU **Zip** 压缩。（你有时会在文件末尾看到 .tgz 来表示相同含义。）因此，我们需要解压并**解包**该文件。

回到终端窗口并输入以下命令：

```bash
% cd crack
% tar -xzvf Crack_5.0a.tar.gz
```

tar 命令从名为 Crack_5.0a.tar.gz（-f Crack_5.0a.tar.gz）的压缩 tar 文件中提取文件（x 选项），并在提取时打印文件名（v 选项）。注意，文件被放入 c50a/ 下的目录中，并且目录已按需创建：

![](img/b852150740856958b10aff9e8c9d2adc_515_0.png)

4. 现在，我们需要对 Crack 源代码进行一些配置更改，以便它能在我们的 Red Hat Linux 系统上成功构建和运行。首先，我们需要编辑 Crack 脚本。切换到 c50a 目录并通过运行以下命令在 Gnome 文本编辑器中打开 Crack：

```bash
% cd c50a
% gedit Crack
```

5. 会弹出一个文本编辑器窗口。滚动到文件中包含以下内容的部分：

```text
#
# now pick your compiler
#
```

6. Red Hat Linux 附带了名为 `gcc` 的 GNU C 编译器，因此我们需要使用 `gcc 2.7.2` 部分（即使我们有 gcc 版本 3.2）。在 vanilla unix cc 的行开头添加 # 字符将其变成注释（这个过程称为**注释掉**代码），并移除 `"gcc 2.7.2"` 部分对应行中的相同字符。我们还需要使用 `stdlib crypt()` 例程，因此移除 `LIBS=...` 行开头的 #。

完成后，修改后的 Crack 文件应该如下所示：

![](img/b852150740856958b10aff9e8c9d2adc_516_0.png)

7. 保存更改并退出 `gedit`。

8. Red Hat Linux 9 不使用标准的 DES 算法加密密码，而是使用基于 MD5（消息摘要 5）的更强算法。Crack 默认设置为使用 DES，因此我们需要更改这一点。以下步骤来自 Crack 5.0a 的 README 文件，请在命令行提示符下输入：

```bash
% mv src/libdes src/libdes.orig
% cd src/util
% cp elcid.c,bbsd elcid.c
```

如果提示是否覆盖 `elcid.c`，请输入 `y`。

9. 既然我们在这里，还有另一个小修改需要做出。Red Hat 9 的 shadow 密码文件使用了出厂版本的 Crack 解释为无效（因为它们不在有效字符列表中）的盐值字符。为了练习目的，我们将修改检查哈希密码有效性的例程以接受这些字符。出厂的例程检查**密文**（哈希密码）中的每个字符是否在允许字符列表中。我们将逻辑颠倒，检查没有字符在禁止字符列表中。

通过输入 `gedit elcid.c` 编辑 `elcid.c` 源文件。找到函数 `elcid_invalid(ciphertext)` 并进行以下三项更改：

- 将变量 `validchars` 的名称更改为 `invalidchars`。
- 将该变量的值更改为 `!`。
- 移除以 `if (!strchr...` 开头的行中的 `!`，以反转逻辑意义。

完成后，它应该如下所示：

```c
int
elcid_invalid(ciphertext)    /* check validity of a ciphertext */
char *ciphertext;
{
   int i;
   int retval;
   static char invalidchars[] = "!";

   retval = 0;

   for (i = 0; i < CIPHERTEXTSIZE && ciphertext[i]; i++)
   {
      if (strchr(invalidchars, (int) ciphertext[i]))
      {
         retval++;
      }
   }

   return (retval);
}
int
```

10. 保存更改并退出 gedit。

**11.** 现在我们可以编译 Crack 程序了。这是通过调用带有 -makeonly 开关的 Crack 脚本来完成的。因此，切换目录回 $HOME/crack/c50a 并运行以下命令：

```bash
$  ./Crack  -makeonly
```

> *注意，我们需要通过提供目录 -./* 来指定在哪里找到 Crack 程序。
> *这意味着当前目录。与 Microsoft Windows 不同，Linux 和其他 Unix 变体除非明确指示，否则不会将当前目录包含在搜索路径中。对于 root 账户来说，这永远不是一个好主意，因为你确实希望确保 root 用户运行的是正确系统位置中的程序，而不是碰巧具有相同名称的其他程序。*

**12.** 当 Crack 以 -makeonly 选项调用时，它会生成所需的程序文件。确保它以消息 Crack: makeonly done 结束：

**13.** 接下来，我们需要创建 Crack 将用于尝试猜测系统密码的密码字典。通过运行 ./Crack -makedict 来完成：

**14.** 同样，确保此操作以消息 Crack: makedict done 结束。

# 获取供 Crack 工作的加密密码

在我们试用新构建的 Crack 程序之前，我们需要提供给它一些要处理的密码。Crack 所需的信息在 Red Hat Linux 9 系统中保存在 */etc/passwd* 和 */etc/shadow* 中，并且这些需要合并到一个文件中。幸运的是，Crack 附带了一个实用程序，可以为我们完成此任务。

注意，我们需要是 root 才能读取 */etc/shadow*，并且由于合并后的文件包含对潜在黑客有用的信息（来自 shadow 密码文件的加密密码），我们需要确保该文件也具有受限访问权限。最好的方法是创建一个具有正确权限（通过设置我们的 umask）的空文件，然后将敏感数据追加到文件中。（我们可以创建具有默认权限的文件然后收紧它们，但理论上存在有人在我们更改权限之前打开文件的可能性。）我们将文件的所有权更改回我们要运行 Crack 的用户，以避免必须作为 root 进行此操作。

因此，运行以下命令以创建适合 Crack 处理的合并文件：

```bash
$  su root
#  umask 077
#  touch passwords.dat
#  scripts/shadowrg.sv > passwords.dat
#  chown userl passwords.dat
#  ls -l passwords.dat
#  exit
```

