
在这里，Tripwire 会要求你输入口令：

`Please enter your site passphrase:`

接下来发生什么取决于你的系统配置。如果你没有清理策略文件中的错误路径，可能会看到一些错误，如下：

- `# Error 101: Unable to get object type: file:/usr/lib/tclX8.0.3/help`
  `No such file or directory`
- `# Error 101: Unable to get object type: file:/usr/lib/tclX8.0.3/help`
  `No such file or directory`

- `LOCALKEYFILE`：（这是针对极度多疑者的安全措施，他们担心当口令在内存中时，攻击者可以捕获它。）
- `LOOSEDDIRECTORYCHECKING`：（`LOOSEDDIRECTORYCHECKING`变量影响 Tripwire 报告目录的方式。）
- `MAILPROGRAM`：（`MAILPROGRAM`存储你指定的邮件程序位置（以及任何传递给它的命令行选项。）
- `POLFILE`：（`POLFILE`变量指向你的策略文件位置（通常为`/usr/TSS/policy/tw.pol`。）
- `REPORTFILE`：（`REPORTFILE`变量指向 Tripwire 存储报告的位置。）
- `SITEKEYFILE`：（`SITEKEYFILE`变量指向你的站点密钥。）
- `ROOT`：（根据上下文可知。）
- `LATEPROMPTING`：（这是针对极度多疑者的安全措施，他们担心当口令在内存中时，攻击者可以捕获它。）
- `DBFILE`：（`DBFILE`变量指向你的数据库文件位置。（这是存储操作系统快的文件。）
- `EDITOR`：（`EDITOR`变量存储你偏好的编辑器的位置。（注意：你必须定义此变量以在交互式编辑模式下 Tripwire。此外，如果你指定了此值，之后将无法通过操作 shell 环境变量手动更改它。）

- `# Error 101: Unable to get object type: file:/usr/lib/tclX8.0.3/help`
  `No such file or directory`
- `# Error 101: Unable to get object type: file:/usr/lib/tclX8.0.3/help`
  `No such file or directory`
- `# Error 101: Unable to get object type: file:/usr/lib/tclX8.0.3/help`
  `No such file or directory`
- `# Error 101: Unable to get object type: file:/usr/lib/tclX8.0.3/help`
  `No such file or directory`
- `# Error 101: Unable to get object type: file:/usr/lib/tclX8.0.3/help`
  `No such file or directory`

- `LATEKEYFILE`：（根据上下文可知。）
- 在第一次运行 Tripwire 之前，根据你的喜好更改这些值。
- 随后，`twadmin`会要求你输入口令：

`Please enter your site passphrase:`

验证口令后，`twadmin`将格式化配置文件并退出：

`Writing config file: /usr/TSS/bin/tw.cfg`

`Wrote configuration file: /usr/TSS/bin/tw.cfg`

接下来，你必须更新策略文件，如下所示：

```
..twadmin --create-polfile ../policy/twpol.txt
```

随后，`twadmin`会再次要求你输入口令：

`Please enter your site passphrase:`

验证口令后，`twadmin`将写入新的策略文件并退出：

`Wrote policy file: /usr/TSS/policy/tw.pol`

现在你已准备好生成 Tripwire 数据库。执行以下命令：

```
[root@linux9 bin#] /.tripwire --init
```
