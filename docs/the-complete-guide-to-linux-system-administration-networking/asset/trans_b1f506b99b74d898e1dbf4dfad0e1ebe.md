
- **auth:** 身份验证模块用于识别用户，通常通过提示密码来完成。
- **account:** 这些模块在身份验证模块确认用户身份后管理用户的账户，通常用于限制访问权限，例如仅在特定时间段内允许访问。
- **session:** 这些模块管理用户的当前会话，通常处理在用户被允许工作前必须完成的任务，例如创建日志文件或挂载用户需要的文件系统。
- **password:** 这些模块在用户需要更改密码（或其他身份验证凭证）时执行。

![](img/43f64015de86d989e30eff5bb284fb96_531_0.png)

完整的 PAM 文档及各个模块的详细说明位于 /usr/share/doc/pam-0.77（在 Red Hat Linux 和 Fedora 中）。

当执行一个 PAM 兼容程序（如 login 或 passwd）时，它会检查为该任务配置了哪些适用的模块。例如，当用户首次登录时，login 会将控制权交给 PAM，PAM 必须按顺序运行所有列为 auth 模块的模块（如上例中的第 2、3、4 行）。当同一类型的模块有多个时，它们被视为“堆叠”（stacked）。除非 control_flag 指示 otherwise，PAM 按顺序执行堆叠中列出的所有模块，并根据各模块的结果返回 Access Permitted（准入允许）或 Access Denied（准入拒绝）。control_flag 元素决定了如何处理堆叠中的模块。它有两种形式：

- **required:** 模块必须成功才能使最终结果为 Access Permitted。由于后续模块也会被执行，用户无法判断是哪个模块失败，但只要有任何 required 模块失败，最终结果即为 Access Denied。
- **requisite:** 模块必须成功才能使最终结果为 Access Permitted。如果 requisite 模块失败，后续模块不会被执行；如果 requisite 模块成功，后续模块也会被执行。
- **sufficient:** 即使该模块失败，最终结果仍可能为 Access Permitted；但如果该模块成功，则已足够获得 Access Permitted。如果 sufficient 模块成功，则不会执行其他模块；如果在堆叠中之前的 required 模块未失败，PAM 会立即返回 Access Permitted。如果 sufficient 模块失败，后续模块仍会被执行，且对 previous 结果不作考虑。
- **optional:** 可选模块的结果不影响模块堆叠的最终结果。可选模块用于执行与访问控制无关的任务（如记录日志），对系统管理或用户需求有帮助。

除了上述四种形式，control_flag 还可以采用更复杂的语法：可以在 test=action 的形式中包含一组或多组指令（用空格分隔），其中 test 是 30 种代码之一（如 user_unknown、acct_expired），action 可以是 ignore、done、bad 等六种代码，或是一个数字，表示在当前堆叠中跳过多少后续模块。此语法可用于创建更复杂的模块堆叠并根据前序模块结果控制执行顺序。默认配置文件中大多数系统并未启用此高级语法，但可在 PAM 文档中查阅详细说明。

PAM 配置文件的最后两个元素是 module_path 和 arguments。module_path 是要执行的完整路径及模块名称。arguments 是在执行该模块时传递给它的信息。第 2、4、9 行是不带参数的示例；除第 1 行（注释）外，其他行（如 pam_stack）均有一个参数 service=system-auth。

pam_stack 模块是一种特殊的“包含”模块。pam_stack 后的 service 表示另一个位于 /etc/pam.d 的配置文件，该文件中的所有模块在此点被执行。例如，下面的几行来自登录配置文件（行号仅作示例，非文件本身内容）：

```
2 auth required /lib/security/pam_securetty.so
3 auth required /lib/security/pam_stack.so service=system-auth
4 auth required /lib/security/pam_nologin.so
```

/etc/pam.d/system-auth 包含由 authconfig 自动生成的模块配置行，依据所选安全措施：

```
auth required /lib/security/$ISA/pam_env.so
auth sufficient /lib/security/$ISA/pam_unix.so likeauth nullok
auth required /lib/security/$ISA/pam_deny.so

account sufficient /lib/security/$ISA/pam_succeed_if.so uid < 100
account required /lib/security/$ISA/pam_unix.so

password requisite /lib/security/$ISA/pam_cracklib.so retry=3
password sufficient /lib/security/$ISA/pam_unix.so nullok use_authtok md5 shadow
password required /lib/security/$ISA/pam_deny.so

session required /lib/security/$ISA/pam_limits.so
session required /lib/security/$ISA/pam_unix.so
```

