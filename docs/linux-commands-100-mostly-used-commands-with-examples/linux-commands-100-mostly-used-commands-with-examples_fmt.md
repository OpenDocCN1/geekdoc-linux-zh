
# Linux 常用命令

## 1. ls：列出当前目录中的文件和目录。

`ls` 命令是 Linux 和类 Unix 操作系统中的一个基本命令，用于列目录中的文件和子目录。

### 示例：

- 列出当前目录中的文件和目录：

```bash
ls
```

- 列出指定目录中的文件和目录：

```bash
ls /path/to/directory
```

- 以人类可读的大小和隐藏文件长格式列出文件：

```bash
ls -l -h -a
```

- 递归地列出所有文件和目录：

```bash
ls -R
```

- 按修改时间（最新优先）对文件排序：

```bash
ls -t
```

## 2. cd：更改目录。

Linux 中的 `cd` 命令用于更改当前工作目录。它允许你通过在一个目录和另一个目录之间移动来遍历文件系统。

### 示例：

- 更改为 home 目录：

```bash
cd
```

此命令会将你带到你的 home 目录。

- 更改为指定目录：

```bash
cd /path/to/directory
```

将 `/path/to/directory` 替换为你想要进入的目录的实际路径。这是一个绝对路径的示例。

- 向上移动一级目录：

```bash
cd ..
```

此命令将你在目录结构中向上一级移动。

- 移动到父目录：

```bash
cd ../parent_directory
```

将 `parent_directory` 替换为你想要进入的父目录名称。这是一个相对路径的示例。

- 移动到子目录：

```bash
cd subdirectory
```

将 `subdirectory` 替换为你想要进入的子目录名称。这是一个相对路径的示例。

- 使用波浪号（~）表示 home 目录：

```bash
cd ~/documents
```

此命令移动到用户 home 目录内的 `documents` 目录。

- 返回上一个目录：

```bash
cd -
```

此命令将你带回上一个工作目录。

- 使用环境变量：

```bash
cd $HOME
```

此命令等效于不带任何参数的 `cd`，并将你带到你的 home 目录。

## 3. pwd：打印当前工作目录。

Linux 中的 `pwd` 命令代表 "print working directory"（打印工作目录）。它用于显示当前工作目录，该目录表示用户在文件系统中的当前位置的绝对路径。

### 示例：

- 显示当前工作目录：

```bash
pwd
```

- 显示逻辑上的当前工作目录：

```bash
pwd -L
```

- 显示物理上的当前工作目录：

```bash
pwd -P
```

## 4. mkdir：创建新目录。

Linux 中的 `mkdir` 命令用于创建目录或文件夹。它允许用户在指定位置创建一个或多个目录。

### 示例：

- 基本用法：

```bash
mkdir my_directory
```

这会在当前工作目录中创建一个名为 `my_directory` 的目录。

- 创建多个目录：

```bash
mkdir dir1 dir2 dir3
```

此命令会在当前工作目录中创建名为 `dir1`、`dir2` 和 `dir3` 的三个目录。

- 设置权限：

```bash
mkdir -m 755 my_directory
```

这会在创建名为 `my_directory` 的目录时，将权限设置为 755（所有者具有读、写和执行权限，其他用户具有读和执行权限）。

- 创建父目录：

```bash
mkdir -p path/to/my_directory
```

这会在指定路径中创建 `my_directory` 目录，以及任何必需的父目录（如果它们不存在）。

## 5. rm：删除文件或目录。

Linux 中的 `rm` 命令用于删除文件目录。它允许用户删除一个或多个文件或目录，并且不会将它们移动到回收站；相反，它会永久删除它们。

### 示例：

- 删除一个文件：

```bash
rm myfile.txt
```

此命令删除名为 `myfile.txt` 的文件。

- 删除多个文件：

```bash
rm file1.txt file2.txt
```

删除 `file1.txt` 和 `file2.txt` 两个文件。

- 删除一个目录：

```bash
rm -r mydirectory
```

递归删除名为 `mydirectory` 的目录及其内容。

- 带确认的删除：

```bash
rm -i sensitivefile.txt
```

在删除文件 `sensitivefile.txt` 之前提示用户确认。

- 强制删除：

```bash
rm -f stubbornfile.txt
```

删除文件 `stubbornfile.txt` 时不进行确认，即使它是写保护的。

## 6. cp：复制文件或目录。

Linux 中的 `cp` 命令用于将文件和目录从一个位置复制到另一个位置。它是文件操作的基本命令，属于 GNU 核心实用程序的一部分。

### 示例：

- 将文件复制到另一个位置：

```bash
cp file.txt /path/to/destination/
```

- 递归复制目录及其内容：

```bash
cp -r /path/to/source_directory/ /path/to/destination/
```

- 在覆盖现有文件前提示：

```bash
cp -i file.txt /path/to/destination/
```

- 仅当源文件较新或目标文件缺失时复制：

```bash
cp -u file.txt /path/to/destination/
```

- 创建硬链接而不是复制：

```bash
cp -l file.txt /path/to/link_destination/
```

- 复制时保留所有权和时间戳：

```bash
cp -a /path/to/source_directory/ /path/to/destination/
```

- 详细模式（显示正在复制的文件）：

```bash
cp -v file1.txt file2.txt /path/to/destination/
```

## 7. mv：移动或重命名文件或目录。

Linux 中的 `mv` 命令用于移动或重命名文件和目录。它允许你更改文件名称或将其从一个目录移动到另一个目录。

### 示例：

- 重命名文件：

```bash
mv old_file.txt new_file.txt
```

此命令将 `old_file.txt` 重命名为 `new_file.txt`。

- 将文件移动到不同的目录：

```bash
mv file.txt /path/to/destination/
```

将 `file.txt` 移动到指定的目标目录。

- 将多个文件移动到目录：

```bash
mv file1.txt file2.txt /path/to/destination/
```

将多个文件移动到指定的目标目录。

- 交互模式：

```bash
mv -i file.txt /path/to/destination/
```

如果目标文件已存在，则提示确认。

- 更新模式：

```bash
mv -u newer_file.txt /path/to/destination/
```

仅当 `newer_file.txt` 比目标中的现有文件更新时才移动。

- 详细模式：

```bash
mv -v file.txt /path/to/destination/
```

显示关于移动操作的详细信息。

## 8. touch：创建空文件或更新现有文件的时间戳。

Linux 中的 `touch` 命令用于更新文件的访问和修改时间戳，或者如果文件不存在则创建一个空文件。它是一个多功能命令，允许用户在修改文件内容之前操纵文件时间戳。

### 示例：

- 创建一个新的空文件：

```bash
touch newfile.txt
```

此命令在当前目录中创建一个名为 `newfile.txt` 的新文件。

- 更新文件的访问和修改时间戳：

```bash
touch existingfile.txt
```

此命令将 `existingfile.txt` 的访问和修改时间戳更新为当前时间。

- 仅更改访问时间：

```bash
touch -a file.txt
```

此命令仅更新 `file.txt` 的访问时间戳。

- 仅更改修改时间：



```bash
touch -m file.txt
```

此命令仅更新 `file.txt` 的修改时间戳。

- 使用指定的日期和时间：

```bash
touch -d "2023-11-10 12:30" file.txt
```

此命令将 `file.txt` 的访问和修改时间戳设置为指定的日期和时间。

- 防止创建文件：

```bash
touch -c non_existent_file.txt
```

此命令检查 `non_existent_file.txt` 是否存在；如果不存在，则不创建该文件。

## 9. cat：显示文件内容。

Linux 中的 `cat` 命令是 "concatenate"（连接）的缩写。它是一个多功能实用程序，用于显示一个或多个文件的内容、连接文件、创建新文件，并在标准输出上连接和显示它们。`cat` 命令是 Linux 中简单且经常使用的命令。

### 示例：

- 显示文件内容：

```bash
cat filename.txt
```

- 连接多个文件并显示输出：

3. 显示文件的行号和内容：

```
cat -n filename.txt
```

4. 显示不可打印字符和行尾：

```
cat -vE filename.txt
```

5. 拼接文件并创建一个新文件：

```
cat file1.txt file2.txt > newfile.txt
```

6. 显示带行号和不可打印字符的内容：

```
cat -n -vE filename.txt
```

## 10. nano 或 vim：用于创建或编辑文件的文本编辑器。

`nano` 和 `vim` 都是在 Linux 和类 Unix 操作系统中常用的文本编辑器。它们是用于从命令行编辑文本文件的强大工具。

### Nano：

`nano` 是一个简单且用户友好的文本编辑器，易于使用，尤其适合初学者。它在屏幕底部提供了一组基本命令，使不熟悉复杂键盘快捷键的用户操作更加直观。

**示例：**

要编辑名为 "example.txt" 的文件，请运行：

```
nano example.txt
```

进入编辑器后，你可以使用底部显示的命令来导航、编辑和保存文件。

### Vim：

`vim` (Vi Improved) 是一个高度可配置且功能强大的文本编辑器，是旧版 `vi` 编辑器的增强版本。它以效率高和功能集广泛著称，但与 `nano` 相比，其学习曲线更陡峭。

**示例：**

要编辑名为 "example.txt" 的文件，请运行：

```
vim example.txt
```

## 11. grep：在文件中搜索特定模式。

`grep` 是 Linux 中一个强大的命令行实用程序，用于在文件中搜索文本模式。其名称源自 ed 命令 `g/re/p` (global/regular expression/print)，该命令曾用于类似的目的。

**示例：**

- 1. 基本搜索：

```
grep "pattern" filename
```

- 2. 不区分大小写的搜索：

```
grep -i "pattern" filename
```

- 3. 在子目录中递归搜索：

```
grep -r "pattern" /path/to/directory
```

- 4. 显示行号：

```
grep -n "pattern" filename
```

- 5. 反向匹配（排除包含模式的行）：

```
grep -v "pattern" filename
```

- 6. 计算匹配行的数量：

```
grep -c "pattern" filename
```

- 7. 显示匹配行前后几行：

```
grep -A 2 -B 2 "pattern" filename
```

- 8. 带行号且不区分大小写的递归搜索：

```
grep -rin "pattern" /path/to/directory
```

## 12. chmod：更改文件权限。

`chmod` 是一个用于更改文件和目录权限的 Linux 命令。"chmod" 是 "change mode"（更改模式）的缩写，它允许你控制谁可以读取、写入和执行文件。

### 模式：

模式由三个部分组成：用户（user）、组（group）和其他人（others），每个部分都有读取（`r`）、写入（`w`）和执行（`x`）权限。此外，你可以使用数字表示法来设置权限。

- 符号表示：

  - `u` 代表用户

  - `g` 代表组

  - `o` 代表其他人

  - `a` 代表所有人（相当于 `ugo`）

- 权限符号：

  - `r` 代表读取

  - `w` 代表写入

  - `x` 代表执行

- 运算符：

  - `+` 用于添加权限

  - `-` 用于移除权限

  - `=` 用于明确设置权限

- 文件：

  指你想要修改权限的文件或目录。

**示例：**

1. 授予文件所有者读取和写入权限：

```
chmod u+rw file.txt
```

2. 移除脚本的组执行权限：

```
chmod g-x script.sh
```

3. 递归地给予目录及其内容的读取和执行权限给所有人：

```
chmod -R a+rx directory/
```

4. 使用数字表示法设置特定权限（读: 4, 写: 2, 执行: 1）：

```
chmod 754 file.txt
```

在此示例中，用户拥有读取、写入和执行权限（4+2+1 = 7），组拥有读取和执行权限（4+1 = 5），其他人只有只读权限（4）。

## 13. chown：更改文件所有者或组。

Linux 中的 `chown` 命令用于更改文件或目录的所有权。所有权指的是与文件或目录关联的用户和组。当需要将文件或目录的所有权从一个用户转移到另一个用户时，此命令特别有用。

**示例：**

- 1. 基本用法 - 更改文件的所有权：

```
chown newowner:newgroup myfile.txt
```

该命令将 `myfile.txt` 的所有权更改为用户 `newowner` 和组 `newgroup`。

- 2. 递归更改目录的所有权：

```
chown -R newowner:newgroup mydirectory
```

该命令递归地将 `mydirectory` 内所有文件和子目录的所有权更改为用户 `newowner` 和组 `newgroup`。

- 3. 详细输出：

```
chown -c newowner:newgroup myfile.txt
```

该命令提供详细输出，指示对 `myfile.txt` 所有权所做的更改。

- 4. 基于当前所有者更改所有权：

```
chown --from=currentowner:currentgroup newowner:newgroup myfile.txt
```

该命令将 `myfile.txt` 的所有权从当前所有者 `currentowner` 和组 `currentgroup` 更改为新所有者 `newowner` 和组 `newgroup`。

## 14. ps：显示正在运行的进程信息。

Linux 中的 `ps` 命令用于显示当前正在运行的进程的信息。它提供系统当前进程的快照，包括它们的进程 ID (PID)、终端关联、资源使用率以及其他详细信息。

**示例：**

1. 显示系统中所有正在运行的进程列表：

```
ps
```

2. 显示所有进程的详细信息：

```
ps -ef
```

3. 显示所有进程的完整格式列表：

```
ps -f
```

4. 显示由特定用户拥有的进程信息（将 `username` 替换为实际用户名）：

```
ps -u username
```

5. 显示树状进程层次结构：

```
ps -e --forest
```

## 15. kill：终止进程。

Linux 中的 `kill` 命令用于向进程发送信号，允许你终止或操控其行为。

**示例：**

- 1. 使用默认信号终止进程：

```
kill 1234
```

这向 PID 为 1234 的进程发送 SIGTERM 信号。

- 2. 强制终止进程：

```
kill -9 5678
```

这向 PID 为 5678 的进程发送 SIGKILL 信号，强制终止它。

- 3. 重启进程：

```
kill -HUP 9876
```

这向 PID 为 9876 的进程发送 SIGHUP 信号，通常用于重启进程。

- 4. 暂停进程：

```
kill -STOP 1111
```

这向 PID 为 1111 的进程发送 SIGSTOP 信号，使其暂停。

- 5. 恢复已暂停的进程：



```
kill -CONT 1111
```

这向 PID 为 1111 的暂停进程发送 `SIGCONT` 信号，恢复其执行。

## 16. `top`：显示实时系统统计信息。

Linux 中的 `top` 命令是一个强大的实用程序，提供系统性能的实时动态概览。它显示有关进程、系统资源使用率和其他重要统计信息。`top` 命令对于监控系统活动、识别资源消耗大的进程以及了解整体系统健康状况特别有用。

**示例：**

- 1. **显示动态概览：**

```
top
```

这将以交互模式启动 `top`，显示有关进程和系统资源的实时信息。

- 2. **设置更新间隔：**

```
top -d 5
```

以 5 秒的更新间隔启动 `top`，每 5 秒提供一次信息。

- 3. **监控特定用户的进程：**

```
top -u username
```

显示由指定用户（`username`）拥有的进程信息。

- 4. **按 PID 监控特定进程：**

```
top -p 1234,5678
```

监控指定进程 ID (PID) 的进程 - 在此示例中为 1234 和 5678。

- 5. **在特定迭代次数后退出：**

```
top -n 5
```

运行 `top` 5 次迭代后退出。

## 17. `df`：显示磁盘空间使用情况。

Linux 中的 `df` 命令用于显示文件系统上的磁盘空间使用情况。它提供有关每个已挂载文件系统的总磁盘空间、已用空间、可用空间以及已用空间百分比的详细信息。此命令对于监控磁盘空间和识别存储问题特别有用。

**示例：**

- 1. **显示所有已挂载文件系统的磁盘空间使用情况：**

```
df
```

2. 以人类可读的格式显示磁盘空间使用情况：

```
df -h
```

3. 显示磁盘空间总使用量：

```
df --total
```

4. 显示特定文件系统（例如 `/dev/sda1`）的信息：

```
df /dev/sda1
```

5. 显示文件系统的 inode 信息：

```
df -i
```

## 18. `du`：显示目录及其子目录的大小。

Linux 中的 `du` 命令用于估算文件和目录的空间使用情况。它计算目录及其子目录的大小，并以人类可读的格式显示磁盘空间使用情况。

### 示例：

- 1. **显示目录的磁盘使用情况：**

```
du -h /path/to/directory
```

