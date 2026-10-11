

想象以下场景。我们正在执行一项任务，试图对人力资源部（HR）发起客户端攻击。我们可以盲目地直接发起攻击，但由于我们不知道他们使用的是什么操作系统和应用，也不知道具体的版本，因此成功的可能性微乎其微。相反，我们会选择谨慎行事，提交一份格式错误的“简历”文档，该文档被设计为无法打开。我们在措辞上精心设计邮件内容，以诱导对方做出某种形式的回应。

第二天，我们收到一封邮件回复，表明人力资源部无法打开我们的文档，这并不令人惊讶。为了帮助解决问题，我们会回复（如果可能的话，最好通过电话联系），询问他们使用的具体 Microsoft Office 版本，并指出该问题可能由版本不兼容引起。这种对话可以继续深入，例如询问 Office 中可能启用的安全功能，或正在使用的操作系统版本。这种类型的对话必须保持平衡、低调，并穿插能够合理化提问的评论，例如：“这份简历使用了宏等高级功能，以使其脱颖而出并方便浏览内容。”虽然具体过程超出了本模块的范围，但这种做法被称为*虚构身份（pretexting）* [354]，并能极大地提高我们的成功率。

在我们的场景中，我们发现人力资源代表理所当然地使用了特定版本的 Microsoft Office，并且允许执行 Word 宏。获得这些信息后，我们可以制作第二份包含宏的 Word 简历文档，该宏利用 PowerShell 开启反向 shell，并将其通过邮件发送给他们。

当然，这是一个简化的成功故事。你的社会工程学虚构身份策略肯定需要更加复杂和具体，基于你预先收集的信息。

### 13.1.2.2 客户端指纹识别

客户端指纹识别 [355] 的过程对于攻击的成功至关重要，但为了获取最精确的信息，我们经常必须直接从目标机器本身收集。我们可以将这一重要的攻击阶段作为利用过程之前的独立步骤来执行，或者将指纹识别整合到利用本身的第一阶段中。

让我们假设在一个实际示例中，我们已经说服受害者访问我们的恶意网页。我们的目标将是识别受害者的网页浏览器版本以及底层操作系统的相关信息。

> 网页浏览器通常是收集目标信息的优良途径。其演化、复杂性以及功能丰富性对最终用户和攻击者而言都已是一把双刃剑。

我们可以创建自己的定制工具，但也有很多可用的开源指纹识别项目，其中最可靠的通常是那些直接利用常见客户端组件（如 JavaScript）的项目。

- [354] (Wikipedia, 2019), https://en.wikipedia.org/wiki/Social_engineering_(security)#Pretexting
- [355] (Wikipedia, 2019), https://en.wikipedia.org/wiki/Device_fingerprint

![](img/ec25e59d75726b7041242a56d3376832_415_0.png)

在此示例中，我们将使用 *Fingerprint2* JavaScript 库，该库可以通过从其 GitHub 仓库下载并解压项目归档文件来安装：

```bash
kali@kali:~/var/www/html$ sudo wget https://github.com/Valve/fingerprint2/archive/master.zip
--2019-07-24 02:42:36--  https://github.com/Valve/fingerprint2/archive/master.zip
.
2019-07-24 02:42:41 (116 KB/s) - `master.zip` saved [99698]

kali@kali:~/var/www/html$ sudo unzip master.zip
Archive:  master.zip
eb44f8f6f5a8c4c9ae476dc60d8ed1015b2b605
  creating: fingerprint2s-master/
  inflating: fingerprint2s-master/.eslintrc
.

kali@kali:~/var/www/html$ sudo mv fingerprint2s-master/ fp
```

列表 379 - 下载 Fingerprint2 库

我们可以基于项目包含的示例，将此库整合到一个 HTML 文件中。我们将在位于 Kali 网络服务器 `/var/www/html/fp` 目录下的 **fingerprint2.html** HTML 文件中包含 **fingerprint2.js** 库。

```bash
kali@kali:~/var/www/html/fp$ cat fingerprint2.html
```

