
### 10.4 使用 PAM 进行用户身份验证

任何提供用户某种权限的程序都需要能够验证用户身份。当您登录系统时，您会提供用户名和密码，登录过程使用这些信息验证登录——以确认您确实是您所声称的那个人。除了密码之外，还有其他形式的身份验证方式，并且密码的存储方式也可以是多种多样的。

PAM 是“可插拔身份验证模块”（Pluggable Authentication Modules）的缩写，它是一种允许系统管理员在无需重新编译执行身份验证的程序的情况下设置身份验证策略的方法。使用 PAM，您可以通过编辑配置文件来控制模块如何插入到程序中。

大多数 Red Hat Linux 用户可能永远不需要触碰这个配置文件。当使用 RPM 安装需要执行身份验证的程序时，它们会自动进行必要的更改，以执行常规的密码身份验证。然而，您可能希望自定义您的配置，在这种情况下，您需要理解该配置文件。

#### 10.4.1 模块

PAM 标准定义了四种类型的模块。auth 模块提供实际的身份验证，可能涉及请求并检查密码，并设置“凭证”，如组成员身份或 Kerberos“票据”。account 模块检查以确保允许进行身份验证（例如，账户未过期，用户允许在此时段登录等）。password 模块用于设置密码。session 模块在用户完成身份验证后使用，使其能够使用其账户，例如挂载用户的家目录或使其邮箱可用。

这些模块可以*堆叠*使用，即使用多个模块。例如，login 通常使用至少两种身份验证方法：如果“rhopts”身份验证成功，则足以允许连接；如果失败，则执行标准的密码身份验证。

可以随时添加新模块，并且支持 PAM 的应用程序随后可以配置为使用这些模块。例如，如果您有一个一次性密码计算器系统，并且可以编写一个支持它的模块（编写模块的文档随系统附带）。支持 PAM 的程序可以使用新模块并与新的一次性密码计算器配合工作，而无需重新编译或以其他任何方式进行修改。

#### 10.4.2 服务

每个使用 PAM 的程序都定义其自己的“服务”名称。login 程序定义服务类型 `login`，ftpd 定义服务类型 `ftp`，等等。通常，服务类型是用于**提供**服务的程序的名称，而不是（如果有区别的话）用于**访问**服务的程序的名称。

#### 10.4.3 配置文件

目录 `/etc/pam.d` 用于配置所有 PAM 应用程序。（在较早的 PAM 版本中，这曾经是 `/etc/pam.conf`；虽然如果没有找到 /etc/pam.d/ 条目，仍会读取 pam.conf 文件，但其使用已弃用。）每个应用程序（实际上是每个**服务**）都有自己的文件。文件看起来像这样：

```
#%PAM-1.0

auth required /lib/security/pam_securtty.so
auth required /lib/security/pam_pwd.b.so shadow nullok
auth required /lib/security/pam_nologin.so
account required /lib/security/pam_pwd.b.so
password required /lib/security/pam_cracklib.so
password required /lib/security/pam_pwb.b.so shadow nullok use_authok
session required /lib/security/pam_pwd.b.so
```

第一行是注释。任何以 `#` 字符开头的行都是注释。接下来的三行堆叠了三个模块用于登录授权。第一行确保如果用户试图以 root 身份登录，则其登录所在的 tty 必须列在 `/etc/securtty` 文件中*如果*该文件存在。第二行导致向用户询问密码并检查该密码。第三行检查文件 `/etc/nologin` 是否存在，如果存在，则显示文件内容，如果用户不是 root，则不允许其登录。

请注意，即使第一个模块失败，所有三个模块都会进行检查。这是一个安全决策——其设计目的是不让用户知道其身份验证失败的原因。

第四行确保账户有效。

第五行执行必要的记账。例如，如果已启用影子密码，pam_pwd.so 模块将检查账户是否已过期，或者用户是否尚未更改其密码且更改密码的宽限期已过。

第六行指定如果登录程序更改用户密码，应使用 pam_pwd.so 模块来执行此操作。（仅当 auth 模块确定需要更改密码时才会这样做——例如，如果影子密码已过期。）