- 2. **显示文件或目录的总磁盘使用量：**

```
du -sh /path/to/file_or_directory
```

- 3. **显示多个目录及其子目录的总磁盘使用量：**

```
du -h --max-depth=1 /path/to/directory1 /path/to/directory2
```

- 4. **显示当前目录及其子目录的总磁盘使用量：**

```
du -h --max-depth=1
```

- 5. 显示所有文件和目录的总磁盘使用量，并在最后显示总计：

```
du -h -c /path/to/directory1 /path/to/directory2
```

## 19. `tar`：创建或提取 tar 归档。

Linux 中的 `tar` 命令用于创建和操作归档文件。它是 "tape archive"（磁带归档）的缩写，常用于将多个文件和目录打包到单个归档文件中。`tar` 命令对于压缩和备份数据非常有用。

### 示例：

- 1. **创建 Tar 归档：**

```
tar -cvf archive.tar file1.txt file2.txt directory/
```

此命令创建一个名为 `archive.tar` 的 tar 归档，其中包含 `file1.txt`、`file2.txt` 以及 `directory/` 的内容。

- 2. **从 Tar 归档中提取文件：**

```
tar -xvf archive.tar
```

此命令提取 `archive.tar` 文件的内容。

- 3. **创建 Gzipped Tar 归档：**

```
tar -czvf archive.tar.gz directory/
```

使用 gzip 压缩创建一个名为 `archive.tar.gz` 的压缩 tar 归档，包含 `directory/`。

- 4. **从 Gzipped Tar 归档中提取文件：**

```
tar -xzvf archive.tar.gz
```

此命令提取压缩文件 `archive.tar.gz` 的内容。

- 5. **列出 Tar 归档的内容：**

```
tar -tvf archive.tar
```

此命令列出 `archive.tar` 文件的内容，而不将其提取出来。

## 20. `wget`：从互联网下载文件。

`wget` 是一个用于从互联网下载文件的命令行实用工具。它支持通过 HTTP、HTTPS 和 FTP 协议进行下载。它是一个功能强大的工具，具有各种选项和功能，用于从 Web 服务器检索内容。

### 示例：

- 1. **基本用法**：

```
wget https://example.com/file.zip
```

此命令从指定 URL 下载 file.zip。

- 2. **以不同名称保存**：

```
wget -O newfile.zip https://example.com/file.zip
```

从 URL 下载文件，但保存为 `newfile.zip`。

- 3. **在后台下载**：

```
wget -b https://example.com/largefile.zip
```

在后台下载文件，允许你继续使用该终端。

- 4. **递归下载**：

```
wget -r -np https://example.com/directory/
```

递归下载指定目录中的所有文件，但不访问父目录（`-np`）。

- 5. **限制下载速度**：

```
wget --limit-rate=200k https://example.com/largefile.zip
```

将下载速度限制为每秒 200 千字节。

- 6. **恢复中断的下载**：

```
wget -c https://example.com/largefile.zip
```

如果下载中断，使用 `-c` 恢复并完成下载。

## 21. `ssh`：安全连接到远程服务器。

`ssh` 命令代表 "Secure Shell"（安全外壳），是一种广泛用于通过网络安全连接到远程服务器或设备的协议。它在两个系统之间提供安全的加密通信，允许用户访问和管理远程系统，仿佛它们是本地系统一样。`ssh` 命令常用于类 Unix 操作系统，包括 Linux。

### 示例：

- 1. **基本 SSH 连接：**

```
ssh username@remote-host
```

此命令使用指定的用户名建立到远程主机的 SSH 连接。

- 2. **指定端口：**

```
ssh -p 2222 username@remote-host
```

使用端口 2222 连接到远程主机。默认的 SSH 端口是 22。

- 3. **执行命令：**

```
ssh username@remote-host ls -l /path/to/directory
```

连接到远程主机并执行 `ls -l /path/to/directory` 命令，显示指定目录中文件的详细列表。

- 4. **身份文件（私钥）：**

```
ssh -i /path/to/private-key username@remote-host
```

指定用于身份验证的私钥文件路径。当使用基于密钥的认证而不是密码时很有用。

- 5. **隧道（端口转发）：**

```
ssh -L 8080:localhost:80 username@remote-host
```

设置本地端口转发，将本地机器端口 8080 的流量重定向到远程主机的端口 80。

- 6. **X11 转发：**

```
ssh -X username@remote-host
```

启用 X11 转发，允许远程服务器在本地机器上显示图形应用程序。

## 22. `scp`：在本地和远程机器之间安全地复制文件。

`scp` 代表 Secure Copy Protocol（安全复制协议），它是一种命令行工具，用于在 Linux 和类 Unix 操作系统中在主机之间安全地复制文件和目录。它使用 SSH（Secure Shell）进行数据传输，并提供加密和身份验证。

### 示例：

- 1. **将文件从本地复制到远程主机：**



```
scp file.txt username@remote_server_ip/path/to/destination/
```

将 `file.txt` 替换为你想要复制的文件名，将 `username` 替换为远程服务器上的用户名，将 `remote_server_ip` 替换为远程服务器的 IP 地址，将 `/path/to/destination/` 替换为远程服务器上的目标路径。

- 2. 将文件从远程主机复制到本地：

```
scp username@remote_server_ip/path/to/file.txt /local/path/
```

此命令将 `file.txt` 从远程服务器复制到本地机器。请根据需要调整路径和用户名。

- 3. 将整个目录从本地复制到远程主机：

```
scp -r my_directory username@remote_server_ip:/path/to/destination/
```

`-r` 选项用于递归复制目录。

- 4. 使用特定端口从远程复制到本地：

```
scp -P 2222 username@remote_server_ip:/path/to/file.txt /local/path/
```

这里，`-P` 选项指定端口号（本例中为 `2222`）。

- 5. 压缩复制：

```
scp -C file.txt username@remote_server_ip:/path/to/destination/
```

`-C` 选项在传输期间启用压缩。

## 23. find：在目录层次结构中搜索文件。

Linux 中的 `find` 命令是一个强大且多功能的工具，用于根据各种条件在目录层次结构中搜索文件和目录。

### 示例：

- 1. 基本用法：

```
find /path/to/search -name "filename.txt"
```

此命令在指定路径中搜索名为 `"filename.txt"` 的文件。

- 2. 不区分大小写的搜索：

```
find /path/to/search -iname "file*.txt"
```

`-iname` 选项执行不区分大小写的搜索，查找匹配指定模式的文件。

- 3. 按文件类型搜索：

```
find /path/to/search -type f
```

此命令在指定路径中查找常规文件。

- 4. 按目录类型搜索：

```
find /path/to/search -type d
```

此命令在指定路径中查找目录。

- 5. 搜索最近 N 天内修改过的文件：

```
find /path/to/search -mtime -7
```

此命令查找最近 7 天内修改过的文件。

- 6. 搜索大于特定大小的文件：

```
find /path/to/search -size +1M
```

此命令查找大于 1 兆字节的文件。

- 7. 对找到的文件执行命令：

```
find /path/to/search -name "*.log" -exec rm {} \;
```

此命令查找所有扩展名为 `".log"` 的文件，并使用 `rm` 命令删除它们。

- 8. 使用逻辑运算符组合多个条件：

```
find /path/to/search -name "*.txt" -o -name "*.md"
```

该命令查找扩展名为 `".txt"` 或 `".md"` 的文件。

### 9. 搜索文件并排除特定路径：

```
find /path/to/search -name "*.jpg" -not -path "/path/to/search/exclude/*"
```

该命令查找 JPEG 文件，但排除了指定排除路径中的文件。

### 10. 搜索空文件：

```
find /path/to/search -type f -empty
```

该命令查找指定路径中的空文件。

## 24. nproc：打印可用的处理单元数量。

Linux 中的 `nproc` 命令是一个简单但功能强大的实用程序，用于提供系统中可用处理单元的信息。它基本上显示系统拥有的处理单元（或核心）数量。

### 示例：

- 1. 基本用法：

```
nproc
```

这将输出系统中可用的处理单元总数。

- 2. 显示核心数量：

```
echo "Number of cores: $(nproc)"
```

该命令使用命令替换（`$(nproc)`）将 `nproc` 的结果嵌入输出消息中。

- 3. 指定最大处理器数量：

```
nproc --all
```

此选项 `--all` 或 `-a` 显示可用的最大处理器数量，包括在线和离线处理器。

- 4. 显示物理核心：

```
nproc --sockets
```

此选项 `--sockets` 或 `-s` 显示物理插槽（处理器）的数量。

- 5. 显示每核心线程数：

```
nproc --threads
```

此选项 `--threads` 或 `-T` 显示每个核心的线程数。

- 6. 显示在线处理器：

```
nproc -online
```

此选项 `-online` 或 `-o` 显示在线处理器（活动处理器）的数量。

- 7. 检查特定数量的核心是否可用：

```
if [ "$(nproc)" -ge 4 ]; then
    echo "There are at least 4 cores available."
else
    echo "There are fewer than 4 cores available."
fi
```

此示例演示了在脚本中使用 `nproc` 来检查可用核心数量的方法。

- 8. 与其他命令结合使用：

```
echo "This system has $(nproc) cores and $(free -m | awk '/^Mem:/ {print $2}') megabytes of RAM."
```

此示例将 `nproc` 与 `free` 命令结合，以显示核心数量和总 RAM 大小。

- 9. 显示帮助信息：

```
nproc --help
```

该命令提供关于 `nproc` 命令可用选项和用法的说明。

## 25. awk：用于模式扫描和处理的文本处理工具。

`AWK` 是一种强大的编程语言和命令行实用工具，用于 Unix 和 Linux 环境中的文本处理。它特别适用于处理和文本文件分析、提取特定信息以及执行数据操作任务。

### 示例：

- 1. 打印特定列：

要打印文件中的特定列，请使用 `print` 语句。

```
#### Print the first and third columns of a file
awk '{print $1, $3}' filename
```

- 2. 过滤数据：

`AWK` 可用于基于条件过滤数据。

```
#### Print lines where the second column is greater than 50
awk '$2 > 50 {print}' filename
```

- 3. 计算：

`AWK` 能够执行数据计算。

```
#### Calculate and print the average of the third column
awk '{sum += $3} END {print "Average:", sum/NR}' filename
```

- 4. 模式匹配：

使用模式来匹配特定行。

```
#### Print lines containing the word "error"
awk '/error/ {print}' filename
```

- 5. 条件语句：

`AWK` 支持条件语句。

```
#### Print "Pass" or "Fail" based on the value in the second column
awk '{if ($2 >= 50) print "Pass"; else print "Fail"}' filename
```

- 6. 字段分隔符：

使用 `-F` 选项指定自定义字段分隔符。

```
#### Print the second field using ":" as the separator
awk -F: '{print $2}' filename
```

- 7. 内置变量：

`AWK` 具有多个内置变量。例如，`NF` 表示一行中的字段数。

```
#### Print lines with more than 3 fields
awk 'NF > 3 {print}' filename
```

- 8. 从命令输出读取：

`AWK` 可以从其他命令的输出中读取。



### List files and their sizes in the current directory
```
ls -l | awk '{print $9, $5}'
```

9. 格式化输出：

使用 `printf` 以获得更好的格式化。

### Print the first and second columns with specific formatting
```
awk '{printf "Name: %-10s Score: %d\n", $1, $2}' filename
```

10. 多条命令：

使用花括号执行多条命令。

### Print the first and second columns, then calculate and print their sum
```
awk '{print $1, $2; sum += $2} END {print "Sum:", sum}' filename
```

## 26. sed：用于过滤和转换文本的流编辑器。

`sed` 是流编辑器（stream editor）的缩写，是 Linux 中功能强大的文本处理工具。它用于对输入流（文件或管道输入）执行基本文本转换并生成输出流。`sed` 常用于脚本和单行命令中的替换、删除、插入及其他文本操作。

### 示例：

1. 替换文件中的文本：

```
sed 's/apple/orange/' fruits.txt
```

该命令将文件 `fruits.txt` 中第一次出现的 "apple" 替换为 "orange"，并将结果打印到标准输出。

2. 全局替换所有出现项：

```
sed 's/apple/orange/g' fruits.txt
```

该命令将文件 `fruits.txt` 中所有出现的 "apple" 替换为 "orange"。

3. 删除包含特定模式的行：

```
sed '/pattern/d' file.txt
```

该命令从文件 `file.txt` 中删除所有包含指定模式的行。

4. 打印特定行：

```
sed -n '1,5p' file.txt
```

该命令打印文件 `file.txt` 中的第 1 到 5 行，而不自动打印其他行。

5. 就地编辑（更新文件）：

```
sed -i 's/old/new/' file.txt
```

该命令将文件 `file.txt` 中第一次出现的 "old" 替换为 "new"，并就地更新文件。

## 27. tree：显示目录树结构。

Linux 中的 `tree` 命令用于以树状格式显示目录和子目录的层次结构。它是可视化表示文件系统结构的有用工具。

### 示例：

1. 显示当前目录的树结构：

```
tree
```

2. 显示带有完整路径的树结构：

```
tree -f
```

3. 在树中显示隐藏文件和目录：

```
tree -a
```

4. 将树的深度限制为 2 层：

```
tree -L 2
```

5. 在树中仅显示目录：

```
tree -d
```

6. 从树中排除特定目录：

```
tree --prune dir_to_exclude
```

7. 反转匹配以显示不匹配模式的文件：

```
tree -i -P "*.txt"
```

## 28. gzip：压缩或解压缩文件。

Linux 中的 `gzip` 命令用于文件压缩和解压缩。它以所使用的 GNU zip 压缩算法命名。

### 示例：

1. 压缩文件：

```
gzip example.txt
```

这将压缩文件 `example.txt` 并创建名为 `example.txt.gz` 的压缩文件。

2. 解压缩文件：

```
gzip -d example.txt.gz
```

解压缩文件 `example.txt.gz` 并将其恢复为 `example.txt`。

3. 保留原始文件：

```
gzip -k example.txt
```

压缩 `example.txt` 并保留原始文件，结果是 `example.txt` 和 `example.txt.gz` 同时存在。

4. 递归压缩：

```
gzip -r my_directory
```

递归压缩目录 `my_directory` 中的所有文件。

5. 测试压缩文件：

```
gzip -t example.txt.gz
```

测试压缩文件 `example.txt.gz` 的完整性。

6. 详细输出：

```
gzip -v example.txt
```

在压缩 `example.txt` 时显示压缩比和文件大小。

## 29. gunzip：解压缩 gzip 文件。

### 示例：

- 解压文件：

```
gunzip example.txt.gz
```

- 解压多个文件：

```
gunzip file1.gz file2.gz
```

- 解压并保留原文件：

```
gunzip -k example.txt.gz
```

- 解压并列出压缩归档的内容：

```
gunzip -l example.txt.gz
```

- 解压并将输出写入标准输出：

```
gunzip -c example.txt.gz > output.txt
```

## 30. ping：测试 IP 网络上主机的可达性。

`ping` 命令是一个网络实用工具，用于测试 Internet Protocol (IP) 网络上主机的可达性。它还测量从源主机发送到目标计算机的消息的往返时间。名称“ping”源自潜艇用来探测水中其他物体的声呐声音。

### 示例：

- 简单 Ping：

```
ping google.com
```

这将向 google.com 发送一系列 ICMP Echo 请求，您会看到每个数据包的往返时间。

- 设置数据包数量：

```
ping -c 4 google.com
```

这仅向 google.com 发送 4 个数据包，然后停止。

- 设置数据包大小：

```
ping -s 100 google.com
```

这向 google.com 发送大小为 100 字节的数据包。

- 设置数据包之间的间隔：

```
ping -i 2 google.com
```

这设置连续数据包之间为 2 秒的间隔。

- 设置超时：

```
ping -t 5 google.com
```

这设置 5 秒的超时时间。如果在此时间内未收到响应，ping 命令将停止。

- 静默模式：

```
ping -q google.com
```

这以静默模式运行 ping 命令，仅在最后显示摘要。

- 详细模式：

```
ping -v google.com
```

这以详细模式运行 ping 命令，提供关于每个数据包的更详细信息。

- IPv6 Ping：

```
ping6 ipv6.google.com
```

这执行使用 IPv6 的 ping。`ping6` 命令用于 IPv6 地址。

