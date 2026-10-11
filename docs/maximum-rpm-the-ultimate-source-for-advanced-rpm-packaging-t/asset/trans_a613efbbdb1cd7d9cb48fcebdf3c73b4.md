

## 5.2.2.11.6. 数组迭代器

对于每个已安装的软件包，按安装时间排序。查看可用的标签，我们发现 INSTALLTIME。太好了！看起来这很简单：

```bash
# rpm -qa --queryformat '%{NAME} was installed on %{INSTALLTIME}\n'
setup was installed on 845414601
pamconfig was installed on 845414602
filesystem was installed on 845414607
...
rpm was installed on 851659311
pgp was installed on 846027549
#
```

嗯，输出内容很多，但实用性不高。那些数字是什么？RPM 没有撒谎——它们是软件包的安装时间。问题在于，这些时间是以操作系统内部使用的数字形式显示的，而人类喜欢看日、月、年等信息。

幸运的是，有一种修饰符正好适用于这种情况。该修饰符名为 :date，它紧跟在标签名称之后。让我们再次尝试示例，这次使用 :date：

```bash
# rpm -qa --queryformat '%{NAME} was installed on %{INSTALLTIME:date}\n'
setup was installed on Tue Oct 15 17:23:21 1996
pamconfig was installed on Tue Oct 15 17:23:22 1996
filesystem was installed on Tue Oct 15 17:23:27 1996
...
rpm was installed on Thu Dec 26 23:01:51 1996
pgp was installed on Tue Oct 22 19:39:09 1996
#
```

这样理解起来就容易多了，不是吗？

以下是可用的修饰符列表：

- :date 修饰符以人类可读的形式显示日期。它将 846027549 转换为 Tue Oct 22 19:39:09 1996。
- :perms 修饰符以易读格式显示文件权限。它将 -32275 转换为 -rwxr-xr-x。
- :deftags 修饰符以人类可读的形式显示在依赖项处理中使用的版本比较标志。它将 12 转换为 >=。
- :fflags 修饰符：如果文件被标记为配置文件，则显示 c；如果被标记为文档文件，则显示 d；否则为空白。因此，2 变为 d。

到目前为止，我们一直在使用代表单个数据项的标签。例如，每个软件包只有一个名称或安装日期。然而，其他标签可以代表许多不同的数据片段。其中一个这样的标签是 FILENAMES，它可用于显示软件包中包含的所有文件名称。

让我们组合一个格式字符串，显示软件包名称，然后显示该软件包包含的每个文件的名称。我们先在 adduser 软件包上尝试，因为它只包含一个文件：

```bash
# rpm -q --queryformat '%{NAME}: %{FILENAMES}\n' adduser
adduser: /usr/sbin/adduser
#
```

嘿，不错：一次就成功了。现在让我们在一个包含多个文件的软件包上试试：

```bash
# rpm -q --queryformat '%{NAME}: %{FILENAMES}\n' etcskel
etcskel: (array)
#
```

嗯。出了什么问题？之前是有效的。嗯，之前有效是因为 adduser 软件包只包含一个文件。FILENAMES 标签指向名称数组，所以当软件包中有一个以上的文件时，就会出现问题。

但有解决方案。它被称为迭代器。迭代器可以遍历数组中的每个条目，并在遍历过程中生成输出。当方括号包围一个或多个标签和字面文本时，就创建了迭代器。由于我们要遍历 FILENAMES 数组，让我们将该标签放入迭代器中：

```bash
# rpm -q --queryformat '%{NAME}: [%{FILENAMES}]\n' etcskel
etcskel: /etc/skel /etc/skel/.Xclients /etc/skel/.Xdefaults /etc/skel/.ba
#
```

输出更多了：它在一长行中直接滚出了屏幕。问题在哪里？我们在迭代器内没有包含换行转义序列。让我们再试一次：

```bash
# rpm -q --queryformat '%{NAME}: [%{FILENAMES}\n]' etcskel
etcskel: /etc/skel
/etc/skel/.Xclients
/etc/skel/.Xdefaults
/etc/skel/.bash_logout
/etc/skel/.bash_profile
/etc/skel/.bashrc
/etc/skel/.xsession
#
```

这就合理多了。如果需要，我们可以在迭代器内放入另一个与文件相关的标签。如果包含 FILESIZES 标签，我们就能看到每个文件的名称，以及它的大小：

```bash
# rpm -q --queryformat '%{NAME}: [%{FILENAMES} (%{FILESIZES} bytes) \n]' etcskel
etcskel: /etc/skel (1024 bytes)
/etc/skel/.Xclients (551 bytes)
/etc/skel/.Xdefaults (3785 bytes)
/etc/skel/.bash_logout (24 bytes)
/etc/skel/.bash_profile (220 bytes)
/etc/skel/.bashrc (124 bytes)
/etc/skel/.xsession (9 bytes)
#
```

