

## 基于角色的账户与商业 Unix

如前所述，某些 Unix 操作系统修改了现有的操作系统基础设施，为基于角色的账户提供了扩展功能。Solaris 就是一个示例，它使用 `su(1M)` 程序允许切换到角色账户。Solaris 还使用 `roleadd(1M)`、`rolemod(1M)` 和 `rolelet(1M)` 程序来操作本地系统角色。`roleadd` 程序用于添加新角色，`rolemod` 程序修改现有条目。`rolelet` 程序用于删除之前录入的角色。在 Solaris 上，`smrole(1M)` 命令用于通过名称服务（如 NIS/NIS+ 或 LDAP）处理的角色。

关于 Solaris 中基于角色的访问控制的更多详细信息，请参考《Solaris 9 12/02 系统管理员安全集》中的《系统管理员指南：安全》章节，地址为 http://docs.sun.com/db/doc/816-4883。由 Alex Noodergaert 和 Keith Watson 编写的《Solaris Operating Environment Security》（位于 www.sun.com/solutions/blueprints/1202/816-5242.pdf）也提供了基于角色的访问控制配置的良好文档。

其他 Unix 操作系统如 AIX 和 HP-UX 也提供了此功能，尽管其语义略有不同。例如，AIX 使用 `mkrole` 命令创建角色，`chrole` 命令更改角色属性，`isrole` 命令列出角色信息，以及 `rmrole` 命令删除角色。HP-UX 的基于角色的账户通过服务控制管理器（Service Control Manager）软件包进行处理。

## 基于角色的账户与 Linux

目前，唯一默认支持基于角色的访问控制的 Linux 是 NSA 安全增强型 Linux（NSA SELux）。NSA SELux 是由美国国家安全局（NSA）启动的一个项目，产生了一系列补丁，这些补丁可以应用于 Linux 系统以提供额外的安全功能。该项目的主要特性之一是集成基于角色的账户。NSA SELux 还包含其他功能，例如强制访问控制策略，这些策略限制了授予任何单个进程的权限，从而防止在服务被破坏时系统完整性受到损害。关于 NSA SELux 的更多信息可以访问 www.nsa.gov/selux。

Linux 系统还可以提供基于规则集的访问控制（RSBAC）包，它提供了基于角色的计费功能。该包是基于角色的账户的基础实现，仅提供基于角色的账户功能。RSBAC 项目位于 www.rbac.org。

## 审计

审计是从不同的系统事件中收集数据的过程，例如登录、进程执行、文件属性或参数的更改以及与权限相关的操作。记录后，审计数据可用于识别尝试性攻击或其他对系统的或其他滥用。审计数据通常以二进制信息的形式存储，并需要一组工具来进行记录和审查。

## 商业 Unix 中的审计

Solaris 通过基础安全模块（BSM）执行系统审计。BSM 能够执行的审计级别是可配置的。使用 `bsmonrun(1M)` 命令启用 BSM，使用 `bsmonun(1M)` 命令禁用。`audit(1)` 命令用于控制审计进程的行为，`auditconfig(1)` 命令用于更改审计配置。BSM 是一个相对复杂的结构，具有许多实用程序和配置文件。Solaris 提供的审计级别在系统资源方面是昂贵的，因此应该注意，审计得越频繁，开销越大。关于 Solaris 基础安全模块的更多信息可以从《Solaris 9 12/0 系统管理员集》中的《系统管理员指南：安全服务》章节获取，地址为 http://docs.sun.com/db/doc/816-4883，也可以从 Darren J. Moffat 编写的《Solaris BSM Auditing》（http://online.securityfocus.com/infocus/1362）获取。

HP-UX 启用了一些审计功能。可以通过 SAM 接口控制审计。偏好命令行界面的用户使用 `audys(1M)` 启动和停止审计，`audus(1M)` 选择要审计的对象，`audevent(1M)` 更改或显示事件信息，`audit(1M)` 更改审计文件大小和参数，以及 `audisp(1M)` 查看审计记录。关于 HP-UX 审计的更多信息可以从 HP 技术文档的审计章节收集，地址为 http://docs.hp.com/cgi-bin/onlinedocs.py?conf=false&mpn=B2355-90672&service=hpux-path=../B2355-90672/00/01/124。

AIX 也包含审计功能。审计进程由 `aud(8dex)` 命令控制。使用 `audevent(8dex)` 命令查看审计事件列表。`audfilter(8dex)` 用于操作主机上的审计文件，`audtrail(8dex)` 用于读取审计轨迹。IBM 在 AIX 的 DCE 页面提供了更多信息，地址为 www-3.ibm.com/software/network/publications。

## Linux 中的审计

大多数默认实现中的 Linux 并没有内置低级审计设施。以前，如果存在空白，由黑客应急团队维护的 auditd 守护进程填补。然而，该工具的维护似乎已经停止。

## 不可执行栈与商业 Unix

Solaris 允许通过在 /etc/system 中添加参数 `noexec_user_stack=1` 设置不可执行栈。应该注意，添加到 /etc/system 只影响之后创建的进程。因此，应该重启系统以确保进程受到此设置的影响。关于此内核参数和其他参数的更多信息可以从 Ido Dubrawsky 编写的《Solaris Kernel Tuning For Security》（http://online.securityfocus.com/infocus/1385）获取，也可以从 ordergaard 和 Keith Watson 编写的《Solaris Operating Environment Network Settings》（http://www.sun.com/solutions/blueprints/1299/network.pdf）获取。

HP-UX 在 11i 及更高版本也提供了不可执行栈。可以通过将内核参数 `executable_stack` 设置为 0 来启用不可执行栈。可能存在其他对系统安全有影响的参数。关于 HP-UX 中不可执行栈和内核参数的更多信息可以通过《HP-11i Release Notes》中的《Execute Protected Stacks》获取，地址为 http://docs.hp.com/cgi-bin/linedocs.py?toc=false&mn=B2355-90672&service=hpux-path=../B2355-90672/00/01/124关于 IBM AIX 和可调内核参数的信息可以通过 IBM 性能管理指南中的《Tunable Parameters》获取，地址为 http://pub16.boulder.ibm.com/pseries/en_US/aixman/pftungngl/23654.htm。