## 31. traceroute：显示数据包到达网络主机所经过的路由。

Traceroute 是一个在 Linux 和其他操作系统中使用的命令行工具，用于追踪数据包从您的计算机到目标 IP 地址或域名所经过的路由。它有助于识别网络路径并测量数据包在互联网上的传输延迟。

### 示例：

- 基本用法：

```
traceroute example.com
```

此命令追踪到 `example.com` 的 IP 地址的路由，显示沿途的路由器（跃点）列表。

- 指定最大 TTL：

```
traceroute -m 15 example.com
```

将最大 TTL 设置为 15，限制追踪的跃点数。

- 不解析主机名：

```
traceroute -n example.com
```

显示 IP 地址而不是将它们解析为主机名，这可以加快处理速度。

- 设置查询数据包：

```
traceroute -q 5 example.com
```

每个跃点发送 5 个查询数据包，而不是默认的 3 个。

- 使用 UDP 数据包：

```
traceroute -U example.com
```

使用 UDP 数据包，而不是默认的 ICMP Echo 请求数据包。

- 指定等待时间：

```
traceroute -w 2 example.com
```

设置等待响应的时间（秒数），然后再发送下一个数据包。

- 追踪到特定端口：



指定目标端口（例如，HTTP 的 80 端口）。

- **IPv6 Traceroute：**

```
traceroute -p 80 example.com
```

使用 IPv6 地址执行 traceroute。

- **将输出保存到文件：**

```
traceroute -6 ipv6.example.com
```

将输出重定向到文件以便后续分析。

- **连续追踪：**

```
traceroute example.com > trace_output.txt
```

连续追踪路由，每个跃点发送单个数据包，等待时间最短。

## 32. ifconfig 或 ip：配置网络接口。

### `ifconfig` 命令：

`ifconfig` 命令用于配置 Linux 系统上的网络接口。它允许您查看和配置网络接口的 IP 地址、子网掩码、广播地址和其他参数。然而，在许多现代 Linux 发行版中，`ifconfig` 已被弃用，转而使用更强大的 `ip` 命令。

#### 示例：

1. **查看网络接口：**

```
ifconfig
```

此命令显示系统中所有网络接口的信息。

2. **查看特定接口的信息：**

```
ifconfig eth0
```

将 `eth0` 替换为您的网络接口名称。此命令显示指定接口的详细信息。

3. **分配 IP 地址：**

```
sudo ifconfig eth0 192.168.1.2
```

此命令将 IP 地址 192.168.1.2 分配给 `eth0` 接口。

4. **设置子网掩码：**

```
sudo ifconfig eth0 netmask 255.255.255.0
```

为 `eth0` 接口设置子网掩码。

5. **启用或禁用接口：**

```
sudo ifconfig eth0 up
sudo ifconfig eth0 down
```

这些命令分别启用或禁用 `eth0` 接口。

### `ip` 命令：

`ip` 命令是一个更强大、更灵活的网络接口配置和管理工具。它提供了 `ifconfig` 之外的广泛功能。

#### 示例：

1. **查看网络接口：**

```
ip link show
```

此命令显示系统中所有网络接口的信息。

2. **查看 IP 地址：**

```
ip address show
```

显示分配给所有接口的 IP 地址的详细信息。

3. **分配 IP 地址：**

```
sudo ip address add 192.168.1.2/24 dev eth0
```

将 IP 地址 192.168.1.2 和子网掩码 255.255.255.0 分配给 `eth0` 接口。

4. **设置子网掩码：**

```
sudo ip address add 192.168.1.2/24 dev eth0
```

这也为 `eth0` 接口设置了子网掩码。

5. **启用或禁用接口：**

```
sudo ip link set eth0 up
sudo ip link set eth0 down
```

这些命令分别启用或禁用 `eth0` 接口。

6. **显示路由表：**

```
ip route show
```

显示内核路由表。

## 33. netstat：显示网络连接、路由表、接口统计、伪装连接和多播成员关系。

Linux 中的 `netstat` 命令是一个强大的网络实用工具，用于显示有关网络连接、路由表、接口统计、伪装连接等的信息。它提供了多种选项，帮助您分析和排除网络相关问题。

### 示例：

- **使用数字地址显示所有监听和非监听套接字：**

```
netstat -an
```

- **显示所有协议的统计信息：**

```
netstat -s
```

- **显示所有 TCP 连接及使用它们的过程：**

```
netstat -atp
```

- **显示路由表：**

```
netstat -r
```

- **仅显示监听中的 TCP 套接字：**

```
netstat -tl
```

- **显示所有接口的信息：**

```
netstat -ie
```

- **显示内核接口表：**

```
netstat -i
```

## 34. ncdu：NCurses 磁盘使用情况 - 一个磁盘使用分析器。

`ncdu` (NCurses Disk Usage) 是 Linux 中用于分析和磁盘空间使用情况的命令行实用程序。它以简单、交互的方式查看和浏览文件系统，并以层级格式显示目录和子目录的大小。

### 示例：

1. **分析当前目录的磁盘使用情况：**

```
ncdu
```

2. **分析特定目录的磁盘使用情况：**

```
ncdu /path/to/directory
```

3. **从分析中排除某些文件或目录：**

```
ncdu -x "*.log" /path/to/directory
```

4. **以只读模式运行以防止意外删除：**

```
ncdu -r /path/to/directory
```

5. **指定包含要分析的目录列表的文件：**

## 35. ltrace：库调用跟踪器。

`ltrace` 是 Linux 中的一个命令行实用工具，用于拦截并显示程序所执行的动态库调用。它可以让你查看进程调用的库函数和系统调用，从而提供程序运行期间行为的重要见解。

**示例：**

- 1. 基本用法：

```bash
ltrace ls
```

此命令跟踪由 `ls` 命令执行的动态库调用。

- 2. 过滤输出：

```bash
ltrace -e fopen ls
```

`-e` 选项允许你过滤输出，仅显示你感兴趣的函数。在此示例中，它仅跟踪由 `ls` 命令对 `fopen` 函数的调用。

- 3. 将输出重定向到文件：

```bash
ltrace -o output.txt ls
```

此命令将 `ltrace` 的输出重定向到名为 `output.txt` 的文件，而不是打印到终端。

- 4. 通过 PID 跟踪特定进程：

```bash
ltrace -p <pid>
```

用你想跟踪的正在运行的进程 ID 替换 `<pid>`。这对于将 `ltrace` 附加到已运行的进程非常有用。

- 5. 显示系统调用：

```bash
ltrace -S ls
```

`-S` 选项除了库调用外，还包含系统调用的显示。

- 6. 在 64 位系统上跟踪 32 位进程：

```bash
ltrace -a 32 -c ls
```

使用 `-a` 选项在 64 位系统上跟踪进程时指定架构（在此情况下为 32 位）。

- 7. 按库过滤：

```bash
ltrace -l libm.so ls
```

此命令仅跟踪由 `ls` 命令对 `libm` 库中函数的调用。

- 8. 显示时间和计数：

```bash
ltrace -c ls
```

`-c` 选项显示每个函数的调用次数和所花时间摘要。

- 9. 跟踪带有命令行参数的程序：

```bash
ltrace gzip file.txt
```

你可以连同其命令行参数一起跟踪程序。

- 10. 跟踪多个命令：

```bash
ltrace -o output.txt sh -c "ls; echo Hello"
```

通过使用 `c` 选项并将它们括在引号中，在 shell 中跟踪多个命令。

- 11. 显示函数参数：

```bash
ltrace -f -F ls
```

`f` 选项跟踪 fork（分叉），而 `F` 选项显示函数参数。

## 36. useradd：创建新的用户账户。

Linux 中的 `useradd` 命令用于在系统上创建新的用户账户。它是一个基本命令，允许你在创建新用户时指定各种参数。

**示例：**

- 1. 创建新用户：

```bash
sudo useradd mohan
```

此命令使用默认设置创建名为 "mohan" 的新用户账户。用户的家目录将是 `/home/mohan`。

- 2. 创建具有特定家目录的用户：



## useradd：创建用户账户

```bash
sudo useradd -m -d /home/customuser customuser
```

`-m`选项确保创建用户家目录，而`-d`指定家目录路径。

### 3. 指定用户的登录 shell：

```bash
sudo useradd -s /bin/bash bashuser
```

此命令创建名为"bashuser"的用户，并将登录 shell 设置为`/bin/bash`。

### 4. 设置用户密码：

```bash
sudo useradd -m -p $(openssl passwd -1 mypassword) secureuser
```

`-p`选项允许你设置用户的加密密码。在此示例中，`openssl passwd -1`生成字符串"mypassword"的加密密码。

### 5. 创建具有特定用户 ID (UID) 和组 ID (GID) 的用户：

```bash
sudo useradd -u 1001 -g 1001 customuser
```

`-u`选项设置用户 ID，而`-g`选项设置用户的主组 ID。

### 6. 创建系统用户：

```bash
sudo useradd -r sysuser
```

`-r`选项用于创建系统用户，通常用于运行系统服务。

### 7. 设置用户账户的过期日期：

```bash
sudo useradd -e 2023-12-31 tempuser
```

`-e`选项设置用户账户的过期日期。在此示例中，"tempuser"的账户将在2023年12月31日过期。

### 8. 显示 useradd 命令帮助：

```bash
useradd --help
```

此命令提供`useradd`命令选项和用法的摘要。

## 37. userdel：删除用户账户。

Linux 中的`userdel`命令用于从系统中删除用户账户及相关文件。它是一个强大的命令，需要管理权限才能执行。当用户账户被删除时，通常相关的家目录和邮件池会被移除，但其他位置的文件不会被触及。

**示例：**

### 1. 基本用法：

```bash
sudo userdel mohan
```

这将删除名为"mohan"的用户账户。

### 2. 删除用户及家目录：

```bash
sudo userdel -r jane
```

这将删除用户账户"jane"及其家目录和内容。

### 3. 强制删除且无需提示：

```bash
sudo userdel -f alice
```

### 4. 指定不同的家目录：

```bash
sudo userdel -m -r bob
```

这将删除用户账户"bob"并将家目录移动到备份位置。

### 5. 将用户从组中移除：

```bash
sudo userdel -G developers,sudo charlie
```

此命令将删除用户账户"charlie"并使其从"developers"和"sudo"组中移除。

### 6. 显示帮助信息：

```bash
userdel --help
```

这将显示选项列表及其解释。

## 38. passwd：更改用户密码。

Linux 中的`passwd`命令用于更改用户密码。它允许用户更新自己的密码，或者如果由超级用户执行，则更改系统中任何用户的密码。

**示例：**

### 1. 更改你自己的密码：

```bash
passwd
```

系统会提示你输入当前密码，然后输入新密码。

### 2. 更改其他用户的密码（作为 root）：

```bash
sudo passwd username
```

用实际的用户名替换"username"。此命令会提示你为指定用户输入新密码。

### 3. 锁定用户账户：

```bash
sudo passwd -l username
```

这将锁定指定用户账户的密码，阻止其登录。

### 4. 解锁用户账户：

```bash
sudo passwd -u username
```

这将解锁指定用户账户的密码，允许其再次登录。

### 5. 删除用户密码：

```bash
sudo passwd -d username
```

这将删除指定用户账户的密码，实际上使通过密码登录变得不可能。

### 6. 使用户密码过期：

```bash
sudo passwd -e username
```

这将强制用户在下次登录时更改密码。

## 39. mpstat：报告处理器相关统计信息。

Linux 中的`mpstat`命令用于显示多处理器系统中每个处理器利用率的详细信息。它提供单个处理器以及所有处理器平均值的统计信息。

**示例：**

### 1. 每 2 秒显示所有处理器的 CPU 利用率统计信息，共 3 次报告：

```bash
mpstat -u 2 3
```

### 2. 显示单个处理器的统计信息：

```bash
mpstat -P ALL
```

### 3. 显示中断统计信息：

```bash
mpstat -I SUM
```

### 4. 显示所有可用信息：

```bash
mpstat -A
```

## 40. sar：收集、报告或保存系统活动信息。

Linux 中的`sar`命令用于收集、报告和保存系统活动信息。它提供有关系统性能的广泛统计信息，包括 CPU 利用率、内存使用、磁盘活动、网络活动等。`sar`收集的数据对性能分析和故障排除非常有用。

**示例：**

### 1. 以 5 秒间隔显示 CPU 利用率统计信息，共 3 次：

```bash
sar -u 5 3
```

### 2. 以 10 秒间隔显示内存利用率统计信息，共 5 次：

```bash
sar -r 10 5
```

### 3. 以 1 分钟间隔无限期显示 I/O 和传输速率统计信息：

### 4. 以 2 秒为间隔显示网络统计信息，共 4 次：

```bash
sar -n DEV 2 4
```

### 5. 以 30 秒为间隔显示所有可用的统计信息，共 10 次：

```bash
sar -A 30 10
```

## 41. echo：显示一条消息或向文件写入消息。

Linux 中的`echo`命令用于在标准输出（通常是终端）上显示一行文本或一串字符。它是一个简单且常用的命令，用于向屏幕打印信息、变量或消息。

**示例：**

### 1. 基本用法：

```bash
echo "Hello, World!"
```

### 2. 使用变量：

```bash
name="mohan"
echo "My name is $name"
```

### 3. 不换行：

```bash
echo -n "This is on the same line"
echo " but this is on the next line."
```

### 4. 转义字符：

```bash
echo -e "This is a line with a\tab."
```

## 42. history：显示命令历史记录。

Linux 命令历史是一个功能，允许用户查看和调取之前在终端中执行过的命令。它通过避免用户重新输入常用命令来帮助用户节省时间。命令历史存储在一个文件中，通常位于用户的家庭目录中，并由 Shell 管理。

**示例：**

### 1. 查看命令历史：

```bash
history
```

这将显示一个编号列表，最近执行的命令位于列表底部。

### 2. 执行以前的命令：

```bash
!5
```

这将执行历史记录中第 5 行的命令。

### 3. 清除命令历史：

```bash
history -c
```

这不会删除历史文件；它只是清除当前会话的历史记录。

## 43. iostat：报告 CPU 和 I/O 统计信息。

Linux 中的`iostat`命令用于报告设备、分区和 NFS（网络文件系统）的 CPU 和输入/输出（I/O）统计信息。它提供了系统性能的综合概述，帮助用户识别潜在的瓶颈并监控资源使用情况。

**示例：**

### 1. 显示 CPU 使用率统计信息：

```bash
iostat -c
```

### 2. 以 2 秒为间隔显示设备使用率统计信息，共 5 次报告：

```bash
iostat -d 2 5
```

### 3. 以每秒兆字节为单位显示设备和分区的扩展统计信息：

```bash
iostat -x -m
```

### 4. 带时间戳显示 NFS 统计信息：

```bash
iostat -N -t
```

## 44. fuser：识别正在使用文件或套接字的进程。



Linux 中的 `fuser` 命令用于识别正在使用特定文件、文件系统或套接字的进程。它显示拥有打开文件的进程的进程 ID（PID），从而允许您确定哪些进程正在访问特定资源。

### 示例：

- 1. **查找正在使用特定文件的进程：**

```
fuser myfile.txt
```

- 2. **查找正在使用已挂载文件系统的进程：**

```
fuser -m /mnt/myfilesystem
```

- 3. **终止正在使用文件的进程：**

```
fuser -k myfile.txt
```

- 4. **查找正在使用网络套接字（例如端口 8080）的进程：**

```
fuser -n tcp 8080
```

- 5. **显示更详细的信息：**

```
fuser -v myfile.txt
```

## 45. `ln`：在文件之间创建链接。

Linux 中的 `ln` 命令用于在文件或目录之间创建链接。它有两种主要形式：创建硬链接和符号链接（软链接）。

### 示例：

- 1. **创建硬链接：**

```
ln file1.txt hardlink.txt
```

这创建了一个名为 `hardlink.txt` 的硬链接，指向与 `file1.txt` 相同的 inode。

- 2. **创建符号链接：**

```
ln -s /path/to/file1.txt symlink.txt
```

这创建了一个名为 `symlink.txt` 的符号链接，指向 `file1.txt`。

- 3. **使用相对路径创建符号链接：**

```
ln -s -r /path/to/file1.txt relative_symlink.txt
```

