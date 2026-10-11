
`mimencode` 比 `uuencode` 更可靠。

- `-q` 使用指定的引用打印字符编码而非 `base64`。
- `-u` 解码标准输入而非编码。

## 命令

- `-p` 在解码期间将解码后的回车/换行符序列转换为本地的换行符约定
- `-o` 文件 将输出发送到指定的文件而非标准输出。

## rmail user...

`rmail` 解释通过 `uecp` 接收的入站邮件。它将 `From` 行合并为格式为 "`return-path!finder`" 的单行，并将处理后的邮件传递给 `sendmail`。

## rwall host [文件]

`rwall` 命令向登录到指定主机的所有用户发送消息。默认情况下，消息来自标准输入，但如果指定了文件，则将使用该文件。

示例：将文件 `go.away` 中的消息发送给当前登录到主机 `local.net` 的所有用户：

```
rwall local.net go.away
```

## sendmail [标志] [地址...]

## newaliases

`mailq [-v]` `Sendmail` 负责将消息传递给预期的接收者。它根据需要跨网络传输消息。它并非设计用于与最终用户接触；其他程序（`mail`, `elm`）处理邮件过程的该阶段。

示例：以详细模式作为前台守护进程调用 `sendmail`：

```bash
sendmail -bD -v
```
