

## A.1.6 如何更改文件名中的大小写

如果您出于某种原因需要将文件或目录的名称全部改为小写或全部改为大写，可以使用代码清单 A.7 中所示的命令。

### 代码清单 A.7 将所有名称改为小写

```
erikk@unixhost:> for i in `ls`; do mv $i `echo $i | tr '[A-Z]' '[a-z]'`; done
```

该 for 循环使用 `ls` 命令获取所有名称（无论是文件还是目录）的列表。借助反引号，`ls` 的输出被送入 `i`。对于找到的每个名称，使用 `mv` 命令，通过 `echo` 的输出并将其送入 `tr`（translate，转换）来改变 A 到 Z 字母的大小写，从而将所有字符改为小写。名为 `ThisText.txt` 的文件将被改为 `thistext.txt`。正则表达式 `'[A-Z]' '[a-z]'` 会处理所有大写字符并将它们转换为小写。

## A.2 Solaris 特有内容

本节包含两条针对 Solaris 管理员的提示。

### A.2.1 prstat

名为 `prstat` 的程序是所有较新的 Solaris 发行版的一部分。它的输出与 `top` 类似，但遗憾的是，它不能像 `top` 那样以交互方式使用。如果您在 Solaris 机器上无法安装 `top`，那么可以使用 `prstat` 来代替。这里提到该程序，是因为没有多少 Solaris 用户知道它的存在。

### A.2.2 注册 Solaris 系统

关于此提示有一点说明：您应该向 Sun Microsystems 注册您的 Solaris 系统。但如果您必须部署大量系统，那么在安装操作系统时逐一注册每个系统，充其量也只是耗时。您应该改为向制造商一次性注册所有系统。代码清单 A.8 展示了如何禁用注册程序。

### 代码清单 A.8 在 Solaris 中禁用注册

```
root@unixhost> cat DISABLE=1 >> /etc/default/solregis
```

再次强调，系统是应该注册的；代码清单 A.8 中的命令展示了如何在例如部署 200 多台系统时，避免在每台系统上逐一执行注册。

## A.3 sed 流编辑器

在每个 *NIX 系统上，`sed` 流编辑器是一个经常被忽视的工具。它的能力并不那么显而易见，有时甚至隐藏得很深。该程序旨在将文本文件作为流来处理，并将修改后的文件再次输出到 stdout。文件大小或多或少无关紧要，因为输出可以再次发送到文件。这意味着该程序能够处理的文件大小几乎不受限制。

### A.3.1 在找到搜索结果后创建空行

如果您需要使用编辑器编辑 XML 文件，那么根据文件的大小和复杂程度，该过程可能会非常繁琐且容易出错。假设您要编辑一个以 DocBook 格式组织的文件（这意味着章节层级由嵌套的 <sect1>、<sect2>、<sect3> 和 <sect4> 标签组成），并且希望通过在每个 <sect1> 标签上方插入一个空行来简化文件内的导航。您可以使用 XSLT 样式表来生成这种格式，但结果不值得为创建样式表所花费的时间。代码清单 A.9 演示了如何使用 sed 达到同样的效果。

### 代码清单 A.9 使用 sed 插入空行

```
...
but there will be times when proper documentation really
saves your day.</para>
<sect1 id="environment">
<title>Environment</title>
<para>There are a lot of settings concerning the environment
variables on a system, which likely will give you a headache,
to say the least.</para>
<sect2 id="env_path">
<title>The <envar>PATH</envar> variable</title>
<para>If the <envar>PATH</envar> variable looks like
this:</para>
<screen>
...
erik@unixhost> sed '/</sect1/{x;p;x}' exchap1.xml
...
```

```
but there will be times when proper documentation really
saves your day.</para>

<sect1 id="environment">
<title>Environment</title>
<para>There are a lot of settings concerning the environment
variables on a system, which likely will give you a headache,
to say the least.</para>
<sect2 id="env_path">
<title>The <userinput>$PATH</userinput> variable</title>
<para>If the <envar>$PATH</envar> variable looks like
this:</para>
<screen>
...
```

在代码清单 A.9 中，`sed` 被指示搜索包含 `<sect1>` 的行。如果找到该字符串，`sed` 会先输出一个空行，然后再输出找到的那一行。由于处理是以流的方式在文件上进行的，因此文件大小对您来说无关紧要。如果您之后用来处理 XML 文件的程序无法处理这些多出的空行，则可以使用命令 `sed '/^$/d'` 删除这些空行。您只需要知道，该命令会删除流中的所有空行。

### A.3.2 删除行首空格和制表符

如果您收到的文本文件包含行首空格或制表符（Tab）字符，而您需要去掉它们，可以使用 `sed` 来实现。代码清单 A.10 演示了具体做法。请注意，在 `[` 和 `]` 之间的字符串需要按以下方式输入：空格、Ctrl-V、Tab。

### 代码清单 A.10 删除行首空白

```
erikk@unixhost> cat leadwhite.txt
This is line 1.
    This is line 2.
        This is line 3.

This is line 4.
    This is line 5.
This is line 6.

erikk@unixhost> sed 's/[  ]*//' leadwhite.txt
This is line 1.
This is line 2.
This is line 3.
```