这创建了一个名为 `relative_symlink.txt` 的符号链接，使用指向 `file1.txt` 的相对路径。

- 4. **覆盖前提示：**

```
ln -i file1.txt hardlink.txt
```

如果 `hardlink.txt` 已经存在，该命令将在覆盖之前进行提示。

- 5. **详细输出：**

```
ln -v file1.txt hardlink.txt
```

为创建的每个硬链接打印一条消息。

- 6. **强制创建符号链接：**

```
ln -sf /path/to/new_target symlink.txt
```

这强制创建符号链接，如果 `symlink.txt` 已存在则将其覆盖。

## 46. `ldconfig`：配置动态链接器运行时绑定。

Linux 中的 `ldconfig` 命令用于配置动态链接器运行时绑定。它更新共享库缓存，该缓存是共享库的系统级索引。此缓存用于动态链接器在运行可执行文件时快速定位和加载共享库。

### 示例：

- 1. **更新共享库缓存：**

```
sudo ldconfig
```

- 2. **显示将执行的操作而不实际更新缓存：**

```
ldconfig -n
```

- 3. **清除整个动态链接器缓存：**

```
sudo ldconfig -X
```

- 4. **带有详细输出的更新缓存：**

```
sudo ldconfig -v
```

- 5. **打印配置变量：**

```
ldconfig -C
```

## 47. `curl`：向服务器传输数据或从服务器接收数据。

`curl`（“Client for URLs”的缩写）是一个命令行工具，用于在 Unix 和 Linux 系统中通过 URL 传输数据。它支持多种协议，如 HTTP、HTTPS、FTP、FTPS、SCP、SFTP、LDAP 等。`curl` 非常灵活且通用，允许用户执行广泛的任务，包括下载文件、向 Web 服务发送请求等。

### 示例：

- 1. **简单的 GET 请求：**

```
curl https://www.example.com
```

- 2. **将输出保存到文件：**

```
curl -o output.html https://www.example.com
```

- 3. **带有数据的 HTTP POST 请求：**

```
curl -X POST -d "param1=value1&param2=value2" https://www.example.com/api
```

- 4. **设置自定义头部：**

```
curl -H "Authorization: Bearer <token>" https://api.example.com/data
```

- 5. **跟随重定向：**

```
curl -L https://www.example.com
```

## 48. `lsof`：列出打开的文件以及打开它们的进程。

Linux 中的 `lsof` 命令用于列出当前被进程打开的文件信息。它提供了关于系统中正在运行的进程所使用的文件、目录和网络套接字的详细信息。这对于系统管理员和用户排查与文件访问相关的问题、确定哪些进程正在使用特定文件或查看特定进程打开的网络连接极为有用。

### 示例：

- 1. **列出所有打开的文件：**

```
lsof
```

- 2. **列出特定进程（例如进程 ID 为 1234）的打开文件：**

```
lsof -p 1234
```

- 3. **列出特定用户（例如用户 'username'）的打开文件：**

```
lsof -u username
```

- 4. **列出特定命令（例如命令 'nginx'）的打开文件：**

```
lsof -c nginx
```

- 5. **列出的打开网络连接：**

```
lsof -i
```

- 6. **列出特定进程的打开文件并仅显示进程 ID：**

```
lsof -p 1234 -t
```

## 49. `iotop`：监控进程的 I/O 使用情况。

`iotop` 是 Linux 系统上的一个命令行实用程序，允许用户实时监视和显示进程的输入/输出（I/O）使用信息。它提供了系统中 I/O 活动的动态交互式视图，帮助用户识别正在从存储设备读取或向其写入数据的进程。

### 示例：

- 1. **以默认设置运行 `iotop`：**

```
iotop
```

这将显示 I/O 使用情况的实时交互式视图。

- 2. **以批处理模式运行 `iotop`，限制迭代次数，每次迭代之间延迟 2 秒：**

```
iotop -b -n 5 -d 2
```

这以批处理模式运行 `iotop`，捕获 5 次迭代的 I/O 统计信息，每次迭代之间延迟 2 秒。

- 3. **仅显示实际正在执行 I/O 的进程或线程：**

```
iotop -o
```

这将仅显示当前参与 I/O 操作的进程或线程。

## 50. `rsync`：在两个位置之间同步文件和目录。

`rsync` 是一个功能强大且通用的命令行工具，用于在类 Unix 操作系统上的两个位置之间同步文件和目录。它仅高效地传输源和目的地之间的差异，使其特别适合用于远程备份或镜像。

### 示例

#### 1. 基本同步

```
rsync -av /path/to/source/ /path/to/destination/
```

此命令将源目录的内容同步到目标目录，保留权限和其他属性。

#### 2. 远程同步

```
rsync -avz -e ssh user@remote:/path/to/source/ /path/to/destination/
```

通过 SSH 在本地计算机和远程计算机之间同步文件。将 `user` 替换为用户名，将 `remote` 替换为远程机器的 IP 或主机名。

#### 3. 排除文件

```
rsync -av --exclude="*.log" /path/to/source/ /path/to/destination/
```

同步源到目标，但排除扩展名为 `.log` 的文件。

#### 4. 试运行

```
rsync -av --dry-run /path/to/source/ /path/to/destination/
```

执行试运行以查看将做出哪些更改，而实际上不传输任何文件。

#### 5. 显示进度

```
rsync -avP /path/to/source/ /path/to/destination/
```

在传输过程中显示进度，指示完成百分比和传输速率。

## 51. `uname`：显示系统信息

Linux 中的 `uname` 命令用于显示系统信息，如系统名称、内核名称、网络节点主机名、内核版本、内核版号、机器硬件名称和处理器架构。

### 示例

- 1. 显示所有系统信息：

```
uname -a
```

- 2. 仅显示内核名称：

```
uname -s
```

- 3. 显示机器硬件名称：

```
uname -m
```

- 4. 显示内核版本：

```
uname -v
```

- 5. 显示操作系统：

```
uname -o
```

## 52. `uptime`：显示系统运行时长



Linux 中的 `uptime` 命令是一个简单但强大的工具，提供系统运行时长以及一些关键性能指标的信息。

### 示例

- 1. 仅显示运行时间信息：

```
uptime -p
```

此命令将以更易读格式仅显示运行时间信息。

- 2. 显示短输出：

```
uptime -s
```

此命令显示系统的启动时间。

- 3. 仅显示负载平均值：

```
uptime -q
```

此命令提供有关系统负载平均值的信息。

- 4. 自定义格式：

```
uptime -f
```

此命令以更机器可读的格式显示以下信息。

## 53. killall：按名称终止进程

Linux 中的 `killall` 命令用于终止或向所有具有指定名称的进程发送信号。它允许您根据进程名称而不是进程 ID `PID` 一次终止多个进程。

### 示例

- 1. 终止所有名为 "firefox" 的进程：

```
killall firefox
```

- 2. 使用 `SIGKILL` 信号强制终止所有名为 "myprocess" 的进程实例：

```
killall -s SIGKILL myprocess
```

- 3. 使用精确匹配选项，确保仅终止名称完全为 "myprocess" 的进程：

```
killall -e myprocess
```

- 4. 交互式终止所有名为 "myprocess" 的进程实例：

```
killall -i myprocess
```

## 54. htop：交互式进程查看器

`htop` 是一个用于类 Unix 操作系统的交互式进程查看器和系统监控器。它提供了一个用户友好的界面，以实时监控和管理系统资源。`htop` 允许用户查看有关运行进程、系统利用率和其他基本性能指标的详细信息。

### 示例

- 1. 启动 `htop`：

```
htop
```

- 2. 显示特定用户的进程（将 "`username`" 替换为实际用户名）：

```
htop -u username
```

- 3. 按 CPU 使用率排序进程：

```
htop -s PERCENT_CPU
```

- 4. 按 PID 终止进程（将 "`pid`" 替换为实际的进程 ID）：

```
htop -k pid
```

- 5. 显示 `htop` 帮助：

```
htop -h
```

## 55. chroot：使用不同的根目录运行命令

Linux 中的 `chroot` 命令用于更改特定进程的根目录，实质上创建一个受限环境，其中指定的命令或 shell 在此环境中运行。这在测试或修复系统时非常有用，而不会影响操作系统的其余部分。

### 示例

- 1. 更改根目录到新位置并在其中运行命令：

```
sudo chroot /path/to/new/root /bin/bash
```

此示例将根目录更改为 `/path/to/new/root` 并在此环境中启动一个新的 Bash shell。

- 2. 更改根目录并执行特定命令：

```
sudo chroot /path/to/new/root /bin/ls -l /home
```

此命令更改根目录并使用 `ls` 命令列出 `/home` 目录的内容。

## 56. who：显示当前登录用户的信息

Linux 中的 `who` 命令用于显示当前登录到系统的用户的信息。它提供详细信息，如用户名、终端、登录时间和来源 IP 地址。

### 示例

- 1. 显示所有已登录用户的列表：

```
who
```

- 2. 显示已登录用户的数量：

```
who -q
```

- 3. 显示当前终端所有者的信息：

```
who -m
```

- 4. 显示系统上次启动的时间：

```
who -b
```

## 57. w：显示谁已登录以及他们在做什么

Linux 中的 `w` 命令用于显示当前登录用户及其活动的信息。它提供了谁已登录、他们在做什么以及他们空闲了多长时间的快速概览。

### 示例

- 1. 显示当前已登录用户的信息：

```
w
```

此命令将显示当前已登录用户的信息，包括他们的用户名、终端、远程主机（如适用）、登录时间、空闲时间、`JCPU`（附加到终端的所有进程使用的总 CPU 时间）、`PCPU`（当前进程使用的 CPU 时间）以及正在执行的命令。

- 2. 显示带有标头的信息：

```
w -h
```

添加 `-h` 选项会抑制标头行，提供更紧凑的用户信息显示。

- 3. 显示特定用户的信息：

```
w username
```

将 "`username`" 替换为您想要显示其信息的实际用户名。这将仅显示指定用户的详细信息。

- 4. 显示特定终端的信息：

```
w -s
```

`-s` 选项按终端名称对输出进行排序，使您更容易看到谁正在使用特定终端。

- 5. 以短格式显示信息：

```
w -s -f
```

`-f` 选项提供更短的输出格式，仅显示用户、终端、登录时间、`JCPU` 和 `PCPU`。

- 6. 显示更多信息：

```
w -i
```

`-i` 选项提供有关系统空闲时间和自系统上次启动以来时间的额外信息。

- 7. 显示带有负载平均值的详细信息：

```
w -l
```

`-l` 选项将系统负载平均值添加到输出中。负载平均值代表特定时间段（1、5 和 15 分钟）内等待 CPU 时间的平均进程数。

- 8. 以特定格式显示信息：

```
w -o user,time,from
```

`-o` 选项允许您指定输出格式。在此示例中，格式包括用户、时间和 `from`（远程主机）。

## 58. sudo：以超级用户或其他用户身份执行命令

`sudo` 是 Unix 和类 Unix 操作系统中的一个命令行工具，允许受权限限制的用户根据安全策略以超级用户或其他用户身份执行命令。名称 "`sudo`" 是 "`superuser do`"（超级用户执行）的缩写。

### 示例

- 1. 安装软件：

```
sudo apt-get install firefox
```

此命令用于安装 Firefox 网页浏览器。`sudo` 命令用于在安装过程中提升权限。

- 2. 编辑系统文件：

```
sudo nano /etc/network/interfaces
```

这会打开 Nano 文本编辑器来编辑网络配置文件。编辑系统文件通常需要超级用户权限。

- 3. 更新软件包列表：

```
sudo apt-get update
```

这会更新本地软件包列表，这是在安装或升级软件之前所必需的步骤。

- 4. 升级已安装的软件包：

```
sudo apt-get upgrade
```

将所有已安装的软件包升级到其最新版本。

- 5. 移除软件：

```
sudo apt-get remove firefox
```

移除 Firefox 浏览器。与安装类似，移除软件通常需要提升的权限。

- 6. 重启服务：

```
sudo service apache2 restart
```

重启 Apache 网络服务器。管理系统服务通常需要超级用户权限。

- 7. 更改文件所有权：

```
sudo chown user:group filename
```

将文件的所有权更改为指定的用户和组。

- 8. 挂载文件系统：

```
sudo mount /dev/sdb1 /mnt
```

将指定设备的文件系统挂载到指定目录。

- 9. 查看系统日志：

```
sudo journalctl
```

使用 `journalctl` 命令显示系统日志。访问日志文件通常需要超级用户权限。

- 10. 将用户添加到组：

```
sudo usermod -aG groupname username
```

将用户添加到指定的组中。

- 11. 以另一个用户身份运行命令：

```
sudo -u username command
```

以指定用户的身份执行命令。

- 12. 使用图形编辑器编辑受保护的文件：

```
sudo gedit /etc/fstab
```

这将打开图形文本编辑器 Gedit 来编辑系统文件。

## 59. journalctl：查询并显示由 systemd 管理的日志消息

`journalctl` 是 Linux 中的一个命令行实用工具，用于查询和显示来自日志（journal）的消息。日志是由 `systemd` 系统和实用服务管理器实现的一种集中式日志记录系统。日志包含关于系统事件、来自各种服务的日志以及内核消息的信息。它是一个强大的工具，用于故障排除、监控和分析系统日志。

### 示例

- 1. 查看完整日志：

```
journalctl
```

此命令显示完整日志，从最早的条目到最近的条目。

- 2. 实时查看日志：

```
journalctl -f
```

`-f` 选项允许你实时跟踪日志，类似于针对传统日志文件的 `tail -f` 命令。

- 3. 查看日志的最后 n 行：

```
journalctl -n 50
```

使用 `-n` 选项指定要从日志末尾显示的行数。

- 4. 查看特定单元（服务）的日志：

```
journalctl -u apache2
```



此命令显示与 Apache 网络服务器相关的日志。将 `apache2` 替换为任何其他 systemd 单元的名称。

### 5. 查看当前启动期间的日志：

`journalctl -b`

仅显示当前启动期间的日志。

### 6. 查看特定启动序列的日志：

`journalctl -b -1`

将 `-1` 替换为启动序列号，以查看特定先前启动的日志。

### 7. 查看特定时间范围内的日志：

`journalctl --since "2023-01-01 00:00:00" --until "2023-01-02 23:59:59"`

使用 `--since` 和 `--until` 选项查看特定时间范围内的日志。

### 8. 显示带有完整详情的日志：

`journalctl -xe`

`-x` 选项显示每个日志条目的完整详情，包括消息和附加字段。

### 9. 按优先级过滤日志：

`journalctl -p err`

使用 `-p` 选项按优先级过滤日志。在此示例中，仅显示优先级为 "err"（错误）的日志。

### 10. 按进程 ID 过滤日志：

`journalctl _PID=1234`

将 `1234` 替换为你想要过滤日志的进程 ID。

### 11. 按消息内容过滤日志：

`journalctl | grep "search_term"`

你可以使用标准 Unix 工具（如 `grep`）根据日志消息的内容来过滤日志。

## 60. dd：复制和转换文件，创建磁盘映像。

`dd` 命令是 Linux 中一个多功能且强大的实用工具，用于复制和转换文件及数据流。"dd" 的名字代表 "data duplicator"（数据复制器），但由于其如果误用可能覆盖数据的潜力，常被称为 "disk destroyer"（磁盘破坏者）。`dd` 命令在块级别上运行，使其在创建磁盘映像、在设备之间复制数据以及转换数据格式等任务中非常高效。

### 示例：

#### 1. 创建磁盘的备份映像：

要创建整个磁盘的备份映像，你可以使用 `dd` 逐块复制其内容。将 `/dev/sdX` 替换为适当的磁盘标识符。

```
sudo dd if=/dev/sdX of=backup.img bs=4M
```

- `if=/dev/sdX`：指定输入文件（源磁盘）。
- `of=backup.img`：指定输出文件（目标磁盘映像）。
- `bs=4M`：将块大小设置为 4 兆字节以提高性能。

#### 2. 在设备之间复制数据：

将一个磁盘的内容复制到另一个磁盘。在此操作中要格外谨慎，以免覆盖重要数据。

```
sudo dd if=/dev/sdX of=/dev/sdY bs=4M
```

