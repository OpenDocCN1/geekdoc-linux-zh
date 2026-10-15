
# /etc/inetd.conf 更改

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

# 使用 Samba Web 管理工具 (SWAT) 进行 Samba 配置

# 第 13 章

## 高安全性设置

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

## 低安全性设置

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

## 高安全性设置

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

## 低安全性设置

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

## 在这种情况下，任何人都可以进入 SWAT 创建一个 `smb.conf`，并带有危险的 `root preexec`。

## 低安全性设置

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

## 高安全性设置

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

## 低安全性设置

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

## 高安全性设置

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

## 低安全性设置

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

## 高安全性设置

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

## 低安全性设置

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

## 高安全性设置

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

## 低安全性设置

SWAT 通过 `inetd` 启动，因此必须配置在 `/inetd.conf` 中。

## 使用 Samba Web 管理工具 (SWAT) 进行 Samba 配置

## 第 13 章

如果你已经实施了高安全性配置，请临时实施低安全性配置并查看是否有差异。如果没有差异，你已经排除了一大范围的可能。如果有差异，请利用这些差异。

确保 Samba 本身正在运行。使用 `ps -ax | grep mbd` 检查守护进程。同时，使用 `testparm` 检查 `smb.conf` 的合法性。

通常，通过命令行控制台上的 `Lynx` 访问 SWAT 可以获取更多信息。以下是一个重定向到文件的 `Lynx` 会话，其中删除了各种屏幕控制字符。请注意，它会故意在第一次请求时失败，然后在重试时请求用户名。这是正常现象。还要注意，屏幕滚动并不整齐。用户名 `Username` 和密码 `Password` 提示可能会覆盖现有文本，这与计算机死机很难区分。如果你看到用户名提示，通过输入你的用户名进行响应。当看到密码提示时，输入密码。

你可以将 `Lynx` 会话管道到日志文件，然后从另一个会话对该文件执行 `tail -f`。这是一个会话示例：

```
lynx http://127.0.0.2:901 > lynx.log
```

```
Getting http://127.0.0.2:901/

Looking up 127.0.0.2:901/

Making HTTP connection to 127.0.0.2:901.

Sending HTTP request sent; waiting for response.

Alert: Access without authorization denied -- retrying

Retrying with access authorization information.

Looking up 127.0.0.2:901.

Making HTTP connection to 127.0.0.2:901.

Username for 'SWAT' at server 127.0.0.2:901':username

Password***

Sending HTTP request.

HTTP request sent; waiting for response.

Samba Web Administration Tool (p1 of 2)

Home Globals Shares Printers Status View Config Password Management
```
