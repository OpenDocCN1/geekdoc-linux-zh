
应用程序 "`/home/billy/index`" 返回了：

对 billy. 你不允许运行 dosemu. 联系系统管理员

![](img/c48ad0dbc61332ca39f773da7141f4e1_239_1.png)

## 打开用户配置文件

在终端命令行，作为 root 用户使用 pico 编辑器打开 dosemu 配置文件（输入 `su pico -w /etc/dosemu.users`）。按回车编辑文件。

```
vi /etc/dosemu.users
```

这是一个 `/etc/dosemu.users` 示例文件

Billy 用于普通用户 !!!

如果你不允许运行 DOSEMU，是不安全的

`at = /etc/dosemu.users`

`[ config ] [ class { ... }]`

登录用户名

注释一个配置变量是

将值设置为使用

以 "c" 开头的变量类定义

- 更多详情请看此处

`root`

`password`

root 允许执行一切

`root = /etc/dosemu.users`

- 只允许运行 dosemu

`guest`

`password`

如果你想允许所有用户使用 dosemu，请使用以下行

将密码字段替换为 *