- `if=/dev/sdX`：指定输入文件（源磁盘）。
- `of=/dev/sdY`：指定输出文件（目标磁盘）。
- `bs=4M`：将块大小设置为 4 兆字节以提高性能。

#### 3. 从 ISO 创建可引导 USB 驱动器：

使用 `dd` 将 ISO 映像写入 USB 驱动器，创建可引导介质。

```
sudo dd if=ubuntu.iso of=/dev/sdX bs=4M
```

- `if=ubuntu.iso`：指定输入文件（源 ISO 映像）。
- `of=/dev/sdX`：指定输出文件（目标 USB 驱动器）。
- `bs=4M`：将块大小设置为 4 兆字节以提高性能。

#### 4. 生成随机数据：

`dd` 可用于生成随机数据以进行测试。

```
dd if=/dev/urandom of=random_data.bin bs=1M count=10
```

- `if=/dev/urandom`：指定输入文件（使用随机数据源）。
- `of=random_data.bin`：指定输出文件（随机数据的目标）。
- `bs=1M`：将块大小设置为 1 兆字节。
- `count=10`：指定要复制的块数（在此情况下，10 兆字节的随机数据）。

## 61. man：显示命令的手册。

Linux 中的 `man` 命令是一个强大的工具，为 Linux 操作系统中的各种命令和实用程序提供手册页或文档。它是命令行访问和查看文档的内置系统。"man" 的名字代表 "manual"（手册）。

### 示例：

#### 1. 查看命令的手册页：

```
man ls
```

此命令显示 `ls` 命令的手册页，该命令用于列出文件和目录。

#### 2. 在手册页中搜索特定关键词：

```
man -k keyword
```

例如：

```
man -k copy
```

此命令在手册页中搜索关键词 "copy"，并显示与该关键词相关的命令列表。

#### 3. 查看手册页的特定部分：

```
man 5 passwd
```

此命令显示 `passwd` 命令的手册页，但专门在第 5 部分，该部分通常包含文件格式信息。

#### 4. 打开库函数的手册页：

```
man 3 printf
```

此命令打开第 3 部分中 `printf` 函数的手册页，该部分包含库调用和函数。

#### 5. 不使用 `man` 命令直接打开手册页：

```
man -l filename
```

此命令直接打开指定文件的手册页。

#### 6. 使用特定选项查看命令的手册页：

```
man ls | col -b
```

此命令将 `ls` 的 `man` 命令输出通过 `col` 命令进行管道处理，以去除退格符，从而让你更清晰地查看。

#### 7. 获取 `man` 本身的帮助：

```
man man
```

此命令显示 `man` 命令的手册页，提供如何使用 `man` 本身的信息。

## 62. tput：设置终端相关功能。

Linux 中的 `tput` 命令是一个强大的实用工具，它与终端交互，允许你操作各种终端功能，例如颜色、光标移动和文本格式化。它在命令行中创建动态且视觉上吸引人的脚本时特别有用。

### 示例：

#### 1. 更改文本颜色：

#### 2. 更改背景颜色

```text
tput setab 4  # Set background color to blue
echo "This has a blue background"
tput sgr0     # Reset text attributes to default
```

#### 3. 文本格式化

```text
tput bold     # Set bold text
echo "This is bold text"
tput sgr0     # Reset text attributes to default
```

#### 4. 移动光标

```text
tput cup 5 10 # Move the cursor to row 5, column 10
echo "Hello, world!"
```

#### 5. 清屏

```text
tput clear # Clear the entire terminal screen
```

#### 6. 获取终端尺寸

```text
rows=$(tput lines)    # Get the number of rows in the terminal
cols=$(tput cols)     # Get the number of columns in the terminal
echo "Terminal size: $rows rows x $cols columns"
```

#### 7. 保存和恢复光标位置

```text
tput sc # Save current cursor position
#### Do some work that moves the cursor
tput rc # Restore cursor to the saved position
```

#### 8. 检查终端功能

```text
tput colors # Print the number of supported colors
tput bel # Emit a bell character (useful for notifications)
```

#### 9. 文本样式

```text
tput rev  # Reverse video (swap background and foreground colors)
echo "This has reversed video"
tput sgr0  # Reset text attributes to default
```

#### 10. 下划线文本

```text
tput smul  # Start underlining text
echo "This is underlined"
tput rmul  # Stop underlining text
```

## 63. nmap：网络探索工具和安全扫描器

`nmap`（Network Mapper，网络映射器）是一款功能强大且多用途的开源工具，用于网络发现和安全审计。它常用于发现计算机网络中的主机和服务，并创建网络结构的地图。`nmap` 通过向目标主机发送数据包并分析响应来工作。

### 示例



# 1. 基本扫描

```text
nmap target_ip
```

该命令对指定的目标 IP 地址执行基本扫描。它显示开放端口及其关联的服务。

# 2. 扫描 IP 地址范围

```text
nmap 192.168.1.1-50
```

扫描从 `192.168.1.1` 到 `192.168.1.50` 的 IP 地址范围。

# 3. 扫描整个子网

```text
nmap 192.168.1.0/24
```

扫描 `192.168.1.0/24` 子网中的所有 IP 地址。

# 4. 扫描多个主机

```text
nmap host1 host2 host3
```

扫描命令行中指定的多个主机。

# 5. 激进扫描

```text
nmap -A target_ip
```

执行激进扫描，包括操作系统检测、版本检测、脚本扫描和路由跟踪。

# 6. 服务版本检测

```text
nmap -sV target_ip
```

尝试确定运行在开放端口上的服务的版本。

# 7. 操作系统检测

```text
nmap -O target_ip
```

尝试确定目标的操作系统。

# 8. 扫描特定端口

```text
nmap -p 80,443 target_ip
```

仅扫描指定的端口（在此示例中为 `80` 和 `443`）。

# 9. 扫描所有 65535 个端口

```text
nmap -p- target_ip
```

扫描所有 `65535` 个端口。这可能需要更长时间，但可确保不会遗漏任何端口。

# 10. 输出到文件

```text
nmap -oN output.txt target_ip
```

将结果保存为名为 `"output.txt"` 的普通格式文件。

# 11. 以 XML 格式输出

```text
nmap -oX output.xml target_ip
```

以 XML 格式保存结果。

# 12. 脚本扫描

```text
nmap --script=default target_ip
```

对目标执行默认脚本。

# 13. 定时和性能

```text
nmap -T4 target_ip
```

将定时模板设置为激进模式，平衡速度和可靠性。

# 14. Ping 扫描

```text
nmap -sn target_ip
```

执行 ping 扫描，不进行端口扫描。

# 15. UDP 扫描

```text
nmap -sU target_ip
```

对目标执行 UDP 扫描。

# 64. iftop：显示接口的带宽使用情况

`iftop` 是一款用于 Linux 的命令行网络带宽监控工具。它显示你的系统与其他系统之间的网络连接列表，并显示每个连接的数据速率和数据信息。

## 示例

### 1. 基本用法

```text
iftop
```

这将启动 `iftop` 的交互模式，显示连接列表、数据速率和传输的总数据量。

### 2. 显示每秒字节数

```text
iftop -B
```

以每秒字节数显示带宽，而不是默认的每秒比特数。

### 3. 按端口过滤

```text
iftop -F 80
```

仅显示使用 `80` 端口的连接。可以根据需要使用其他端口号。

### 4. 显示时间戳

```text
iftop -t
```

为输出的每一行添加时间戳。

### 5. 监控特定接口

```text
iftop -i eth0
```

仅监控指定网络接口上的流量（将 `eth0` 替换为你的实际接口名称）。

### 6. 不解析主机名

```text
iftop -n
```

阻止 `iftop` 将 IP 地址解析为主机名，从而加快显示速度。

### 7. 在主机旁边显示端口

```text
iftop -N
```

同时显示主机及其对应的端口。

### 8. 应用 BPF 过滤器

```text
iftop -F "host 192.168.1.1"
```

使用 BPF 过滤器仅显示与指定主机的流量（将 `192.168.1.1` 替换为所需的 IP 地址）。

# 65. fsck：文件系统一致性检查和修复

`fsck` 命令（代表 "file system consistency check"，即文件系统一致性检查）是一个强大的实用工具，用于在 Linux 和其他类 Unix 操作系统中检查和修复磁盘上的文件系统不一致性。当系统遇到意外关机、断电或其他可能导致文件系统损坏的问题时，通常会使用它。`fsck` 可以处理各种文件系统类型，如 `ext2`、`ext3`、`ext4` 等。

## 示例

### 1. 检查文件系统

```text
fsck /dev/sda1
```

该命令检查和修复设备 `/dev/sda1` 上的文件系统。请将 `/dev/sda1` 替换为你的系统的适当设备标识符。

### 2. 自动修复文件系统

```text
fsck -y /dev/sda1
```

`-y` 选项自动回答 `fsck` 提出的所有问题为 `yes`，使其适用于无人值守的修复过程。

### 3. 交互修复

```text
fsck -r /dev/sda1
```

`-r` 选项在修复每个问题前提示用户确认。这允许你手动审查并批准每个修复。

### 4. 检查和修复所有文件系统

```text
fsck -A
```

该命令检查和修复 `/etc/fstab` 文件中指定的所有文件系统。它通常在系统启动过程中使用。

### 5. 检查特定类型的文件系统

```text
fsck.ext4 /dev/sda1
```

在此示例中，`fsck.ext4` 专门用于 `ext4` 文件系统。不同的文件系统可能有自己的 `fsck` 变体。

### 6. 强制检查文件系统，即使它是干净的

```text
fsck -f /dev/sda1
```

`-f` 选项强制检查文件系统，即使它看起来是干净的。这对于确保彻底检查很有用。

### 7. 检查和修复根文件系统

```text
fsck -f /
```

要检查和修复根文件系统，可能需要从实时 CD 或其他可启动媒体启动，以卸载根分区。

### 8. 试运行（检查但不修复）

```text
fsck -n /dev/sda1
```

`-n` 选项执行试运行，显示将执行的操作，但实际上不对文件系统做任何更改。

# 66. tac：反向连接并显示文件

Linux 中的 `tac` 命令用于连接并以反向顺序显示文件内容。“tac” 这个名字源于单词 "cat"（连接）的倒写。它是一个简单但强大的工具，在各种场景中都很实用，特别是当你想查看文件的末尾或将文本文件中行的顺序反转时。

## 示例

### 1. 基本用法

以反向顺序显示文件的内容。

```text
tac filename.txt
```

### 2. 反向连接多个文件

连接多个文件的内容并以反向顺序显示。

```text
tac file1.txt file2.txt
```

### 3. 反转命令输出

使用命令的输出作为 `tac` 的输入并反转顺序。

```text
ls -l | tac
```

### 4. 显示日志文件的末尾

以反向顺序查看日志文件的最后几行，以快速查看最新的条目。

```text
tac /var/log/syslog
```

### 5. 反转文件中的行并保存到另一个文件

反转文件中的行，并将结果保存到一个新文件中。

```bash
tac original.txt > reversed.txt
```

### 6. 递归反转目录中文件的顺序

显示目录及其子目录中所有文件的内容，并以反转顺序输出。

```bash
find /path/to/directory -type f -exec tac {} \;
```

### 7. 仅显示末尾的 N 行

仅显示文件末尾的特定行数。

```bash
tac -n 10 filename.txt # 显示最后 10 行
```

### 8. 带行号的反转输出

显示文件的反转内容，并附带行号。

```bash
tac -n filename.txt
```

### 9. 管道中行顺序的反转

将 `tac` 与其他命令结合在管道中使用。

```bash
cat filename.txt | grep "pattern" | tac
```

### 10. 压缩文件中行顺序的反转

使用 `zcat` 解压缩并以反转顺序显示压缩文件的内容。

```bash
zcat filename.txt.gz | tac
```

# 67. rev: 反转文件或文件的行

Linux 中的 `rev` 命令是一个简单的实用工具，用于反转行中的字符。它从文件或标准输入读取数据，反转每一行中字符的顺序，然后将结果写入标准输出。

## 示例

### 基本用法

```bash
echo "Hello, World!" | rev
```



## 从文件读取

```bash
rev textfile.txt
```

这将反转 `textfile.txt` 的内容，并将结果打印到控制台。

## 反转每个单词

```bash
echo "Linux is awesome" | rev | sed 's/ /\\n/g' | rev
```

## 仅反转行的一部分

```bash
echo "abcdef" | rev | cut -c 2-4 | rev
```

此示例反转整行的字符，提取第 2 到第 4 个字符，然后将它们反转回来。

## 反转文件中的每一行并重定向到另一个文件

```bash
rev input.txt > output.txt
```

这将从 `input.txt` 中读取每一行，反转字符，并将结果写入 `output.txt`。

## 反转变量中的字符串

```bash
my_string="OpenAI"
echo "$my_string" | rev
```

反转变量 `my_string` 的内容。

## 68. alias: 为命令创建别名

在 Linux 中，`alias` 命令用于为其他命令创建快捷方式或替代名称。这在节省时间、减少输入量或为复杂或常用的命令创建个性化快捷方式时特别有用。别名通常在 shell 配置文件中定义，例如 Bash 使用 `.bashrc`，以便在每次打开新的终端会话时都可用。

### 示例

#### 简单别名

```bash
alias ll='ls -l'
```

现在，每当你输入 `ll` 时，它将执行 `ls -l` 命令。

#### 自定义命令选项

```bash
alias grep='grep --color=auto'
```

此别名为 `grep` 命令的输出添加颜色，使其更容易区分匹配项。

#### 组合命令

```bash
alias update='sudo apt-get update && sudo apt-get upgrade'
```

此别名将更新和升级命令组合成单个命令。

#### 导航到特定目录

```bash
alias documents='cd ~/Documents'
```

输入 `documents` 会将当前目录更改为 `~/Documents`。

#### 强制递归删除

```bash
alias rm='rm -i'
```

此别名为 `rm` 命令添加交互式提示，在删除文件前要求确认。

#### 显示彩色的、人类可读的文件大小

```bash
alias df='df -h'
```

`-h` 选项使文件大小以人类可读的格式显示，例如 KB、MB、GB。

#### 仅列出目录

```bash
alias lsd='ls -l | grep "^d"'
```

此别名仅列出当前位置的目录。

#### 清除终端的快捷方式

```bash
alias cls='clear'
```

输入 `cls` 将清除终端屏幕。

## 69. date: 显示或设置系统日期和时间

Linux 中的 `date` 命令用于显示当前日期和时间，或设置系统日期和时间。它还允许你以各种格式格式化输出。

### 示例

#### 显示当前日期和时间

```bash
date
```

此命令将以默认格式显示当前的日期和时间。

#### 以自定义格式显示日期和时间

```bash
date +"%Y-%m-%d %H:%M:%S"
```

此示例将输出格式化为 "YYYY-MM-DD HH:MM:SS" 格式显示日期和时间。

#### 显示星期几

```bash
date +"%A"
```

此命令将显示当前的星期几。

#### 在特定时区显示日期

```bash
TZ="America/New_York" date
```

这将时区设置为 "America/New_York"，并显示该时区的当前日期和时间。你可以将 "America/New_York" 替换为所需的时区。

#### 计算未来/过去的日期

```bash
date --date="2 days ago"
```

此命令显示两天前的日期和时间。

## 70. cal: 显示日历

Linux 中的 `cal` 命令是一个简单的实用工具，用于在终端中显示日历。它可以显示当前月份、特定月份或整年的日历。

### 示例

#### 显示当前月份

```bash
cal
```

这将显示当前月份的日历，并高亮显示当前日期。

#### 显示当前年份的特定月份

```bash
cal 12 2023
```

此示例显示 2023 年 12 月的日历。你可以将 `12` 和 `2023` 替换为所需的月份和年份。

#### 显示特定年份

```bash
cal 2022
```

此命令显示 2022 年的完整日历。

#### 显示特定月份并高亮特定日期

```bash
cal -m 11 -y 2023
```

此示例显示 2023 年 11 月的日历，并高亮显示当前日期。`-m` 选项设置月份，`-y` 选项设置年份。

#### 显示周一为一周的第一天

```bash
cal -m
```

默认情况下，`cal` 命令以周日作为一周的开始。`-m` 选项将起始日更改为周一。

#### 显示特定国家的日历

```bash
cal -A 3 -B 2
```

此示例显示一个日历，包含当前月份后 3 个月 `-A 3` 和前 2 个月 `-B 2`。

