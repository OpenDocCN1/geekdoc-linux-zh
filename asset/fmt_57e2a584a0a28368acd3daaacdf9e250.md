
- - `[bdudbs]` - 更新到 `linux-4.12.10`。修复 `#4126`。

- - `2017-09-01`

- - `[bdudbs]` - `LFS-8.1` 发布。

## 1.4 资源

### 1.4.1 常见问题 (FAQ)

如果你在构建 LFS 过程中遇到任何错误、有任何疑问或认为书中存在错误，请先查阅常见问题（FAQ），地址位于：http://www.linuxscratch.org/faq。

### 1.4.2 邮件列表

`linuxscratch.org` 服务器托管了多个用于 LFS 项目的邮件列表。这些列表包括开发列表和支持列表。如果 FAQ 无法解决你的问题，下一步是搜索邮件列表：http://www.linuxscratch.org/search。

有关列表的订阅方式、存档位置以及更多信息，请访问 http://www.linuxscratch.org/mail。

### 1.4.3 即时聊天 (IRC)

LFS 社区的许多成员可以通过即时聊天（IRC）提供帮助。在使用之前，请确保你的问题没有在 FAQ 或邮件存档中被解答。你可以访问 IRC 网络：`irc.freenode.net`。频道名为 `#LFS-support`。

### 1.4.4 镜像站点

LFS 项目拥有全球镜像，方便访问网站和下载所需的软件包。请访问 http://www.linuxscratch.org/mirrors.html 查看镜像列表。

### 1.4.5 联系方式

请将你的所有问题和反馈发送至 LFS 邮件列表（见上文）。

## 1.5 帮助

如果你在阅读本书时遇到问题或疑问，请查阅 http://www.linuxscratch.org/faq/#generalfaq 页面。很多问题在上面已有答案。如果你的问题在该页面上没有找到，请尝试寻找问题所在。以下提示将为你提供一些指导：http://www.linuxscratch.org/hints/downloads/files/errors.txt。

我们有一个非常棒的 LFS 社区，愿意通过邮件列表和 IRC 提供帮助。但我们每天都会收到许多支持请求，其中许多通过先查看 FAQ 和搜索邮件列表就可以轻松解答。为了让我们能提供最佳帮助，你需要先进行自主研究。这让我们能够关注更罕见的支持需求。如果你的搜索没有结果，请在请求帮助时包含所有相关信息（见下文）。

### 1.5.1 需要说明的内容

除了对问题的简要说明外，任何请求中包含的关键信息有：

- 使用书籍的版本
- 宿主机发行版及版本
- 遇到的具体错误信息
- `configure` 脚本的输出
- 说明你是否偏离了书籍

### 1.5.2 configure 脚本

如果在运行 `configure` 脚本时出现任何问题，请检查屏幕输出以确定原因。

### 1.5.3 编译问题

屏幕输出和各种文件的内容都是很有用的。以下是编译失败时应包含的内容示例：

- `Texinfo-4.7`
- `Xz-5.0.0`

# 重要事项

> 注意，上述提到的符号链接对于使用本书中的指令构建 LFS 系统是必须的。指向其他软件（如 `dash`、`mawk` 等）的符号链接可能可以工作，但 LFS 开发团队并未对其进行测试或支持，并且可能需要根据指令或对某些软件包使用额外的补丁。

要检查你的主机系统是否具有所有适当的版本以及具备编译程序的能力，请运行以下命令：

