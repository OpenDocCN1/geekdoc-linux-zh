
```bash
cd /mnt/hdc4/src/john-1.6/
wget ftp://ftp.popen.com/pub/wordlists/all.gz
```

配置你的 John the Ripper 版本，告诉它你有多少个节点。默认情况下，John 假设你有两个节点。如果你的情况也是如此，请跳过此段落。要更改集群中的节点数量，你需要手动编辑 `run/` 目录下的 `john.ini` 配置文件。用文本编辑器打开该文件。在底部有一行 `total = 2;`。将数字 `2` 更改为你拥有的节点数量。

John the Ripper 编译完成、字典安装且节点数量配置完成后，安装即结束。接下来你创建一个密码，提取其哈希值，最后破解该密码。

# 运行 John

通过为 ClusterKnoppix 机器上的用户 `knoppix` 设置新密码开始破解。对于此示例，请选择一个相对简单的密码，例如 `bottle`，以确保你不会花费几个小时等待 John 偶然发现。要设置密码，运行以下命令：

```bash
sudo passwd knoppix
```

在提示时输入两次新密码。然后创建一个密码文件的未加密（unshadowed）版本。在现代 UNIX 和 Linux 系统中，`/etc/passwd` 文件实际上并不包含密码哈希值。它们存储在密码文件的影子文件中，只有 root 或 shadow 用户可以读取。为了在不以 root 运行 John 的情况下破解密码，必须创建一个包含哈希值的密码文件，以便普通用户读取。将未加密的结果存储在：

```bash
john-1.6/run/unshadow /etc/passwd /etc/shadow > /tmp/unshadow
```

这为你提供了一组可以操作的哈希，你现在可以开始破解密码了。在 `john-1.6/run/` 目录内运行以下命令：

```bash
.john-rules -external:parallel -wordfile:/.../tmp/unshadow
```