```html
<!doctype html>
<html>
<head>
    <title>Fingerprint2 test</title>
</head>
<body>
<h1>Fingerprint2</h1>

<p>Your browser fingerprint: <strong id="fp"></strong></p>
<p><code id="time"></code></p>
<p><span id="details"></span></p>
<script src="fingerprint2.js"></script>
<script>
    var d1 = new Date();
    var options = {};
    Fingerprint2.get(options, function (components) {
        var values = components.map(function (component) { return component.value })
        var murmur = Fingerprint2.x64Hash128(values.join(''), 31)
        var d2 = new Date();
        var timeString = "Time to calculate the fingerprint: " + (d2 - d1) + "ms";
        var details = "<strong>Detailed information: </strong><br />";
        if(typeof window.console == "undefined") {
            for (var index in components) {
                var obj = components[index];
                var value = obj.value;
                if (value != null) {
                    var line = obj.key + " = " + value.toString().substr(0, 150);
                    details += line + "<br />";
                }
            }
        }
    }
  }
  document.querySelector("#details").innerHTML = details
  document.querySelector("#fp").textContent = murmur
  document.querySelector("#time").textContent = timeString
</script>
</body>
</html>
```

列表 380 - 使用 Fingerprintjs2 JavaScript 库

列表 380 中的 JavaScript 代码调用 Fingerprint2.get 静态函数以启动指纹识别过程。库返回的 components 变量是一个数组，包含从客户端提取的所有信息。存储在 components 数组中的值会被传递给 murmur [332] 哈希函数，以创建浏览器的哈希指纹。最后，相同的值会被提取并显示在 HTML 页面上。

上述网页（图 240）来自我们的 Windows 实验室机器，揭示了几行 JavaScript 代码提取了浏览器 User Agent 字符串、其本地化设置、已安装的浏览器插件及相对版本、关于底层 Win32 操作系统平台的一般信息以及其他详细信息。

## Fingerprintjs2

```
Your browser fingerprint: 062bc40b044b31l83b04eb42afl2526l
Time took to calculate the fingerprint: 256ms
Detailed information:
userAgent = Mozilla/5.0 (Windows NT 10.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36 Edge/16.16299
webdriver = false
language = en-US
colorDepth = 24
decisionMemory = not available
hardwareConcurrency = 1
screenResolution = 800,600
availableScreenResolution = 800,560
timezoneOffset = 420
timezone = America/Los_Angeles
sessionStorage = true
localStorage = true
indexedDB = true
addBehavior = false
openDatabase = false
cpuClass = not available
platform = Win32
plugins = Edge PDF Viewer,Portable Document Format,application/pdf,pdf
canvas = canvas windexing:yes,canvas fp:data:image/png;base64,iVBORw0KGgoAAAAANSUUhEUgAAoQAAAQDCAAYAAAAgUd08AAAAgAA9RQ612ars4c060AAAAAA0R218AAxJwv2VYUAAAA8YSU8RBVhe74
webgl = data:image/png;base64,iVBORw0KGgoAAAAASUUEIA8AAAAUQAAcYAAABMTX55SAAAAKXQRR81Rl2ars4c060AAAAQR218AAA6CxJw2VYUAAAAGYSU8RBVhe74
webGLVendorRenderer = Microsoft-Microsoft Basic Render Driver
adBlock = false
heshieledResolution = false
heshieledDo = false
heshieledBrowser = false
touchSupport = 0,false,false
fonts = Arial,Arial Black,Arial Narrow,Arial Rounded MT Bold,Book Antiqua,Bookman Old Style,Calibri,Cambria,Cambria Math,Century
audio = 124.0007979219147
```

![](img/ec25e59d75726b7041242a56d3376832_417_0.png)

```
Mozilla/5.0 (Windows NT 10.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537 Edge/16.16299
```

![](img/ec25e59d75726b7041242a56d3376832_417_1.png)

我们可以将此 User Agent 字符串提交到在线用户代理数据库，以识别浏览器版本和操作系统，如图 241 所示。