#### 显示带周数的日历

```bash
cal -w
```

`-w` 选项在日历中添加周数。

#### 显示不同区域设置的日历

```bash
LC_TIME=fr_FR cal
```

此命令使用法语区域设置显示日历。你可以将 `fr_FR` 替换为适当的区域设置。

## 71. logname: 打印用户的登录名

Linux 中的 `logname` 命令用于显示当前用户的登录名。它从存储用户登录和登出信息的 utmp 或 wtmp 文件中获取用户的登录名。

### 示例

#### 基本用法

```bash
logname
```

这将简单地输出当前用户的登录名。

#### 使用命令替换

```bash
echo "The current user is $(logname)"
```

在此示例中，`logname` 命令在命令替换中使用，将用户的登录名嵌入到句子中。

#### 检查其他用户的登录名

```bash
logname -u username
```

将 `username` 替换为你要检查其登录名的用户的实际用户名。如果你想获取当前登录用户以外的其他用户的登录名，这会有用。

#### 与其他命令结合使用

```bash
echo "You are logged in as $(logname) and your home directory is $HOME"
```

此示例将 `logname` 的输出与 `echo` 命令结合使用，以显示当前用户的登录名和主目录。

#### 在脚本中检查登录名

```bash
#!/bin/bash
current_user=$(logname)
echo "The script is being run by $current_user"
```

在脚本中，你可以使用 `logname` 命令将当前用户的登录名存储到变量中，以便后续使用。

## 72. export: 设置环境变量

Linux 中的 `export` 命令用于设置环境变量。环境变量是影响系统上运行的进程行为的动态值。这些变量可以被设置它们的 shell 的任何子进程访问。

### 示例

#### 设置简单变量

```bash
export MY_VARIABLE="Hello, World!"
```

这将设置环境变量 `MY_VARIABLE` 的值为 "Hello, World!"。

#### 追加到 PATH

```bash
export PATH=$PATH:/usr/local/bin
```

这将 `/usr/local/bin` 添加到 `PATH` 环境变量的末尾。通常用于包含可执行文件所在的目录。

#### 为后续命令设置变量

```bash
export EDITOR=vim
```

这将默认文本编辑器设置为 Vim。后续依赖 `EDITOR` 变量的命令将使用 Vim。

#### 导出变量以供子 shell 使用

```bash
export MY_VARIABLE="Hello, Subshell!"
(echo $MY_VARIABLE)
```

在此示例中，变量被设置后在子 shell 中被访问。括号启动了一个子 shell，且该变量在此作用域内可用。

#### 设置多个变量

```bash
export VAR1="Value1" VAR2="Value2"
```

您可以在单条命令中导出多个变量，用空格分隔它们。



### 6. 取消设置变量：

```bash
export MY_VARIABLE=
```

将变量设置为空值实际上相当于取消设置该变量。

### 7. 在 Shell 脚本中导出变量：

```bash
#!/bin/bash
export SCRIPT_VAR="Script Variable"
echo $SCRIPT_VAR
```

运行 shell 脚本时，导出的变量在脚本环境中是可访问的。

### 8. 查看所有已导出变量：

```bash
export
```

不带任何参数运行 `export` 会显示所有当前已导出变量的列表。

## 73. hostname：显示或设置系统主机名。

Linux 中的 `hostname` 命令用于显示或设置系统的主机名。主机名是分配给网络设备上的标签，用于在各种网络操作中识别该设备。`hostname` 命令也有助于查看或更改系统的主机名。

示例：
- 查看当前主机名：

```bash
hostname
```

此命令将输出系统的当前主机名。
- 显示完全限定域名 (FQDN)：

```bash
hostname -f
```

`-f` 选项用于显示系统的 FQDN，其中包含主机名和域名。
- 临时设置新的主机名：

```bash
sudo hostname newhostname
```

此命令临时为系统设置一个新的主机名。
- 永久设置新的主机名（需要重启系统）：

```bash
sudo hostnamectl set-hostname newhostname
```

此命令为系统设置新的主机名，且更改将在重启后保留。它使用 `hostnamectl`，这是用于查询和更改系统主机名及相关设置的工具。
- 查看静态主机名（配置在 `/etc/hostname` 中）：

```bash
cat /etc/hostname
```

静态主机名通常在 `/etc/hostname` 文件中配置。此命令显示该文件的内容。
- 使用文本编辑器编辑静态主机名：

```bash
sudo nano /etc/hostname
```

使用 `nano` 等文本编辑器编辑 `/etc/hostname` 文件中的静态主机名。编辑完成后，保存更改并退出编辑器。
- 编辑 hosts 文件以将主机名与 IP 地址关联：

```bash
sudo nano /etc/hosts
```

`/etc/hosts` 文件将 IP 地址映射到主机名。您可以编辑此文件以将您的主机名与期望的 IP 地址关联。
- 检查当前域名：

```bash
domainname
```

此命令显示与系统关联的 NIS/YP 域名。

## 74. zip：打包和压缩文件。

Linux 中的 `zip` 命令用于将文件和目录压缩为 zip 归档文件。它是一种跨平台创建和管理压缩文件的流行实用工具。

示例：
- 压缩单个文件：

```bash
zip archive.zip file.txt
```

这将创建一个名为 `archive.zip` 的 zip 归档文件，其中包含文件 `file.txt`。
- 压缩多个文件：

```bash
zip archive.zip file1.txt file2.txt
```

创建一个名为 `archive.zip` 的 zip 归档文件，包含 `file1.txt` 和 `file2.txt`。
- 压缩目录：

```bash
zip -r archive.zip directory/
```

`-r` 选项用于递归地将指定目录（`directory/`）中的所有文件和子目录包含在 zip 归档文件中。
- 将文件添加到现有归档：

```bash
zip -u archive.zip newfile.txt
```

`-u` 选项通过添加 `newfile.txt` 来更新现有的 zip 归档（`archive.zip`）。
- 设置压缩级别：

```bash
zip -9 archive.zip file.txt
```

`-9` 选项将压缩级别设置为最大。您可以使用 1 到 9 的值来调整压缩级别，其中 1 是最快压缩，9 是最佳压缩。
- 排除文件：

```bash
zip archive.zip *.txt -x exclude.txt
```

此命令创建一个 zip 归档（`archive.zip`），包含当前目录中所有 `.txt` 文件，但排除文件 `exclude.txt`。
- 密码保护 Zip 归档：

```bash
zip -e secure.zip sensitive-file.txt
```

`-e` 选项提示输入密码，并创建包含指定文件（`sensitive-file.txt`）的密码保护的 zip 归档（`secure.zip`）。
- 列出 Zip 归档的内容：

```bash
unzip -l archive.zip
```

使用 `unzip -l` 命令列出色 zip 归档（`archive.zip`）的内容而不提取它们。
- 提取 Zip 归档：

```bash
unzip archive.zip
```

`unzip` 命令将 zip 归档（`archive.zip`）的内容提取到当前目录。

## 75. unzip：解包 zip 归档。

Linux 中的 `unzip` 命令用于从 ZIP 格式压缩归档中提取文件。它是一个多用途工具，大多数 Linux 发行版都预装了它。

示例：
- 提取 ZIP 文件：

```bash
unzip file.zip
```

此命令将在当前目录中提取 `file.zip` 中的所有文件。
- 提取到特定目录：

```bash
unzip file.zip -d /path/to/destination
```

这将把 `file.zip` 的内容提取到指定的目标目录。
- 列出 ZIP 文件的内容：

```bash
unzip -l file.zip
```

`-l` 选项列出 ZIP 文件的内容而不提取它们。
- 提取特定文件：

```bash
unzip file.zip file1.txt file2.txt
```

您可以指定要从 ZIP 归档中提取的特定文件。
- 覆盖现有文件：

```bash
unzip -o file.zip
```

`-o` 选项在不需要提示的情况下覆盖现有文件。
- 静默模式（无输出）：

```bash
unzip -q file.zip
```

`-q` 选项抑制在提取时打印文件和目录名称。
- 以完整路径提取：

```bash
unzip -j file.zip
```

`-j` 选项提取文件时不带其路径，丢弃任何目录结构。
- 受密码保护的 ZIP 文件：

```bash
unzip -P your_password file.zip
```

使用 `-P` 选项后跟密码来从受密码保护的 ZIP 归档中提取文件。
- 测试 ZIP 文件的完整性：

```bash
unzip -t file.zip
```

`-t` 选项在不提取内容的情况下测试 ZIP 文件的完整性。
- 更新现有文件：

```bash
unzip -u file.zip
```

`-u` 选项更新现有文件，并从 ZIP 归档中提取新文件。

## 76. lsblk：列出有关块设备的信息。

Linux 中的 `lsblk` 命令用于列出有关块设备（如硬盘及其分区）的信息。它提供了系统中连接的块设备、其挂载点、大小和关系的详细概述。

示例：
- 基本用法：

```bash
lsblk
```

不带任何选项的此命令显示系统中所有块设备的层级列表。
- 显示文件系统信息：

```bash
lsblk -f
```

此选项包含每个设备上的文件系统类型信息。
- 以字节显示大小：

```bash
lsblk -b
```

以字节打印大小，而不是默认的可读格式。
- 显示所有设备，包括空设备：

```bash
lsblk -a
```

在输出中包含空设备。
- 显示设备权限：

```bash
lsblk -m
```

显示关于设备权限的信息。
- 显示特定设备信息：



```bash
lsblk /dev/sda
```

显示特定设备（在此例中为 `/dev/sda`）的信息。

- **不打印依赖设备：**

```bash
lsblk -d
```

抑制依赖设备的输出。仅显示顶级设备。

- **以 ASCII 字符打印树结构：**

```bash
lsblk -i
```

使用 ASCII 字符绘制树状结构，提供可视化表示。

## 77. findmnt：显示当前已挂载的文件系统信息。

Linux 中的 `findmnt` 命令用于显示当前已挂载的文件系统列表或搜索特定的挂载点。它以简洁且易于阅读的格式提供已挂载文件系统的相关信息。`findmnt` 命令是 util-linux 软件包的一部分，在大多数 Linux 发行版中均可用。

### 示例：

- **列出所有已挂载的文件系统：**

```bash
findmnt
```

此命令将显示所有已挂载文件系统的列表，包括它们的挂载点、源设备、文件系统类型及其他相关信息。

- **按文件系统类型过滤：**

```bash
findmnt -t ext4
```

此命令将仅显示 ext4 文件系统类型的已挂载文件系统。

- **按源设备过滤：**

```bash
findmnt -S /dev/sda1
```

此命令将显示与 `/dev/sda1` 设备相关联的已挂载文件系统信息。

- **显示特定列：**

```bash
findmnt -o SOURCE,TARGET,FSTYPE,OPTIONS
```

此命令将仅显示指定的列：源设备、目标挂载点、文件系统类型和挂载选项。

- **列出网络文件系统（NFS、SMB）：**

```bash
findmnt -t nfs,smb
```

此命令将显示已挂载的 NFS 和 SMB 文件系统信息。

- **搜索特定挂载点：**

```bash
findmnt /mnt/data
```

如果挂载点 `/mnt/data` 当前已挂载，此命令将显示有关该挂载点的信息。

- **显示无标题信息：**

```bash
findmnt -n
```

此命令将显示没有列标题的信息，使其适合在脚本中进行解析。

## 78. mount：挂载文件系统。

Linux 中的 `mount` 命令用于将文件系统连接到目录树。此操作使连接的文件系统上的文件和目录可被系统访问和使用。`mount` 命令对于操作外部存储设备、网络共享和其他文件系统至关重要。

### 示例：

- **挂载 USB 驱动器：**

```bash
sudo mount /dev/sdb1 /mnt/usb
```

此命令将 USB 驱动器的第一个分区（`/dev/sdb1`）挂载到 `/mnt/usb` 目录。请确保在运行命令之前挂载点（在此例中为 `/mnt/usb`）已存在。

- **挂载 ISO 镜像：**

```bash
sudo mount -o loop path/to/image.iso /mnt/iso
```

在此处，使用 `-o loop` 选项将 ISO 镜像文件（`path/to/image.iso`）作为设备挂载。ISO 文件的内容将在 `/mnt/iso` 目录中可访问。

- **挂载网络共享（NFS）：**

```bash
sudo mount -t nfs server:/shared_folder /mnt/network_share
```

此示例将 NFS 服务器上的共享文件夹（`server:/shared_folder`）挂载到本地目录 `/mnt/network_share`。`-t nfs` 选项指定文件系统类型为 NFS。

- **以特定文件系统类型挂载：**

```bash
sudo mount -t ext4 /dev/sdc1 /mnt/data
```

在这种情况下，`-t ext4` 选项明确指定设备的文件系统类型（本例中为 ext4）为（`/dev/sdc1`）。然后该设备被挂载到 `/mnt/data` 目录。

- **以只读选项挂载：**

```bash
sudo mount -o ro /dev/sdd1 /mnt/read_only
```

`-o ro` 选项以只读模式挂载设备（`/dev/sdd1`），确保无法在文件系统上执行写操作。这对于保护设备上的数据完整性可能非常有用。

- **卸载设备：**

```bash
sudo umount /mnt/usb
```

要断开已挂载设备，请使用 `umount` 命令后跟挂载点。在此示例中，挂载在 `/mnt/usb` 的 USB 驱动器被卸载。

## 79. umount：卸载已挂载的文件系统。

Linux 中的 `umount` 命令用于卸载（断开）当前已挂载的文件系统，以便可以访问或移除底层设备或目录。正确卸载文件系统对于确保数据完整性和防止数据损坏至关重要。

### 示例：

- **卸载文件系统：**

```bash
umount /mnt/data
```

此示例将卸载挂载在 `/mnt/data` 的文件系统。

- **卸载设备：**

```bash
umount /dev/sdb1
```

卸载与指定设备相关联的文件系统，在此例中为 `/dev/sdb1`。

- **强制卸载：**

```bash
umount -f /mnt/data
```

强制卸载，在文件系统忙碌时很有用。请谨慎使用，因为如果进程正在积极使用文件系统，可能会导致数据损坏。

- **卸载所有文件系统：**

```bash
umount -a
```

卸载 `/etc/fstab` 中列出的所有文件系统。请谨慎使用，尤其是在运行中的系统上。

- **按设备名称卸载：**

```bash
umount /dev/sdb*
```

卸载与匹配模式 `/dev/sdb*` 的设备相关联的所有文件系统。

- **按挂载点卸载：**

```bash
umount -R /mnt/data
```

递归卸载指定目录下所有已挂载的文件系统。

- **详细输出：**

```bash
umount -v /mnt/data
```

显示有关卸载过程的详细信息。

- **试运行（测试）：**

```bash
umount -n /mnt/data
```

模拟卸载操作，而不实际断开文件系统。适用于测试。

- **卸载 NFS 共享：**

```bash
umount -t nfs server:/mnt/share
```

卸载 NFS（网络文件系统）共享。

- **卸载 CIFS 共享：**

```bash
umount -t cifs //server/share /mnt/cifs
```

卸载 CIFS（通用互联网文件系统）共享。

- **延迟断开卸载：**

```bash
umount --lazy /mnt/data
```

延迟断开文件系统，允许进程继续使用该文件系统，直到它们完成工作。

- **卸载并断开回环设备：**

```bash
losetup -d /dev/loop0 && umount /mnt/loop
```

断开回环设备，然后卸载相关联的文件系统。

## 80. sftp：通过 SSH 协议安全传输文件。

`SFTP`（安全文件传输协议）是 FTP（文件传输协议）的安全替代方案，用于在网络上的计算机之间传输文件。它在不安全的网络（通常是互联网）上提供安全通道。SFTP 加密命令和数据连接，防止对敏感信息的未授权访问。

### 示例：

- **连接到远程服务器：**

```bash
sftp username@remote_host
```

用你的远程用户名替换 `username`，用服务器的 IP 地址或域名替换 `remote_host`。

- **使用自定义端口连接：**

```bash
sftp -oPort=2222 username@remote_host
```

此示例使用 2222 端口连接到远程服务器。根据需要调整端口号。

- **上传文件到远程服务器：**

```bash
put local_file.txt
```

此命令将 `local_file.txt` 上传到远程服务器上的当前工作目录。

