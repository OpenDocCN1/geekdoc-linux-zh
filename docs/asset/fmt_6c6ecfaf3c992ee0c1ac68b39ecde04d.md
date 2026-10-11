
在此例中，`dig` 输出与给定 IP 地址对应的主机名为 rumored.com。

[<] [>] [<<] [Up] [>>] [Top] [Contents] [Index] [?]

## 33.4.6 列出域名所有者

互联网域名的域名记录包含了注册该域名的组织或个体的联系信息。我们使用 `whos` 命令来查看 `.com`、`.org`、`.net` 和 `.edu` 顶级域名的记录。

仅将域名作为参数，`whos` 会输出拥有该特定域名记录的“Whois 服务器”名称。若要输出域名记录，请通过 `-h` 选项参数指定要使用的 Whois 服务器。

- 若要输出 `linart.net` 的 Whois 服务器名称，输入：

```
$ whos linart.net RET
```

- 若要使用 `whos.networkolutions.com` Whois 服务器查看 `linart.net` 的域名记录，输入：

```
$ whos -h whos.networkolutions.com linart.net RET
```

注意：此命令还会输出处理给定域名的服务器名称——这有助于了解网站托管在何处。

## 33.5 向另一个用户的终端发送消息

使用 `write` 向另一个用户的终端写入消息。将你想要写入的用户名作为参数。此命令写入你提供的消息，并在前面带有一个行头，指示后续是来自你的消息，并给出当前系统时间。它还会在用户的终端上响铃。

- 若要向登录了用户 `sleep` 的终端发送 `Wake up!` 消息，输入：

```
$ write sleepy RET

Wake up!

C-d

$
```

另一个用户可以通过运行 `write` 并提供你的用户名作为参数来向你回复。传统上，用户在消息后输入 `~o'`，这表示他们的话“结束（over）”，现在轮到另一个人说话了。认为对话已完成的用户，会在行尾输入 `~oo'`，意味着他们“结束（over）并离开（out）”。

类似的命令 `wall` 可向本地系统上的所有其他用户写入消息。它接受文本文件作为参数并输出该文件的内容；如果不带参数，它将输出你单独输入 `C-d` 的内容。它消息前带有“广播消息，来自用户名”（其中用户名是你的用户名），随后是当前系统时间，并在它广播的所有终端上响铃。

- 若要将 `/etc/motd/` 的内容输出到所有登录终端，输入：

```
$ wall /etc/motd RET
```

- 若要将文本‘Who wants to go out for Chinese food?’ 输出到所有登录终端，输入：

```
$ wall RET

Who wants to go out for Chinese food? RET

C-d
```