基于这两个文件，login 命令在登录过程中会按以下顺序执行这些模块（auth 堆叠）：

- pam_securetty.so（来自 /etc/pam.d/login）
- pam_stack.so（来自 /etc/pam.d/login——该模块仅启动后续三个模块）
- pam_env.so（来自 /etc/pam.d/system-auth）
- pam_unix.so（来自 /etc/pam.d/system-auth）
- pam_deny.so（来自 /etc/pam.d/system-auth）
- pam_nologin.so（来自 /etc/pam.d/login）

/usr/share/doc/pam-0.77/html/pam-6.html（在 Red Hat Linux 或 Fedora 中）提供每个模块的参考信息，包括示例和所有受支持参数的描述。这些描述会根据模块支持的四种类型（auth、account、session、passwd）给出特定信息。例如，pam_unix 可以用于 auth、account、session 或 passwd。

![](img/43f64015de86d989e30eff5bb284fb96_533_0.png)

> 尽管您需要查阅 PAM 文档以了解每个模块的工作原理和可用选项，但阅读示例配置文件和最常用模块有助于理解如何根据自身网络需求配置 PAM。请注意，PAM 配置可能相当复杂，配置不当的系统可能会以意想不到的方式允许或阻止访问。学习 PAM 时，建议逐行修改配置文件，并在每次更改后测试结果，以观察变化。

下面给出 halt 命令的示例 PAM 配置文件：/etc/pam.d/halt。（已删除注释行。）此命令用于关闭所有 Linux 服务，以便安全地切断电源。

![](img/43f64015de86d989e30eff5bb284fb96_533_1.png)

> 当您按下 Ctrl+Alt+Del 来重启或关闭 Linux 系统时，init 程序会执行重启命令。通常会执行 shutdown 命令（可在 /etc/inittab 配置文件中看到）。您也可以在命令行使用 halt 或 reboot 命令来关闭或重启系统。

```
# $PAM-1.0
auth    sufficient    pam_rootok.so
auth    required      pam_console.so
#auth   required      pam_stack.so service=system-auth
account required      pam_permit.so
```

halt 命令的 auth 堆叠包含 rootok 和 console 两个模块，工作方式如下：

1. rootok 模块检查执行 halt 命令的用户是否为 root（通常通过检查用户 ID 是否为 0 实现）。如果是，PAM 认为条件已满足，直接返回 Access Permitted，因此 root 可以执行 halt。
2. 如果用户不是 root，console 模块检查用户是否在本地控制台（而非通过网络或调制器等远程连接登录）。如果用户在控制台，则可以执行 halt；否则 PAM 拒绝访问，命令不会执行。

假设您允许其他用户在控制台操作，但不让他们以 root 身份登录。您不希望他们运行 halt 命令。由于 PAM 的默认行为是如果没有模块明确允许访问则拒绝，您可以通过删除或注释掉上述示例文件中的第二行来实现只允许 root 运行 halt。这样一来，如果 rootok 模块失败（因为用户不是 root），halt 命令将无法执行，后续检查也不会进行。

## 使用网络信息服务（NIS）

网络信息服务（NIS）是一个让系统管理员为多个 Linux（或 UNIX）服务器管理单一配置文件集的程序。例如，如果您有 10 台 Linux 服务器，每台服务器为 25 名用户提供文件和打印服务，通常需要在每台服务器上独立管理用户账户。如果有用户需要在其他服务器上获得访问权限，则必须在额外服务器上创建专门的用户账户。

通过 NIS，您可以在一个文件中管理全部 250 名用户（10 台服务器，每台 25 名用户）。该文件位于其中一台系统（NIS 服务器）上，当用户在其他任何服务器上登录时，该服务器会联系 NIS 服务器查询该用户是否拥有有效账户。

NIS 服务有时称为黄页服务（YP），在 /etc/rc.d/init.d 目录中可以看到多个支持 NIS 客户端和服务器的程序，包括 ypserv、ybind、yppasswd、ypxfrd 等。

NIS 通常以更新版本 NIS+ 或 NISplus 提供。您可以通过运行 authconfig 程序来让系统使用 NIS 服务器。该程序（如图 11-9 所示）允许您输入 NIS 域名和服务器名称。设置自己的 NIS 服务器超出本书范围，但使用 Linux 完全可以实现。