- **从远程服务器下载文件：**

```bash
get remote_file.txt
```

从远程服务器下载 `remote_file.txt` 到本地工作目录。

- **在远程服务器上导航：**

```bash
cd remote_directory
```

更改远程服务器上的当前工作目录。

- **在本地机器上导航：**

```bash
lcd local_directory
```

更改本地机器上的当前工作目录。

- **列出远程服务器上的文件：**

```bash
ls
```

列出当前远程目录中的文件和目录。

- **列出本地机器上的文件：**

```bash
lls
```

列出当前本地目录中的文件和目录。

- **删除远程服务器上的文件：**

```bash
rm remote_file.txt
```

从远程服务器删除 `remote_file.txt`。



## 递归上传或下载

```bash
put -r local_directory
```

将整个本地目录及其内容递归上传到远程服务器。

```bash
get -r remote_directory
```

将整个远程目录及其内容递归下载到本地机器。

## 保留文件时间戳

```bash
put -P local_file.txt
```

保留上传文件在远程服务器上的时间戳。

## 退出 SFTP 会话

```
exit
```

关闭 SFTP 会话并返回到本地 shell。

## 81. locate：在系统上查找文件和目录的位置

`locate` 是 Linux 中用于查找文件和目录位置的命令行实用工具。它依赖于预先构建的文件及其位置索引，因此是比直接搜索文件系统更快的替代方案。

### 示例

1. **搜索文件**

```
locate myfile.txt
```

此命令将搜索并显示系统中所有名为 `myfile.txt` 的文件的路径。

2. **不区分大小写的搜索**

```
locate -i MyFile.txt
```

`-i` 选项使搜索不区分大小写，因此它会匹配 `myfile.txt`、`MyFile.txt` 等文件。

3. **将搜索限制在特定目录**

```
locate -r '/home/user/*.txt'
```

`-r` 选项允许你使用正则表达式。此示例搜索 `/home/user/` 目录中所有扩展名为 `.txt` 的文件。

4. **更新 locate 数据库**

```
sudo updatedb
```

`locate` 依赖于一个需要定期更新的数据库。`updatedb` 命令用于刷新此数据库。通常使用 `sudo` 运行，因为它可能需要访问系统文件。

5. **显示匹配数量**

```
locate -c myfile.txt
```

`-c` 选项统计匹配的数量，但不显示实际路径。

6. **显示相对于根目录的路径**

```
locate -r '^/etc\.\*\.conf$'
```

此示例使用正则表达式查找 `/etc` 目录中所有扩展名为 `.conf` 的文件。`^` 表示路径的开头。

7. **抑制警告**

```
locate -q myfile.txt
```

`-q` 选项抑制关于不可读目录和权限的警告。

8. **显示版本信息**

```
locate --version
```

显示 `locate` 命令的版本信息。

9. **帮助**

```
man locate
```

显示 `locate` 命令的手册页，提供有关其用法和选项的详细信息。

## 82. last：显示最近登录用户的列表

Linux 中的 `last` 命令用于显示系统中最近登录用户的信息。它从 `/var/log/wtmp` 文件中提取数据，该文件记录了登录和注销活动。

### 示例

1. **显示最近登录的用户**

```
last
```

这将显示已登录用户的列表，包括他们的登录和注销时间以及会话持续时间。

2. **显示最近 5 次登录**

```
last -n 5
```

此命令显示最近 5 次登录，提供更简洁的输出。

3. **显示特定用户的最近登录记录**

```
last username
```

将 `username` 替换为你要查看的实际用户名。这将显示该特定用户的登录/注销历史。

4. **仅显示重启条目**

```
last reboot
```

此命令显示系统重启列表及相应的时间。

5. **显示特定日期的登录记录**

```
last -F YYYYMMDD
```

将 `YYYYMMDD` 替换为所需的日期，格式为年-月-日（例如，20231110 代表 2023 年 11 月 10 日）。这将仅显示在该特定日期的登录记录。

6. **显示特定时段的登录记录**

```
last -s YYYY-MM-DD -t YYYY-MM-DD
```

将开始日期（`-s`）和结束日期（`-t`）替换为所需的日期范围。此命令将显示指定时段内的登录记录。

7. **显示 IP 地址及用户登录信息**

```
last -i
```

此选项包含 IP 地址及用户登录信息，提供关于登录来源的额外信息。

8. **在输出中显示主机名**

```
last -a
```

`-a` 选项在输出中显示主机名，提供有关用户从哪个主机登录的信息。

## 83. stty：更改和打印终端行设置

Linux 中的 `stty` 命令用于更改和打印终端行设置。它允许用户配置终端界面的各个方面，例如输入和输出设置、控制字符等。

### 示例

1. **显示当前终端设置**

```
stty -a
```

此命令显示终端的所有当前设置。

2. **更改擦除字符**

```
stty erase ^H
```

这将把擦除字符更改为 `Ctrl + H`（退格键）。你可以将 `^H` 替换为合适的控制字符。

3. **禁用回显（密码输入）**

```
stty -echo
```

此命令关闭字符输入时的回显功能。适用于密码输入。

4. **启用回显**

```
stty echo
```

此命令开启字符回显功能。

5. **更改终端大小**

```
stty rows 40 cols 80
```

这将终端大小设置为 40 行和 80 列。根据你的需求调整数值。

6. **忽略中断信号（Ctrl + C）**

```
stty intr ""
```

此命令忽略中断信号（`Ctrl + C`）。双引号表示空字符串。

7. **恢复默认终端设置**

```
stty sane
```

此命令将终端恢复到正常状态，撤销使用 `stty` 所做的任何更改。

8. **禁用流量控制（Ctrl + S 和 Ctrl + Q）**

```
stty -ixon
```

此命令禁用软件流量控制，允许你将 `Ctrl + S` 和 `Ctrl + Q` 用于其他目的。

9. **设置输入和输出速度**

```
stty speed 9600
```

这将输入和输出速度设置为 9600 波特。根据你的要求调整数值。

10. **将终端设置为原始模式**

```
stty raw
```

这将终端置于原始模式，输入未经任何处理直接通过（适用于某些交互式应用程序）。

## 84. tail：显示文件的末尾部分

Linux 中的 `tail` 命令是一个强大的实用工具，允许你显示文本文件或数据流的最后几行。它特别适用于实时监控日志文件或快速查看大文件的末尾。

### 示例

1. **显示文件的最后 10 行**

```
tail filename
```

2. **从文件末尾显示特定行数的内容**

```
tail -n 20 filename
```

这将显示文件的最后 20 行。

3. **实时监控文件（类似于 `tail -f`）**

```
tail -f filename
```

这通常用于监控日志文件，当新行被添加时进行更新。

4. **显示并持续更新文件的最后 10 行**

```
tail -n 10 -f filename
```

5. **显示文件的末尾部分，并随着新数据的添加而更新**

```
tail -c 500 filename
```

这将显示文件的最后 500 个字节。

6. **显示在特定点之后添加到文件的行**

```
tail -n +5 filename
```

这将显示从第 5 行开始到文件末尾的所有行。

7. **显示添加到文件的行，但仅显示更改内容**

```
tail -n 10 -f filename | grep "pattern"
```

当新行被添加时，这将仅显示包含指定模式的行。

8. **按倒序显示行（从末尾到开头）**

```
tac filename | tail -n 10
```

注意：`tac` 是 `cat` 的反向操作，并且并非在所有系统上都可用。

9. **同时显示多个文件**

```
tail -n 5 file1 file2
```

这将显示两个文件的最后 5 行。

## 85. head：显示文件的开头部分

Linux 中的 `head` 命令用于显示文本文件或数据流的开头部分。默认情况下，它显示文件的前 10 行，但你可以通过使用 `-n` 选项指定不同的行数。

### 示例

1. **显示文件的前 10 行**

`head` 命令用于显示文件的开头部分。默认情况下，它显示前 10 行。

**示例：**



# head 命令示例

## 1. 显示文件的前 10 行（默认）：

```bash
head filename.txt
```

## 2. 显示文件中的特定行数（例如，5 行）：

```bash
head -n 5 filename.txt
```

## 3. 显示文件的前 20 个字节：

```bash
head -c 20 filename.txt
```

## 4. 仅在指定多个文件时显示文件头：

```bash
head -q file1.txt file2.txt
```

## 5. 始终显示文件头，即使只有一个文件：

```bash
head -v filename.txt
```

## 6. 使用管道（`|`）将 `head` 与其他命令组合使用：

```bash
cat filename.txt | head -n 8
```

此示例使用 `cat` 显示整个文件内容后，再利用 `head` 显示该文件的前 8 行。

## 7. 显示命令输出的前几行：

```bash
ls -l | head
```

这会显示 `ls -l` 命令输出的前 10 行。

## 8. 显示多个文件的前 3 行：

```bash
head -n 3 file1.txt file2.txt
```

此命令显示 `file1.txt` 和 `file2.txt` 的前 3 行。

## 9. 显示目录中所有文本文件的前 N 行：

```bash
head -n N *.txt
```

将 `N` 替换为所需的行数。此命令显示当前目录中所有扩展名为 `".txt"` 的文本文件的前 `N` 行。

# 86. chsh：更改登录 Shell

Linux 中的 `chsh` 命令用于更改用户的默认登录 Shell。“Shell”是指允许用户与操作系统交互的命令解释器。Linux 系统中的每个用户都被分配了一个默认 Shell，而 `chsh` 提供了一种修改该设置的方法。

## 示例

### 1. 更改当前用户的默认 Shell：

```bash
chsh -s /bin/zsh
```

此命令将当前登录用户的默认 Shell 更改为 Zsh。您需要提供目标 Shell 的完整路径（在此例中为 `/bin/zsh`）。

### 2. 更改特定用户的默认 Shell：

```bash
chsh -s /bin/bash username
```

将 `username` 替换为您想要更改默认 Shell 的实际用户名。此示例将默认 Shell 更改为 Bash。

### 3. 列出可用的 Shell：

```bash
chsh -l
```

此命令列出系统上所有可用的 Shell。输出将显示可用 Shell 的路径。

### 4. 交互模式：

```bash
chsh
```

运行不带任何选项的 `chsh` 会提示您输入所需的 Shell。它将交互式地询问新 Shell 的路径。只需输入路径并按 Enter 即可。

### 5. 将默认 Shell 更改为当前用户的 Shell：

```bash
chsh -s "$(which zsh)"
```

此示例使用 `which` 命令获取当前用户 Shell（在此例中为 Zsh）的路径，并将其设置为默认 Shell。

### 6. 以 root 身份更改其他用户的默认 Shell：

```bash
sudo chsh -s /bin/fish username
```

此命令允许系统管理员（root）更改其他用户的默认 Shell。将 `username` 替换为实际用户名，将 `/bin/fish` 替换为所需的 Shell。

# 87. stat：显示文件或文件系统状态

Linux 中的 `stat` 命令用于显示文件或文件系统的详细信息。它提供了一套全面的细节，包括文件类型、访问权限、inode 编号、UID（用户 ID）、GID（组 ID）、大小，以及最后访问时间、修改时间和状态变更时间的时间戳。

## 示例

### 1. 显示基本信息：

```bash
stat filename
```

这提供了文件的基本信息，包括大小、权限和时间戳。

### 2. 以简洁格式显示信息：

```bash
stat -t filename
```

这以简洁形式显示信息，适用于脚本编写或提取特定细节。

### 3. 显示文件系统信息：

```bash
stat -f filename
```

这显示文件所在文件系统的相关信息，包括总空间和空闲空间。

### 4. 显示多个文件的信息：

```bash
stat file1 file2
```

您可以提供多个文件作为参数，以获取每个文件的信息。

### 5. 自定义输出格式：

```bash
stat --format="File: %n Size: %s bytes" filename
```

使用控制字符自定义输出格式。`%n` 代表文件名，`%s` 代表文件大小。

### 6. 跟随符号链接：

```bash
stat -L symlink
```

如果文件是符号链接，此命令将显示被链接文件的信息，而不是链接本身的信息。

### 7. 递归显示信息：

```bash
find /path/to/directory -type f -exec stat {} \;
```

使用带有 `exec` 的 `find` 命令递归地对目录中的所有文件应用 `stat`。

### 8. 显示 Inode 编号：

```bash
stat --format="Inode: %i" filename
```

`%i` 代表文件的 inode 编号。

### 9. 人类可读的输出：

```bash
stat --format="Size: %s bytes" --printf="%h\n" filename
```

`--printf` 中的 `%h` 提供人类可读的文件大小。

# 88. watch：重复执行命令并显示结果

Linux 中的 `watch` 命令是一个实用工具，允许您定期执行给定命令并实时显示结果。这对于监控命令输出的变化或更新而无需每次都手动重新运行特别有用。

## 示例

### 1. 基本用法：

```bash
watch date
```

这将每隔 2 秒（默认）持续更新并显示当前日期和时间。

### 2. 监控磁盘空间：

```bash
watch df -h
```

此命令将定期显示磁盘空间使用情况，默认每隔 2 秒更新一次。

### 3. 检查系统资源使用情况：

```bash
watch -n 1 top
```

`-n` 选项允许您指定以秒为单位的更新间隔。在此示例中，`top` 将每秒刷新一次，提供关于系统资源使用情况的实时信息。

### 4. 监控日志文件：

```bash
watch -n 5 tail /var/log/syslog
```

此示例监控系统日志文件，每隔 5 秒更新一次。这对于实时查看日志条目非常有用。

### 5. 跟踪文件变化：

```bash
watch -d ls -l
```

`-d` 选项突出显示连续两次更新之间的差异。在这种情况下，它会在每次刷新时显示文件列表的变化。

### 6. 监控网络连接：

```bash
watch -n 2 ss -t -a
```

此示例使用 `ss` 命令显示关于 TCP 套接字连接的信息。它每隔 2 秒刷新一次。

### 7. 自定义更新间隔：

```bash
watch -n 10 free -m
```

这里，更新间隔设置为 10 秒，并使用命令 `free -m` 以兆字节为单位显示内存使用情况。

### 8. 突出显示命令输出的变化：

```bash
watch -d 'ps aux | grep ssh'
```

`-d` 选项突出显示命令 `ps aux | grep ssh` 输出在每次更新时的差异，便于发现变化。

### 9. 监控脚本：

```bash
watch ./myscript.sh
```

您可以使用 `watch` 持续监控脚本的输出。将 `./myscript.sh` 替换为您的脚本路径。

### 10. 组合多个命令：

```bash
watch 'echo "Hello" && date && df -h'
```

您可以使用 `watch` 后的单引号内的复合命令按顺序执行多个命令并查看它们的输出。

# 89. shutdown：关机或重启系统

Linux 中的 `shutdown` 命令用于以安全且有序的方式关闭系统。它允许您计划系统关机或重启，给用户警告并防止新的登录。

## 示例

### 1. 立即关机：

```bash
sudo shutdown now
```

### 2. 计划在 10 分钟后关机：

```bash
sudo shutdown +10
```

系统将在 10 分钟后关机。

### 3. 计划在特定时间关机：

```bash
sudo shutdown 22:00
```

此命令计划在晚上 10:00 关机。

### 4. 在关机前显示自定义消息：



```bash
sudo shutdown +5 "System maintenance in 5 minutes. Save your work!"
```

用户将在关机前 5 分钟看到指定的消息。

### 5. 取消已计划的关机：

### 6. 立即重启系统：

```
sudo shutdown -r now
```

此命令会立即重启系统。

### 7. 安排15分钟后重启：

```
sudo shutdown -r +15
```

系统将在15分钟后重启。

### 8. 安排在特定时间重启：

```
sudo shutdown -r 08:30
```

这将安排在早上8:30重启系统。

### 9. 在重启前显示消息：

```
sudo shutdown -r +5 "System will reboot in 5 minutes for updates."
```

用户将在重启前五分钟看到指定的消息。

## 90. reboot: 重启系统。

Linux 中的 `reboot` 命令用于重启系统。它是一个简单的命令，允许你优雅地启动系统重启。

### 示例：

- 1. **简单重启：**

```
reboot
```

此命令将立即启动系统重启。

- 2. **延迟重启：**

```
reboot -d 60
```

`-d` 选项指定在启动重启前的延迟秒数。在此示例中，系统将在60秒延迟后重启。

- 3. **强制重启：**

