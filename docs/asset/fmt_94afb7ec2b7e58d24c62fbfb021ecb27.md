
## 表 6-3. Tripwire 命令和文件

| 路径 | 描述 |
| :--- | :--- |
| `/etc/tripwire/tw.txt` | 加密策略文件 |
| `/etc/tripwire/twcfg.txt` | 明文配置文件 |
| `/etc/tripwire/twpol.txt` | 明文策略文件 |
| `/var/lib/Tripwire/report` | 存储 Tripwire 报告 |
| `/var/lib/tripwire` | 存储 Tripwire 数据库 |

要自定义配置和策略文件，你需要修改 `/etc/tripwire` 目录中可编辑的版本。这些文件有两个版本：一个是你可以编辑以自定义配置的 `.txt` 文件，另一个是由 `twinstall.sh` 脚本生成的。Tripwire 策略文件存储了监控哪些文件和程序以及如何检查它们的规则。规则由一个对象和一个属性掩码组成。对象是一个目录或文件，其条目规则包含路径。

属性掩码通过 `->` 符号分隔，整个规则以分号 `;` 结束。每个对象只能有一个规则。属性掩码是一系列单字符代码，表示不同的文件和目录特征，例如 `p` 表示权限，`s` 表示大小，`t` 表示类型，`m` 表示 MD5 值。你可以使用 `+` 或 `-` 符号来指定是否检查某项属性。`+p` 表示检查对象的权限，`-p` 表示不检查。查看 `twpolicy` 手页可获得属性代码的完整列表。在下一个示例中，`/chris/myfile` 对象将检查其权限和大小：

```
/chris/myfile -> +ps;
```

Tripwire 还定义了几个内置变量，用于存储不同类型对象的标准属性集。例如，`ReadOnly` 列出了应具有只读访问权限的文件或目录的标准属性。`Dynamic` 用于监控可能会变化的文件。它将检查这些属性（如权限）以及倾向于不改变的用户，而忽略大小和 MD5 值等易变属性。`IgnoreAll` 将仅检查文件是否存在，忽略所有其他属性。`IgnoreNone` 则将所有属性应用于文件。这可以提供高级别的安全保护。

```
/usr/bin -> ReadOnly
/usr/bin/slogin -> IgnoreNone
/usr/chris/mydoc -> Dynamic
```

你可以通过属性（如 `severity` 严重程度）进一步限定规则，以指示违规的严重程度；或者使用 `emailto` 指定在发生违规时发送消息的电子邮件地址。属性输入在规则后的括号内。多个属性之间用逗号分隔。

```
/chris/myfile -> +ps (emailto = chris@turtle.mytrek.com);
/usr/bin -> ReadOnly (severity = 70, emailto = admin@turtle.mytrek.com);
```

你还可以将规则分组并对所有规则应用相同的属性。在这种情况下，规则被包裹在大括号 `{}` 中，属性列在前面的括号中。通过此功能，你可以避免为多个文件重复输入属性。此外，你可以同时为多个文件添加属性。在以下示例中，`/chris/myfile` 和 `/chris/myproject` 目录都被分配了电子邮件地址和严重程度属性：

```
{
severity = 70,
emailto = chris@turtle.mytrek.com
}
{
/chris/myfile -> +ps;
/chris/myproject -> +sm;
}
```

![](img/95726952b50a5b7113b49b7e63a39779_142_0.png)

共有四个属性：`rulename`、`emailto`、`severity` 和 `recurse`。`rulename` 属性通常用于在一个标题下分组规则，该标题将用于 Tripwire 报告列出组中的任何违规项。`recurse` 属性指定目录的属性检查是否也适用于子目录。默认值为 `true`，设置为 `false` 则将不检查目录中的任何文件。在以下示例中，`rulename` 为上一个示例列出的规则提供了名称“Chris Important Files”。请务必用逗号分隔属性。此外，`/chris/myproject` 目录中的文件和子目录不会被检查。

