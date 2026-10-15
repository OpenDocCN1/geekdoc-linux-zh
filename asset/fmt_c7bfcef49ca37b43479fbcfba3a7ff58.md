
```
cd /usr/src/redhat/BUILD
rm -rf cdplayer-1.0
mkdir -p cdplayer-1.0
cd cdplayer-1.0
gzip -dc /usr/src/redhat/SOURCES/cdplayer-1.0.tgz | tar -xvvf -
if [ $? -ne 0 ]; then
exit $$
fi
cd cdplayer-1.0
chown -R root.root
chmod -R a+rx,g-w,o-w
```

其结果是解压无顶层目录的 tar 文件的正确命令序列。

### 在多源码 Spec 文件中使用 `%setup`

如果你觉得这些关联的选项对于解压单个源码文件来说多此一举，那么你是正确的。这些选项的真正目的是为了将多个归包合并成一个可构建的实体。让我们看看它们在这种环境下是如何工作的。为了这个示例，我们的 spec 文件将有以下源码标签：

```
source: source-zero.tar.gz
source1: source-one.tar.gz
source2: source-two.tar.gz
```

是的，源码标签应该指向源码。解压第一个源码很难；要求的是使用不带选项的 `%setup`：它产生以下命令：

```
cd /usr/src/redhat/BUILD
rm -rf cdplayer-1.0
gzip -dc /usr/src/redhat/SOURCES/source-zero.tar.gz | tar -xvvf -
if [ $? -ne 0 ]; then
  exit $?
fi
cd cdplayer-1.0
cd /usr/src/redhat/BUILD/cdplayer-1.0
chown -R root.root
chmod -R a+rx,g-w
```

如果 `source-zero.tar.gz` 不包含顶层目录，我们可以通过添加 `-c` 选项来创建一个：`%setup -c` 的结果是：

```
cd /usr/src/redhat/BUILD
rm -rf cdplayer-1.0
mkdir -p cdplayer-1.0
cd cdplayer-1.0
gzip -dc /usr/src/redhat/SOURCES/source-zero.tar.gz | tar -xvvf -
if [ $? -ne 0 ]; then
  exit $?
fi
cd cdplayer-1.0
chown -R root.root
chmod -R a+rx,g-w
```

当然，如果顶层目录与包名不匹配，可以添加 `-n` 选项：`%setup -n` 的结果是：

```
cd /usr/src/redhat/BUILD
rm -rf cdather
gzip -dc /usr/src/redhat/SOURCES/source-zero.tar.gz | tar -xvvf -
if [ $? -ne 0 ]; then
  exit $?
fi
cd cdather
cd /usr/src/redhat/BUILD/cdather
chown -R root.root
chmod -R a+rx,g-w
```

或者 `%setup -c -n cdather` 的结果是：

```
cd /usr/src/redhat/BUILD
rm -rf cdather
mkdir -p cdather
cd cdather
gzip -dc /usr/src/redhat/SOURCES/source-zero.tar.gz | tar -xvf -
if [ $? -ne 0 ]; then
  exit $
fi
cd cdather
cd /usr/src/redhat/BUILD/cdather
chown -R root.root
chmod -R a+rx,g-w
```

现在添加第二个源码文件。这里变得有点有趣了。首先，我们需要识别我们讨论的是哪个源码标签（因此是哪个源码文件）。根据源码包的特性，我们需要使用 `-a` 或 `-b` 选项。对于这个示例，假设我们需要 `-a` 选项。加上 "1" 来指向 `source1` 文件中的源码，我们得到：

```
%setup -a 1
```

由于我们已经看到使用 `-a` 或 `-b` 选项会导致重复解压，我们需要通过添加 `-T` 选项来禁用默认解压：

```
%setup -T -a 1
```

接下来，我们需要确保顶层目录不被删除。否则，我们刚刚解压的第一个源码就会消失。这意味着我们需要包含 `-D` 选项来防止这种情况发生。添加这个最终选项，并将完整的宏包含在我们的 `%prep` 脚本中，我们得到：

```
%setup
%setup -T -D 1
```

这将导致以下命令：

```
cd /usr/src/redhat/BUILD
rm -rf cdplayer-1.0
gzip -dc /usr/src/redhat/SOURCES/source-zero.tar.gz | tar -xvvf -
if [ $? -ne 0 ]; then
  exit $
fi
cd cdplayer-1.0
cd /usr/src/redhat/BUILD/cdplayer-1.0
chown -R root.root
chmod -R aRX,g,w,o-w
cd /usr/src/redhat/BUILD
cd cdplayer-1.0
gzip -dc /usr/src/redhat/SOURCES/source-one.tar.gz | tar -xvvf -
if [ $? -ne 0 ]; then
  exit $
fi
cd cdplayer-1.0
cd /usr/src/redhat/BUILD/cdplayer-1.0
chown -R root.root .
chmod -R aRX,g,w,o-w
```

到为止一切顺利。让我们包含最后一个源码文件，但放在 `cdplayer-1.0` 下名为 `database` 的子目录下。在这种情况下我们可以使用 `%setup` 吗？

如果 `source-two.tgz` 创建了 `database` 子目录，我们可以使用。否则，就需要手动操作。对于我们的示例，假设 `source-two.tgz` 创建时没有包含 `database` 子目录，所以我们需要自己动手。这里是我们的 `%prep` 脚本：

```
%setup
%setup -T -D -a 1
mkdir database
cd database
gzip -dc /usr/src/redhat/SOURCES/source-two.tar.gz | tar -xvvf -
```

以下是生成的脚本：

```
cd /usr/src/redhat/BUILD
rm -rf cdplayer-1.0
gzip -dc /usr/src/redhat/SOURCES/source-zero.tar.gz | tar -xvvf -
if [ $? -ne 0 ]; then
  exit $$
fi
```

## 13.4 宏：软件包构建者的简用简写

```
cd cdplayer-1.0
gzip -dc /usr/src/redhat/SOURCES/source-one.tar.gz | tar -xvvf -
if [ $ -ne 0 ]; then
exit $?
fi
mkdir database
cd database
gzip -dc /usr/src/redhat/SOURCES/source-two.tar.gz | tar -xvvf -
```

我们添加的用于解压最后一组源码的这三个命令目的是将其添加到 `%prep` 脚本的末尾。

使用 `%setup` 宏的结论是，你可能可以让它实现你想要的功能，但不要害怕尝试。即使无法使用 `%setup`，手动添加必要的命令来完成工作也是容易的。最重要的是，在测试你的 `%setup` 宏时，务必使用 `--test` 选项，这样你就可以看到它们被转换成了哪些命令。

接下来，让我们来看看 RPM 的第二个宏 `%patch`。

## 13.4.2 `%patch` 宏

`%patch` 宏正如其名称所示，用于对解压后的源码应用补丁。在下面的示例中，spec 文件包含以下 patch 行：

```
patch0 patch-zero
patch1 patch-one
patch2 patch-two
```

在最简单的情况下，可以在不带任何选项的情况下调用 `%patch` 宏：

以下是生成的命令：

```
echo "Patch #0"
patch -p0 -s < /usr/src/redhat/SOURCES/patch-zero
```

`%patch` 宏很好很好显示正在应用补丁的消息，并调用 `patch` 命令执行实际工作。`patch` 命令有两个选项：

- `-p` 选项：指导 `patch` 从文件名开头移除指定数量的斜杠（以及中间的目录）。在这种情况下，什么都不会被删除。