```
reboot -f
```

`-f` 选项强制立即重启，而不会优雅地终止进程。请谨慎使用此选项，因为如果有未保存的更改，可能会导致数据丢失。

- 4. **带消息重启：**

```
reboot -n "System will restart for updates at 3:00 PM"
```

`-n` 选项允许你添加一条消息，该消息将在重启前发送给所有已登录的用户。

- 5. **重启到特定内核：**

```
reboot -k 5.4.0-81-generic
```

`-k` 选项允许你指定系统重启后要启动的特定内核版本。

- 6. **重启后关机：**

```
reboot -p
```

`-p` 选项在重启后关闭系统。当你想完全关闭机器时，这很有用。

- 7. **按计划时间重启：**

```
shutdown -r 22:30
```

或者，你可以使用 `shutdown` 命令来安排在特定时间重启。在此示例中，系统将在晚上10:30重启。

## 91. lsusb: 显示有关USB总线和设备的信息。

Linux 中的 `lsusb` 命令用于列出连接到系统的USB（通用串行总线）设备的信息。它提供详细信息，如供应商和产品ID、设备类以及与USB设备相关的其他信息。

### 示例：

- 1. **基本用法：**

```
lsusb
```

此命令将列出连接到系统的USB设备。

- 2. **详细输出：**

```
lsusb -v
```

这将提供有关每个USB设备的详细信息，包括配置、接口等。

- 3. **树状视图：**

```
lsusb -t
```

以树状结构显示USB设备，展示它们之间的层次结构和关系。

- 4. **特定设备：**

```
lsusb -d 045e:00cb
```

将 `045e:00cb` 替换为你想要获取信息的特定USB设备的供应商和产品ID。此命令将显示关于该特定设备的详细信息。

- 5. **列出总线和设备编号：**

```
lsusb -t | grep -i 'bus\\device'
```

此命令显示总线和设备编号的简洁列表，使识别USB设备更容易。

- 6. **仅显示设备描述：**

```
lsusb | awk '{print $6, $7, $8, $9, $10, $11, $12, $13}'
```

此命令使用 `awk` 仅显示设备描述。

- 7. **显示USB 3.0设备：**

```
lsusb | grep '3.0'
```

此命令过滤输出以仅显示USB 3.0设备，帮助你识别高速USB连接。

- 8. **显示总线和设备编号：**

```
lsusb | cut -d' ' -f2,4
```

此命令提取并显示USB设备的总线和设备编号。

## 92. lspci: 显示有关PCI总线和连接设备的信息。

Linux 中的 `lspci` 命令是一个强大的工具，提供有关系统中PCI总线及其连接设备的详细信息。PCI（外围组件互连）是一种标准接口，用于将各种硬件设备（如网卡、显卡和存储控制器）连接到计算机的主板上。

### 示例：

- 1. **列出所有PCI设备：**

```
lspci
```

此命令以紧凑格式显示所有PCI设备的列表。

- 2. **显示特定设备的详细信息：**

```
lspci -v -s <bus>;<device>.<function>
```

将 `<bus>`、`<device>` 和 `<function>` 替换为 `lspci` 命令输出中的相应值。这提供了关于特定PCI设备的详细（冗长）信息。

- 3. **以人类可读格式显示信息：**

```
lspci -nn
```

此命令以更具人类可读性的格式显示供应商和设备代码。

- 4. **显示特定供应商的信息：**

```
lspci -d <vendor_id>
```

将 `<vendor_id>` 替换为供应商的十六进制代码。此命令显示来自特定供应商的设备列表。

- 5. **显示使用的内核驱动和模块：**

```
lspci -k
```

此命令显示每个PCI设备当前使用的内核驱动和模块的信息。

- 6. **列出所有设备及其IRQ分配：**

```
lspci -v -vv
```

此命令提供非常详细的输出，包括每个PCI设备的IRQ分配。

- 7. **以树状格式显示PCI设备：**

```
lspci -t
```

此命令以树状结构组织PCI设备，展示总线和设备的层次结构。

- 8. **仅显示以太网设备：**

```
lspci | grep Ethernet
```

此命令使用 `grep` 过滤输出，仅显示包含“Ethernet”的行，帮助你快速识别网络相关设备。

## 93. strace: 跟踪系统调用和信号。

`strace` 是一个强大的命令行工具，用于Linux和其他类Unix操作系统，以跟踪和调试进程发出的系统调用和信号。它允许你检查进程与Linux内核之间的交互，提供关于程序系统级行为的宝贵见解。

### 示例：

- 1. **跟踪命令：**

```
strace ls -l
```

此命令跟踪 `ls` 命令在以长格式列出文件时发出的系统调用。

- 2. **将输出重定向到文件：**

```
strace -o output.txt ls -l
```

此示例将 `strace` 的输出重定向到名为 `output.txt` 的文件，以便稍后分析。

- 3. **跟踪特定系统调用：**

```
strace -e trace=open,read,write ls -l
```

此命令仅跟踪 `ls` 命令发出的 `open`、`read` 和 `write` 系统调用。

- 4. **显示时间戳：**

```
strace -t ls -l
```

它为输出的每一行添加时间戳，提供关于每个系统调用发生时间的信息。

- 5. **显示带参数的系统调用：**

```
strace -v ls -l
```

`-v` 选项提供更详细的信息，包括每个系统调用的参数。

- 6. **跟踪正在运行的进程：**

```
strace -p PID
```

将 `PID` 替换为你想要跟踪的正在运行的进程的进程ID。

- 7. **过滤特定系统调用的输出：**

```
strace -e trace=write -e write=1 ls -l
```

此示例仅跟踪 `write` 系统调用，特别是针对文件描述符1（stdout）。

- 8. **统计系统调用：**

```
strace -c ls -l
```

它打印每个系统调用的计数和时间的摘要，提供系统调用活动的快速概览。

## 94. vmstat: 报告虚拟内存统计信息。

`vmstat` 是Linux中的一个命令行实用程序，提供关于虚拟内存统计信息、系统资源、进程和CPU利用率的信息。“vmstat”这个名字代表“virtual memory statistics”（虚拟内存统计）。它是系统管理员和用户监测和分析系统性能的一个有用工具。

### 示例：

- 1. **基本用法：**

```
vmstat
```

此命令显示虚拟内存统计信息的摘要，包括进程、内存、交换分区和CPU利用率。这些值代表自上次重启以来的平均值。

- 2. 显示内存统计信息

```bash
vmstat -s
```

此命令提供内存统计摘要，显示以千字节为单位的总内存、已用内存和可用内存。

- 3. 显示进程相关信息

```bash
vmstat -p [partition]
```



此命令显示进程相关信息，包括进程 ID、优先级、虚拟内存大小、常驻集大小等。您可以指定特定的分区来过滤输出。

### 4. 显示磁盘统计信息

```bash
vmstat -d
```

此命令提供磁盘统计信息，包括读/写次数、读取/写入的块数以及每秒 I/O 操作数。

### 5. 定期显示系统信息

```bash
vmstat 2 5
```

此命令每 2 秒显示一次系统统计信息，共显示 5 次。

### 6. 显示 CPU 使用率

```bash
vmstat -n 2 5
```

此命令每 2 秒显示一次 CPU 使用率，共显示 5 次。`-n` 选项防止显示表头，使输出更易于解析。

### 7. 显示进程队列统计信息

```bash
vmstat -q
```

此命令显示有关进程队列的信息，包括等待 CPU 时间的进程数量和处于不可中断睡眠状态的进程数量。

### 8. 显示内核线程

```bash
vmstat -t
```

此命令显示时间戳以及包括内核线程在内的各种统计信息。

## 95. ss: 显示套接字统计信息

Linux 中的 `ss` 命令是一个强大的工具，用于显示套接字统计信息。它提供系统中网络套接字的详细信息，包括其状态、类型及其他相关细节。`ss` 命令是 `iproute2` 包的一部分，常被用作旧版 `netstat` 命令的替代品。

**示例：**

- 1. **显示所有套接字**

```bash
ss
```

此命令显示系统上所有套接字的列表。

- 2. **显示正在监听的套接字**

```bash
ss -l
```

显示所有正在监听的套接字。

- 3. **显示已建立的连接**

```bash
ss -a -e
```

此命令显示所有已建立的连接，包括传入和传出连接。

- 4. **显示 TCP 套接字**

```bash
ss -t
```

仅显示 TCP 套接字。

- 5. **显示 UDP 套接字**

```bash
ss -u
```

仅显示 UDP 套接字。

- 6. **显示 Unix 域套接字**

```bash
ss -X
```

仅显示 Unix 域套接字。

- 7. **显示摘要统计**

```bash
ss -s
```

显示每个协议的摘要统计信息。

- 8. **显示与套接字关联的进程**

```bash
ss -p
```

显示每个套接字的进程信息。

- 9. **按端口过滤**

```bash
ss -t -a 'sport = :80'
```

仅显示源端口为 80 的 TCP 套接字。

- 10. **显示套接字详情**

```bash
ss -t -i
```

显示扩展的套接字信息。

- 11. **显示定时器**

```bash
ss -o
```

显示套接字定时器。

- 12. **显示更多信息**

```bash
ss -t -i -o -e
```

显示有关 TCP 套接字的详细信息。

## 96. renice: 更改运行中进程的优先级

Linux 中的 `renice` 命令用于更改运行中进程的调度优先级。此命令允许您更改进程的 nice 值，该值决定了其在系统调度器中的优先级。nice 值的范围从 -20 到 19，数值越低表示优先级越高。

**示例：**

- 1. **通过 ID 更改特定进程的优先级**

```bash
renice 10 -p 1234
```

此命令将 ID 为 1234 的进程的优先级增加到 nice 值 10。

- 2. **更改进程组的优先级**

```bash
renice -5 -g 5678
```

此命令将 ID 为 5678 的进程组中所有进程的优先级降低到 nice 值 -5。

- 3. **更改由用户拥有的所有进程的优先级**

```bash
renice 3 -u username
```

此命令将用户 "`username`" 拥有的所有进程的优先级提高到 nice 值 3。

- 4. **查看进程当前优先级**

```bash
renice -p 5678
```

此命令显示 ID 为 5678 的进程的当前优先级。

## 97. sync: 将缓存写入同步到持久存储

Linux 中的 `sync` 命令用于确保文件系统的所有待处理更改写入磁盘。它有助于同步系统内存中的数据与磁盘上的数据，从而在意外关机或断电的情况下降低数据丢失的风险。`sync` 命令不会直接刷新文件系统缓冲区，而是安排它们在最早的机会进行刷新。

**示例：**

- 1. **基本用法**

```bash
sync
```

仅使用该命令即可同步所有文件系统缓冲区。

- 2. **使用文件描述符**

```bash
sync; echo 3 > /proc/sys/vm/drop_caches
```

此序列首先同步文件系统缓冲区，然后清除页缓存、dentries 和 inodes。

- 3. **带选项使用**

```bash
sync -f -d -v
```

- `-f`：即使文件系统处于干净状态也强制执行同步操作。
- `-d`：启用磁盘写入缓存。
- `-v`：详细模式。

- 4. **关机前同步**

```bash
sync && shutdown -h now
```

此命令同步文件系统，然后启动系统关机。

- 5. **查看同步进度**

```bash
watch -n 1 sync
```

这每秒更新一次同步状态。

## 98. tcpdump: 捕获和显示网络流量

`tcpdump` 是一个强大的命令行数据包分析器工具，允许您在 Linux 系统上捕获和显示网络流量。它广泛用于网络故障排除、分析和安全审计。

**示例：**

- 1. **捕获特定接口上的所有数据包**

```bash
tcpdump -i eth0
```

此命令捕获 `eth0` 接口上的所有数据包。

- 2. **捕获具有特定源或目标 IP 地址的数据包**

```bash
tcpdump host 192.168.1.2
```

这捕获 IP 地址 192.168.1.2 为源或目标的数据包。

- 3. **捕获特定端口上的数据包**

```bash
tcpdump port 80
```

这捕获端口 80 上的数据包。

- 4. **捕获来自特定 IP 和端口的数据包**

```bash
tcpdump src 192.168.1.2 and port 22
```

这捕获源 IP 为 192.168.1.2 且端口为 22 的数据包。

- 5. **捕获并显示数据包详细信息（详细模式）**

```bash
tcpdump -v
```

此命令提供有关每个捕获数据包的更详细信息。

- 6. **捕获特定数量的数据包**

```bash
tcpdump -c 10
```

这捕获并显示前 10 个数据包，然后退出。

- 7. **将捕获的数据包写入文件**

```bash
tcpdump -w capture.pcap
```

这将捕获的数据包写入名为 `capture.pcap` 的文件，之后可以使用 Wireshark 等工具进行分析。

- 8. **从文件读取数据包**

```bash
tcpdump -r capture.pcap
```

这从指定的 `capture.pcap` 文件中读取并显示数据包。

- 9. **仅捕获 TCP 或 UDP 数据包**

```bash
tcpdump tcp
```

或

```bash
tcpdump udp
```

这分别仅捕获 TCP 或 UDP 数据包。

- 10. **捕获具有特定协议的数据包**

```bash
tcpdump icmp
```

这仅捕获 ICMP（ping）数据包。

- 11. **捕获非详细输出**

```bash
tcpdump -q
```

这提供更少细节的安静输出。

## 99. time: 测量程序执行时间

Linux 中的 `time` 命令是一个实用工具，提供有关命令或脚本所使用的资源的信息。它通常用于测量进程的执行时间并分析其性能。`time` 命令可以跟踪总耗时、用户 CPU 时间和系统 CPU 时间。

**示例：**

- 1. **基本用法**

```bash
time ls
```

此示例将测量执行 `ls` 命令所需的时间。

- 2. **显示更详细的信息**

```bash
time -v ls
```

`-v` 选项提供更多信息，包括 CPU 使用情况、系统和用户时间。

- 3. **重定向输出**

```bash
time -o output.txt ls
```

您可以使用 `-o` 选项将输出重定向到文件。

- 4. **计时管道**

```bash
time (command1 | command2)
```

您也可以通过将命令括在括号中来对命令管道进行计时。

- 5. **计时脚本**

```bash
time ./myscript.sh
```

你可以使用 `time` 命令来测量 shell 脚本的执行时间。

## 100. sort：对文本文件的行进行排序。



# Linux 中的 `sort` 命令是一个强大的实用工具，用于对文本文件或输入流的行进行排序。它是一个多功能工具，允许你根据各种标准将数据按升序或降序排列。

## 示例

### 1. 按升序对文本文件进行排序

```
sort filename.txt
```

该命令将 `filename.txt` 的内容按升序排序，并在终端上显示结果。

### 2. 按降序对文本文件进行排序

```
sort -r filename.txt
```

`-r` 选项用于按降序对数据进行排序。

### 3. 排序并将输出重定向到新文件

```
sort input.txt > output.txt
```

该命令读取 `input.txt` 的内容，对其进行排序，然后将结果保存在 `output.txt` 中。

### 4. 对数值数据进行排序

```
sort -n numbers.txt
```

如果你有一个包含数值的文件，可以使用 `-n` 选项按数值进行排序。

### 5. 指定自定义分隔符

```
sort -t'!' -k2,2 file.csv
```

如果你正在处理字段由特定分隔符分隔的文件（例如，使用“;”作为分隔符的 CSV 文件），可以使用 `-t` 选项指定分隔符，并使用 `-k` 选项指示用于排序的关键字段。

### 6. 忽略前导空白

```
sort -b data.txt
```

`-b` 选项用于在排序时忽略前导空格（空白字符）。

### 7. 唯一排序

```
sort -u names.txt
```

`-u` 选项确保排序后仅显示唯一的行。当你想要消除重复条目时，这将非常有用。

### 8. 合并已排序的文件

```
sort -m sorted1.txt sorted2.txt
```

`-m` 选项用于合并两个或更多预先排序好的文件。

### 9. 按月份名称排序

```
sort -M months.txt
```

如果你有一个包含月份名称的文件，可以使用 `-M` 选项按日历顺序对它们进行排序。

### 10. 人类可读的排序

```
ls -lh | sort -k5,5
```

在此示例中，`ls -lh` 命令列出具有人类可读大小的文件，而 `sort -k5,5` 则基于第五列（大小）对其进行排序。