```
(
rulename = "Chris Important Files"
severity = 70,
emailto = chris@turtle.mytrek.com
)
{
/chris/myfile -> +ps;
/chris/myproject -> +sm recurse = false;
}
```

Tripwire 还支持指令（directives），你可以在其中为特定主机或文件系统定义变量或规则以及全局变量。这允许管理员创建一个用于不同主机的单一策略文件（详情请见 `twpolicy` 手页）。指令以 `@@section` 开始。在标准策略文件中，你将有一个针对全局变量 `GLOBALS` 的指令，以及针对 Linux 文件系统 `FS` 的指令。`GLOBALS` 部分定义 Tripwire 文件和目录的位置。`FS` 部分设置用于不同属性集的变量，例如 `SEC_INVARIANT` 被分配给检查类型、权限、用户和组。这用于不应更改的文件和目录。你将在 `twpol.txt` 文件中找到以下内容：

```
SEC_INVARIANT = +ptpug;
```

*(注：原文后续存在大量重复的错误文本，此处已根据逻辑进行截断)*

## 第 6 章：安全配置

创建新的策略文件更为复杂，将在策略更新章节中介绍。

### 使用 Tripwire

一旦创建了配置和策略文件，你就可以通过带有 `--init` 选项调用 Tripwire 为监控的文件和程序创建签名数据库。系统最初会提示你输入本地口令，该口令是在运行 `twinstall.sh` 时指定的：

```
tripwire --init
```

Tripwire 数据库保留在 `/var/lib/tripwire` 中，并以主机名加 `.twd` 后缀命名。例如，`turtle.mytrek.com` 的 Tripwire 数据库将是 `/var/lib/tripwire/turtle.mytrek.twd`。

为了增强安全性，建议将 Tripwire 数据库存放在只读介质上，如软盘或 CD-ROM。你可以通过指定新的 Tripwire 数据库目录来重新配置，或者使用 `-d` 选项在执行 Tripwire 命令时手动指定 Tripwire 数据库的位置。

现在数据库已经创建完成，你可以使用 Tripwire 定期检查系统的完整性。你可以通过 `--check` 选项手动进行。你还可以将 `Tripwire --check` 命令设置为 cron 任务，在指定时间自动运行。Tripwire --check 命令将被放置在 `/etc/cron.daily` 文件中，并每天运行 Tripwire：

```
tripwire --check
```

Tripwire 将检查策略文件中所有的文件并生成报告。Tripwire 报告存储在根据主机名、日期时间和命文件中，后缀为 `.twr`。例如，2001 年 8 月 12 日 10:29:54 生成的报告命名为 `20010812-102954.twr`。这些文件保留在 `/var/lib/tripwire/report` 目录下。报告将列出任何违规情况，注明严重程度，并指示文件是被添加、删除还是修改了。

要查看报告，你需要使用 `twaprint` 命令的 `--print-report` 选项。你还需要使用 `-r` 选项指定你想要的文件。报告显示在标准输入上，并在屏幕上滚动。你可以将其重定向到文件进行保存，或者通过管道 `more` 或 `less` 命令以通过屏幕查看。以下示例显示了 `20010812-102954.twr` 报告，将其输出管道至 `more` 命令：

```
twprint --print-report -r /var/lib/tripwire/report/20010812-102954.twr | more
```

你也可以使用 `triprint` 查询数据库中关于特定文件的信息。使用 `--print-dbfile` 选项并指定文件名：

```
triprint --print-dbfile /etc/passwd
```

随着文件修改导致系统发生变化，你的 Tripwire 数据库可能会过。你可以使用 `--update` 选项更新 Tripwire 数据库，将报告的违规项作为正确的条目包含。你需要指定持有有效数据错误报告的特定文件。

```
tripwire --update -r /var/lib/tripwire/report/20010812-102954.twr
```
