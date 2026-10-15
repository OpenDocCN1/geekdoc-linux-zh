
你可能想要在用户进入目录时显示 `.message` 文件中的文本，可以如下使用 `dirmessage_enable` 选项：

```
dirmessage_enable=YES
```

由于，出于安全考虑，你不应该为此目的使用 root 登录或其他管理登录。

# 添加消息文件

尽管 FTPpd 不支持像 WU-FTP 等 FTP 服务器那样对 README 和欢迎文件的安排，但你可以在 vsFTPpd 服务器上的任何可访问目录中添加 `.message` 文件。然后，如果你如下所示使用 `dirmessage_enable` 选项，当用户进入该目录时，`.message` 文件中的文本将显示出来：

```
dirmessage_enable=YES
```