最后一行指定应使用 pam_pwd.so 模块来管理会话。目前，该模块不执行任何操作；它可以用任何必要的模块替换（或通过堆叠补充）。

请注意，每个文件内行的顺序很重要。虽然 required 模块调用的顺序并不太重要，但还有其他可用的控制标志。虽然 optional 很少使用，并且在 Red Hat Linux 系统上默认从不使用，但 sufficient 和 requisite 使得顺序变得重要。

让我们来看看 rlogin 的 auth 配置：

```
auth    required    /lib/security/pam_security.so
auth    sufficient  /lib/security/pam_rhosts_auth.so
auth    required    /lib/security/pam_pwd.so shadow nullok
auth    required    /lib/security/pam_nologin.so
```

这看起来几乎像登录条目，但多了一行指定额外的模块，并且模块的指定顺序不同。

首先，pam_security.so 阻止 root 在不安全的终端上登录。这实际上禁止了所有 root 登录尝试。如果您希望允许它们（在这种情况下，我们建议不要连接互联网或处于良好的防火墙之后），您可以简单地删除该行。

其次，pam_nologin.so 如上文所述检查 /etc/nologin。

第三，如果 `pam_rhosts_auth.so` 验证了用户，PAM 会立即向 `rlogin` 返回成功，而无需进行任何密码检查。如果 `pam_rhosts_auth.so` 未能验证用户，则该失败的验证将被忽略。

最后（如果 `pam_rhosts_auth.so` 未能验证用户），`pam_pwdb.so` 模块执行常规的密码身份验证。

请注意，如果您不希望当 `security` 检查失败时提示输入密码，可以将 `pam_security.so` 模块从 `required` 更改为 `requisite`。

#### 10.4.4 影子密码

默认的 `pam_pwdb.so` 模块支持影子密码。为了将您的系统转换为影子密码，请使用以下命令：

```
cd /etc
pwconv
chmod 600 passwd- shadow-
```

`pam_pwdb.so` 模块会自动检测到您正在使用影子密码，并进行所有必要的调整。

#### 10.4.5 更多信息

这只是关于 PAM 的介绍。更多随系统附带在 `/usr/doc/pam*` 中，包括*系统管理员指南*、*模块编写人员手册*、*应用程序开发人员手册*以及 PAM 标准 DCE-RFC §6.0。此外，文档可从 Red Hat 网站获取，地址为 `http://www.redhat.com/linux-info/pam/`。

## 10.5 启动过程、Init 和关机

### 10.5.1 System V Init

本节简要介绍了启动过程的内部工作原理。它详细说明了机器如何使用 SysV Init 启动，以及它与旧版 Linux 发行版中使用的原始 init 之间的区别。

Init 是在启动时由内核运行的程序。它负责启动启动时需要运行的所有常规进程。这些包括允许您登录的 getty、NFS 守护进程、FTP 守护进程，以及您希望在机器启动时运行的任何其他内容。

SysV Init 正在迅速成为 Linux 世界中控制启动时软件启动的标准。这是因为它比传统的 BSD init 更容易使用，并且功能更强大、更灵活。

SysV init 与 BSD init 的另一区别在于，其配置文件位于 /etc 的子目录中，而不是直接位于 /etc 中。该目录称为 **rc.d**。在其中，您将找到 **rc.sysinit** 以及以下目录：

- init.d
- rc0.d
- rc1.d
- rc2.d
- rc3.d
- rc4.d
- rc5.d
- rc6.d

**init.d** 包含大量脚本。基本上，您需要为每个可能需要在启动时或进入另一个运行级别时启动的服务编写一个脚本。服务包括网络、nfs、sendmail、httpd 等。服务不包括像 setserial 这样必须仅运行一次然后退出的项目。这类项目应该放在 **rc.local** 或 **rc.serial** 中。

如果您希望使用 **rc.local**，它应该位于 /etc/rc.d 中。大多数系统都包含一个，尽管它没有做太多事情。如果您需要在启动时执行特定于串口的操作，也可以在 /etc/rc.d 中包含 rc.serial。

事件链如下：