这非常好。但如果每行都显示软件包名称、文件名和大小，那就更好了。也许如果把 NAME 标签放入迭代器中：

```bash
# rpm -q --queryformat '[%(NAME): %(FILENAMES) (%{FILESIZES} bytes) \n]'
> etcskel
etcskel: /etc/skel(parallel array size mismatch)
#
```

错误信息说明了一切。FILENAMES 和 FILESIZES 数组大小相同。NAME 标签甚至不是数组。当然大小不匹配！

### 5.2.2.11.7. 迭代单条目标签

如果标签只包含一个数据项，可以将其放入迭代器中，使其在每次迭代时显示该单项数据。这是通过在标签名称前加等号来实现的。让我们在当前示例上试试：

```bash
# rpm -q --queryformat '[%{=NAME}: %(FILENAMES) (%{FILESIZES} bytes) \n]'
> etcskel
etcskel: /etc/skel (1024 bytes)
etcskel: /etc/skel/.Xclients (551 bytes)
etcskel: /etc/skel/.Xdefaults (3705 bytes)
etcskel: /etc/skel/.bash_logout (24 bytes)
etcskel: /etc/skel/.bash_profile (220 bytes)
etcskel: /etc/skel/.bashrc (124 bytes)
etcskel: /etc/skel/.xsession (9 bytes)
#
```

关于格式字符串，基本上就这些了。现在，如果 RPM 的标准输出没有给你想要的东西，你没有理由抱怨。只需使用 --queryformat 即可！

### 5.2.2.11.8. 如果你正在好奇...

什么？你说你不知道有哪些可用的标签？你可以使用 RPM 的 --querytags 选项。当作为唯一选项使用时（即 rpm --querytags），它会生成可用标签列表。需要注意的是，RPM 显示的是完整的标签名称。例如，RPMTAG_ARCH 是完整名称，但在你的格式字符串中只需使用 ARCH 即可。以下是 --querytags 选项运行的部分示例：

```bash
# rpm --querytags
RPMTAG_NAME
RPMTAG_VERSION
RPMTAG_RELEASE
 ...
   RPMTAG_VERIFYSYSCRIPT
#
```

预先警告：完整列表相当长。在这本书撰写时，有 60 多个标签！你会注意到每个标签都以大写打印，并以 RPMTAG_ 开头。如果我们在格式字符串中使用最后一个标签 RPMTAG_VERIFYSYSCRIPT，可以用以下任何方式指定：

- %(RPMTAG_VERIFYSYSCRIPT)
- %(RPMTAG_VerifySyScript)
- %{RPM_TAG_Version}\n%{VERIFY_SCRIPT}\n%{VerifyScript}\n%{VerifyScrip}

关于标签的唯一硬性规定是，如果包含 `RPM_TAG` 前缀，则必须全部大写。这里的第四个例子展示了指定标签的传统方式：省略前缀，全部大写。然而，选择权在你。

另一件需要记住的是，并非每个软件包都具有每种类型的标签信息。在请求的信息不可用的情况下，`RPM` 将显示 `(none)` 或 `(unknown)`。还有一些标签由于种种原因，在格式字符串中使用时不会产生有用的输出。有关 queryformat 标签的全面列表，请参见附录 D，“--queryformat 的可用标签”。

## 5.2.3. 使用 `-vv` 获取大量信息

有时我们需要比 `-v` 能获取的更多信息。通过添加另一个 `v`，我们可以开始看到 `RPM` 内部工作机制的更多细节：

```bash
# rpm -qvv rpm
D: opening database in /var/lib/rpm/
D: querying record number  2341208
rpm:2.3.1
#
```

以 `D:` 开头的行是通过使用 `-vv` 添加的。我们可以看到 `RPM` 数据库的位置，以及包含 `rpm-2.3.1` 软件包信息的记录编号。接下来是通常的输出。

在绝大多数情况下，不需要使用 `-vv`。它通常由在 `RPM` 本身工作的软件工程师使用，输出可能会在不通知的情况下改变。但是，它是了解 `RPM` 内部工作机制的便捷方式。

## 5.2.4. `--root <path>`：将 `<path>` 用作备用根

在查询命令中添加 `--root <path>` 会强制 `RPM` 假设由 `<path>` 指定的目录实际上是根目录。此外，`RPM` 期望其数据库驻留在相对于 `<path>` 的默认 `rpmdir` 文件条目指定的目录中。

通常，此选项仅在初始系统安装或系统通过救援磁盘启动且需要重新安装某些软件包以恢复正常操作时使用。

