

# 第6章 保护 Active Directory

Windows 2000 Server（任意版本）作为新系统安装时，默认情况下它将成为工作组或域的成员服务器。（如果是将 Windows NT 主域控制器 [PDC] 或备份域控制器 [BDC] 升级到 Windows 2000，处理方式有所不同。在升级 NT PDC 或 BDC 的情况下，安装程序会提示用户将域升级为 Active Directory。如果未执行此操作，以前的所有信息将会丢失。）

# Active Directory 中信息的逻辑结构

Active Directory 包含关于各种类型对象的信息。它们按照层次结构组织成更大的逻辑单元：

- 容器 (Containers)
- 域 (Domains)
- 域森林 (Forests of domains)

在接下来的章节，我们将从简单到复杂的顺序考虑这些单元。

# 对象 (Objects)

对象是 Active Directory 数据库中用户、资源或服务的表示。每个对象由一组属性（attributes）描述。每个属性都有一个对应的值。对象通常以图标的形式出现在管理控制台中，当你右键点击该对象时，可以查看其属性的值。某些对象不会显示在各种管理控制台中，因为它们的设计目的并不是为了管理。表 6.1 列出了各种对象及其相应属性和值的示例。

表 6.1 对象、属性与值之间的关系

| 对象 | 属性 | 值 |
| :--- | :--- | :--- |
| 用户 | 电子邮件地址 | myname@company.com |
| 用户 | 名字 | George |
| 节点 | 名称 | SERVER01 |
| 节点 | DNS 名称 | Server01.mycompany.com |
| 打印机 | 类型 | HP LaserJet 5si |

# 容器 (Containers)

容器是目录中的一种对象，仅包含其他对象。容器类似于文件系统中的文件夹。容器对象像文件文件夹一样包含其他容器。容器不代表任何用户、服务或资源，但它有自己的属性和值。相反，容器是使 Active Directory 塑成树状结构的关键。域和组织单元（OU）都是容器的示例。

在 Active Directory 中，容器不是安全主体（security principals）。你无法对容器应用权限，这些权限也不会通过它们向下传递。如果你希望实现相同的功能，可以将 OU 与组合并，将所有对象放在这些组中并对组进行嵌套。这需要一些规划以确保你的继承关系符合你的预期。

# 域 (Domains)

域是一组参与相同子树的 Windows 2000 计算机。Active Directory 由一个或多个域组成。根据网络设计和实现情况，每个域都可以跨越局域网（LAN）和广域网（WAN）链路。多个域可以存在于同一个局域网。当 Active Directory 中存在多个使用不同命名空间的域时，它被视为域森林。该森林必须包含共享共同架构（schema）和配置的域。它们产生用户、服务和资源的全局目录（GC）。

# 域树 (Domain Trees)

树是容器和对象的层次结构组织。嵌套容器类似于文件系统中的文件夹。每个分支的末端是表示用户、服务和资源的对象。这些对象类似于文件。

域树是一组共享共同架构的域，通过信任关系联合在一起，创建一个单一的命名空间。Active Directory 可以包含一个或多个树，可以通过它们的信任关系或命名空间来描述。

![](img/729efc56f204a2ebffb8295c3a2dfdf_271_0.png)

当 Windows 2000 Server 作为成员加入 Active Directory 域时，它可以与任何域控制器通信安全信息。域被配置为树结构中的顶层容器，该结构通过信任关系创建，并使用域名服务（DNS）。

共享相同命名空间的域被组织成域树。命名空间意味着域通过 DNS 名称链接起来。例如，名为 root.com 的域和其名为 child.com 的子域都属于同一个命名空间。然而，名为 forest.com 的域不属于该命名空间，事实上，它构成了另一个域树的基础。Active Directory 中可以存在多个具有命名空间的域，也可以存在没有命名空间的域。多个具有不同命名空间并参与同一个 Active Directory 的域通常被视为多个域树的森林，如图 6.1 所示。但请注意，一个域本身也可以是一个森林。森林中第一个创建的域是该森林的根域。

# 图 6.1 作为森林的 Active Directory

![](img/729efc56f204a2ebffb8295c3a2dfdf_272_0.png)

存在一个极其强大的管理员组，它仅存在于森林根域中。它被称为企业级管理员（Enterprise Admins）——整个 Active Directory 的核心管理组。无法将该组的任何成员锁定在其权限之外，因此仔细地向系统管理员授予这些权限至关重要。关于为什么锁定不起的详细示例将在后文的“对 Active Directory 发起攻击”章节中提供。

# 信任关系 (Trust Relationships)

信任关系是域树中的连接点。为了显示这种关系，每个域的带有箭头的逻辑结构显示了域之间的显式信任关系，以及由这些关系产生的任何隐式信任关系。

注意：传递信任（Transitive trusts）是 Windows 2000 的新特性。旧的 Windows NT 信任关系是非传递的。例如，在旧的 Windows NT 架构中，A 域可以信任 B 域，B 域可以信任 C 域，但 A 域不会自动信任 C 域。但在 Windows 2000 架构中，信任关系是传递的，使用 A → B → C 信任关系，存在传递信任，即 A 域信任 C 域。

Active Directory 使用 Kerberos 安全协议建立域之间的信任关系。Kerberos 信任是传递的且层次化的。Kerberos 的层次信任关系是：使用相同命名空间的域会自动被其所属域信任。传递信任是在多个域之间流，即 A 信任 B，B 信任 C，隐含 A 信任 C。图 6.2 显示了一个信任关系集。

注意：Kerberos 适用于 Windows 2000 客户端和服务器，因此如果你处于混合环境，则使用 NT LAN 管理器（NTLM）与 NT 系统交互。

# 图 6.2 隐式和显式信任关系

![](img/729efc56f204a2ebffb8295c3a2dfdf_274_0.png)

# 系统文件与备份 Active Directory

Active Directory 的系统数据文件包括：

- Active Directory 本体（NTDS.DIT 文件）
- 证书服务数据库（如果安装了证书机构）
- 类注册（组件服务的数据库）
- 性能计数器配置
- 注册表
- SYSVOL — 共享文件夹，包含组策略模板和用户登录脚本

在执行 Active Directory 备份时，所有这些数据会被存储。Active Directory 支持全量备份；无法进行增量备份。备份的最长有效期为60 天，这被称为墓碑时间（tombstone time）。当你向 Active Directory 恢复数据时，可以通过两种方式之一进行：

- 权威恢复（Authoritative）
- 非权威恢复（Non-authoritative）

