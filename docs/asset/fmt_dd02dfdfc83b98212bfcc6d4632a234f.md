
- `winrm set winrm/config/winrs @{MaxMemoryPerShellMB="2048"}`（用于增加每个 shell 可以使用的最大内存）

## vRO

在 vRO 服务器上需要进行以下配置更改。

### Kerberos

为了让 vRO 使用 Kerberos，需要在 vRO 服务器上创建并填充 `krb5.conf` 文件。根据所使用的的 vRO 版本，该文件应存储在以下位置：

**Windows Server 2012 R2** `C:\Program Files\VMware\CIS\jre\lib\security`

**较版本的 Windows 版本** `C:\Program Files\Common Files\VMware\vCenter Server - Java Components\lib\security`

**Linux Appliance** `/usr/java/jre-vm/lib/security/`

根据列表 21.1 中的信息填充该文件。在此示例中，Windows 域名名为 `sunnydale.local`，域控制器为 `dc01.sunnydale.local`。请确保大小写匹配，因为这对解决方案的正常运行至关重要。

### 列表 21.1 krbs.conf 文件内容

```
[libdefaults]
default_realm = SUNNYDALE.LOCAL
udp_preference_limit = 1
[realms]
SUNNYDALE.LOCAL = {
 kdc = dc01.sunnydale.local
default_domain = sunnydale.local
}
[domain_realms]
sunnydale.local=SUNNYDALE.LOCAL
sunnydale.local=SUNNYDALE.LOCAL
```

文件到位后，重启 vRO 服务。

## PowerShell 插件

可以配置 vRO PowerShell 插件。在 vRO 控制台的设计工作流视图中，导航到 `Library/PowerShell/Configuration`（图 21.1）。

### 图 21.1 vRO PowerShell 主配置工作流

![](img/62596f5acc979040608a4e5111beb7d6_746_0.png)

启动 `Add A PowerShell Host` 工作流。在 PowerShell Host 选项卡上（图 21.2）填充以下文本框：

Name: `vCOPOSH`

Host / IP: `vcoposh.sunnyydale.local`

Port: `5985`

### 图 21.2 添加 PowerShell 主（PowerShell Host 选项卡）

![](img/62596f5acc979040608a4e5111beb7d6_747_0.png)

在 Host Type 上的下拉框中选择以下内容（图 21.3）：

PowerShell Remote Host Type: `WinRM`

Transport Protocol: `HTTP`

Authentication: `Kerberos`

### 图 21.3 添加 PowerShell 主（Host Type 选项卡）

![](img/62596f5acc979040608a4e5111beb7d6_748_0.png)

在 User Credentials 选项卡上，使用以下信息填写表单（图 21.4）：

Session Mode: `Shared session`

User Name: `vcosvc@sunnydale.local`（确保使用域账户）

Password: 域账户的密码

点击 `Submit`，如果一切顺利，工作流将完成（图 21.5）。

## 第 21 章 VREALIZE ORCHESTRATOR

### 图 21.4 添加 PowerShell 主（User Credentials 选项卡）

![](img/62596f5acc979040608a4e5111beb7d6_749_0.png)

### 图 21.5 成功添加 PowerShell 主

![](img/62596f5acc979040608a4e5111beb7d6_749_1.png)

## 运行外部脚本

配置好插件后，现在可以使用它可以运行存储在配置为 PowerShell 主的服务器上的脚本。让我们通过一个简单的示例来看如何操作。我们将使用一个存储在 PowerShell 主上的脚本 `Write-HelloWorld.ps1`（列表 21.2）。

### 列表 21.2 Write-HelloWorld.ps1

```
$Text = "a says Hello World!"
$Text | Out-File C:\Scripts\Test.txt -Append
```

在 vRO 客户端中，导航到 `Library/PowerShell` 并运行 `Invoke An Script` 工作流。将 host 设置为之前在 PowerShell 插件中配置的 PowerShell 主（图 21.6）。

### 图 21.6 运行外部脚本（PowerShell Host 选项卡）

![](img/62596f5acc979040608a4e5111beb7d6_750_0.png)

### 图 21.7 运行外部脚本

![](img/62596f5acc979040608a4e5111beb7d6_751_0.png)

### 图 21.8 运行外部脚本

![](img/62596f5acc979040608a4e5111beb7d6_752_0.png)

### 列表 21.5 用于 Invoke-ExternalPSSScriptReturnCode 的 vRO JavaScript 代码

```javascript
// 创建变量
var session
var sessionOutput;
var XMLReturncode = "";
var returnCode = ""

// 使用 powershell Host 会话
try {
    session = powershellHost.openSession();
    var script = '& ' + scriptPath + ' ' + arguments;

    System.log("Script is: " + script);

    // 运行脚本
    sessionOutput = session.invokeScript(script);

    // 获取结果
    results = sessionOutput.getResults();

    // 从结果获取返回代码
    if (results != null) {

        XMLReturncode = results.xml();
        returnCode = XMLReturncode.split("<I32>").pop().split("</I32>").shift();

        System.log("XMLReturnCode is: " + XMLReturncode);
        System.log("returnCode is: " + returnCode);
    }
    System.log("Script output is: " + sessionOutput.getHostOutput());
} catch (ex) {
    System.warn(ex);
} finally {
    if (session) {
        powershellHost.closeSession(session.getSessionId());
    }
}
```

## 第 21 章 VREALIZE ORCHESTRATOR

> 提示：在 vRO 工作流文件夹中创建一个 `Dev/Scratch` 文件夹是值得的，你可以在其中创建可能需要某些测试的工作流初稿。之后，可以将它们移动到更合适的文件夹。

`Invoke-ExternalPSScriptReturn` 工作流现在已可以使用 `Test-ReturnCode.ps1` PowerShell 脚本进行测试。运行工作流并提供以下输入（PowerShell 21:13）：

- 于 PowerShellHost：由 vRO PowerShell 插件创建的 PowerShell Host
- 于 scriptPath：`C:\Scripts\Test-ReturnCode.ps1`
- `-a 3`

### 图 21.13 Invoke-ExternalPSScriptReturnCode 参数

![](img/62596f5acc979040608a4e5111beb7d6_757_0.png)

在工作流日志中，你应该应该看到类似下面的输出，包含脚本的返回代码和脚本的输出：