```bash
cat > version-check.sh << "EOF"
#!/bin/bash
## 列出关键开发工具版本号的简单脚本
export LC_ALL=C
bash --version | head -n1 | cut -d " ' -f2-4
MYS=$(readlink /bin/sh -f /bin/sh)
echo "/bin/sh -> $MYS"
echo $MYS | grep -q bash | echo ERROR: /bin/sh does not point to bash
echo -n "Binutils: ; ld --version | head -n1 | cut -d " " -f3-
bison --version | head -n1

if [ -h /usr/bin/yacc ]; then
echo "/usr/bin/yacc -> `readlink -f /usr/bin/yacc`"
elif [ -x /usr/bin/yacc ]; then
echo yacc is `/usr/bin/yacc --version | head -n1`
else
echo "yacc not found"
fi

pip2 --version 2>&1 < /dev/null | head -n1 | cut -d " " -f1,6-
echo -n "Coreutils: ; chown --version | head -n1 | cut -d ") -f2
diff --version | head -n1
find --version | head -n1
gawk --version | head -n1

if [ -h /usr/bin/awk ]; then
echo "/usr/bin/awk -> `readlink -f /usr/bin/awk`"
elif [ -x /usr/bin/awk ]; then
echo awk is `/usr/bin/awk --version | head -n1`
else
echo "awk not found"
fi
gcc --version | head -nl
g++ --version | head -nl
ld --version | head -nl | cut -d" " -f2- # glibc version
grep --version | head -nl
gzip --version | head -nl
cat /proc/version | head -nl
m4 --version | head -nl
make --version | head -nl
patch --version | head -nl
echo Perl`perl -V:version`
sed --version | head -nl
tar --version | head -nl
makeinfo --version | head -nl
xz --version | head -nl
echo 'int main(){}' > dummy.c && g++ -o dummy.c
if [ -x dummy ];
then
    echo "g++ compilation OK";
else
    echo "g++ compilation failed"
fi
rm -f dummy.c dummy
EOF
bash version-check.lfs
```

LFS 设计为在一个会话中完成构建。这意味着指令假设系统在过程中不会被关闭。但这并不意味着系统必须在一个会话中完成。问题在于，如果在不同的时间点恢复 LFS，某些过程必须在重启后重新完成。

### 2.3.1. 第 1–4 章

这些章节在主机系统上完成。重启时，请注意以下几点：

- *在 2.4 节之后以 root 用户身份执行的操作需要为 root 用户设置 LFS 环境变量。*

### 2.3.2. 第 5 章

- 必须挂载 `/mnt/lfs` 分区。
- 第 5 章中的所有指令必须由用户 `lfs` 执行。在执行第 5 章的任何任务之前，必须执行 `su -fs`。
- 第 5.3 节“通用编译指令”中的过程至关重要。如果对安装软件包有任何疑问，请确保删除之前解压过的 tar 包，重新提取软件包文件，并完成该节的所有指令。

### 2.3.3. 第 6–8 章

- 必须挂载 `/mnt/lfs` 分区。
- 进入 `chroot` 时，必须为 root 设置 LFS 环境变量。否则，LFS 变量不会被设置。
- 必须挂载虚拟文件系统。这可以在进入 `chroot` 之前或之后完成，通过切换到主机虚拟终端并以 root 身份运行第 6.2.2 节“挂载并填充 `/dev`”和第 6.2.3 节“挂载虚拟内核文件系统”中的命令。

## 2.4. 创建新分区

与其他操作系统一样，LFS 通常安装在专用分区上。构建 LFS 的推荐方法是使用空分区，或者如果你有足够的未分区空间，也可以创建一个。

最小系统需要一个大约 6 GB 的分区，这足够存储所有的 tar 包和编译软件包。然而，如果 LFS 系统打算作为主 Linux 系统，可能需要额外空间。20 GB 的分区大小对于增长是合理的。LFS 系统本身不会占用多少空间。需要一个较大的分区来提供足够的临时存储，并在 LFS 完成后。此外，编译软件包可能需要大量磁盘空间，在安装后将回收。

由于并不总是有足够的内存（RAM）用于编译，使用小型磁盘分区作为交换空间是一个好主意。该分区用于内核很少使用的数据，并为活动进程留出更多内存。LFS 交换分区可以与主机系统使用的相同，在这种情况下没有必要创建另一个。
