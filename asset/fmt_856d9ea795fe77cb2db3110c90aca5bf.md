
## PAM Kerberos

如你所见，`dtaction` 和 `dtlogin` 应用程序指定了 `libpam_ntlm`。这允许我登录 CDE（见图 8–2）。一旦我登录，就可以运行 `passwd` 命令：如果我这样做，`passwd` 将在 Windows 2000 域控制器上更改我的密码。如果我想访问 Windows 2000 服务器上的共享，我不需要先运行 `cflogin` 工具，因为我已经通过 NTLM 完成了身份验证。换句话说，我的交互式登录发生在 CDE 登录屏幕；我的网络登录发生在 CDE 登录界面（图 8–2 **CDE 登录界面**）。

使用 PAM NTLM，任何登录到 HP-UX 11 系统的用户都可以通过 Windows 或 Windows 2000 服务器进行认证。PAM NTLM 是 HP CIFS/9000 Client 产品的一部分。该产品允许 HP-UX 用户通过通用文件系统 (CIFS) 协议管理 Windows 服务器上的共享，这是 Windows 服务器上 NFS 的替代方案。要访问这些共享，你必须运行 `cifslogin` 工具或使用 PAM 进行认证。PAM NTLM 使用加密密码对用户进行身份验证，并支持使用 HP-UX 的 `passwd` 命令在 Windows 2000 上更改密码。

PAM NTLM 配置文件为 `/etc/cifsclient/pam/smb.conf`。在配置 PAM 之前，你必须在此文件中设置 `workgroup` 和 `password server` 参数，以反映你的 Windows 2000 域和域控制器。例如，如果你的域名为 `BOOK` 且域控制器为 `W2KSERV`，那么你的配置文件看起来如下：
