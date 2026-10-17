
图 27-1 `example.org` 的 LDAP 树

## 684 Linux 管理：初学者指南

## 客户端/服务器模型

与大多数网络服务一样，LDAP 遵循标准的客户端/服务器范式。客户端与服务器之间的典型交互如下：

- LDAP 客户端应用程序连接到 LDAP 服务器。此过程也称为“绑定到服务器”(`binding to a server`)。
- 根据服务器上配置的访问限制，LDAP 服务器会接受或细化绑定/连接请求。
- 假设服务器接受请求，客户端可以选择查询目录、浏览存储在服务器上的信息，或尝试修改/更新 LDAP 服务器上的信息。
- 同样，根据访问限制，服务器可以允许或拒绝客户端尝试的任何操作。如果服务器无法回答请求，它可能会将客户端指向另一个上游 LDAP 服务器，该服务器可能对请求有更具权威性的响应。

## LDAP 的用途

LDAP 是一种分布式目录服务，可以作为各种类型信息的存储。LDAP 目录几乎可以存储任何类型的信息——性质各异，如纯文本信息、图像、二进制数据或公钥证书等。

多年来，创建了各种 LDAP 架构 (`schemas`)，以便在 LDAP 目录中存储不同的数据源。以下是 LDAP 的一些用途：

- LDAP 可以作为组织的完整身份管理解决方案。它可以为用户提供身份验证和授权服务。事实上，网络信息服务（NIS；见第 26 章）提供的服务可以完全被 LDAP 代。
- DNS 记录中的信息可以存储在 LDAP 中。
- LDAP 可为组织提供“黄页”（例如用户或员工的联系信息——电话、地址、部门等）。
- 邮件路由信息可以存储在 LDAP 中。
- Samba 允许 Samba 服务器在 LDAP 中存储大量的对象属性。这使得 Samba 在需要冗余和复制的环境中可以作为 Microsoft Windows 域控制器的强大替代品。

## 第 27 章 轻级目录访问协议 (LDAP) 685

## LDAP 术语

如果你打算精通 LDAP 术语，最好了解基本的 LDAP 技术术语。本节定义了一些术语，并解释了你在处理 LDAP 时经常遇到的一些概念。

- **Entry**（或对象）：LDAP 目录中的一个单元。每个条目通过其区分名称 (`DN`) 进行唯一标识。这是一个示例：

```
uid=yyang, ou=sales, dc=example, dc=com
```

- **Attributes**（属性）：这些与条目关联的信息，例如组织的地址或员工的电话号码。
- **objectClass**：这是一个特殊属性。LDAP 中的所有对象必须具有 `objectClass` 属性。`objectClass` 定义指定了每个 LDAP 需要哪些属性，并指定了条目的对象类。此属性的值可以被客户端修改，但 `objectClass` 本身不能删除。

`objectClass` 定义本身存储在 `schema files` 中。
- **Schema**（架构）：决定目录结构和内容的规则集合。架构包含属性类型定义、`objectClass` 定义以及其他信息。

架构列出了每个对象类型的属性，以及这些属性是必需的还是可选的。架构通常存储在纯文本文件中。

以下是架构的示例：

- **core.schema**：定义基本的 LDAP3 属性和对象。它是 OpenLDAP 实现中必需的架构。
- **inetorgperson.schema**：定义 `inetOrgPerson` 对象类及其关联属性。该对象用于存储人员的联系信息。
- **LDIF**：代表 LDAP 数据交换格式 (`LDAP Data Interchange Format`)。它是用于 LDAP 条目的纯文本文件。用于向 LDAP 服务器导入或导出数据的文件应采用这种格式。用于 LDAP 服务器之间复制的数据也采用这种格式。

## OpenLDAP

OpenLDAP 是运行在 Linux/UNIX 系统上的 LDAP 开源实现。OpenLDAP 是一个程序包，由 `slapd`、`slurpd`、各种工具和库组成，通过各种客户端和服务器端实用实现了 LDAP 协议。

## 服务器端守护进程

服务端由两个主要的守护进程组成：

- `slapd` 这是一个独立的 LDAP 守护进程，监听来自客户端的 LDAP 连接，并对收到的 LDAP 操作做出响应。
- `slurpd` 这是一个独立的复制守护进程，用于将更改从一个 LDAP 服务器传播到另一个。(`700`)

## OpenLDAP 实用工具

OpenLDAP 实用工具是一组命令行工具，用于查询、查看、更新和修改存储在 LDAP 目录中的数据。在 Fedora、Red Enterprise Linux (`RHEL`) 和 CentOS 上，它们通过 `openldap-clients*.rpm` 包提供，部分通过 `openldap-servers*.rpm` 包提供。程序在表 27-1 中列出并描述。

| 实用工具 | 描述 |
| --- | --- |
| `ldapmodify` | 用于修改 LDAP 中的条目。它可以直接从命令行或通过文件接受输入。 |
| `ldapadd` | `ldapmodify -a` 命令的硬链接。用于向 LDAP 数据库添加新条目。（`ldapadd` 命令的功能可以通过向 `ldapmodify` 命令添加多个一个选项来获得。） |
| `ldapdelete` | 用于从 OpenLDAP 目录删除条目。 |
| `ldpasswd` | 为 LDAP 用户设置密码。 |
| `ldapsearch` | 用于查询/搜索 LDAP 目录。 |
| `slapadd` | 接受 LDIF 文件输入以填充 LDAP 目录。位于 `/usr/sbin/`。 |
| `slapcat` | 将 LDAP 目录的内容导出为 LDAP 类型文件。位于 `/usr/sbin/`。 |
| `slapindex` | 根据当前的实际内容对 LDAP 数据库进行重新索引。位于 `/usr/sbin/`。 |
| `slappasswd` | 用于生成经过哈希/加密的密码，可用于各种特权目录操作。位于 `/usr/sbin/`。 |

表 27-1 OpenLDAP 实用工具

## 第 27 章 轻量级目录访问协议 (LDAP)

## 安装 OpenLDAP

为了让 OpenLDAP 服务端和客户端组件运行起来，在 Fedora、`RHEL` 和 CentOS 系统上需要这些包：

- **`openldap-2*.rpm`** 为 OpenLDAP 提供配置文件和库。
- **`openldap-clients*.rpm`** 提供访问和修改 OpenLDAP 目录所需的客户端程序。
- **`openldap-servers*.rpm`** 提供配置和运行 LDAP 所需服务器 (`slapd`, `slurpd`) 以及其他工具。

> 提示：如果你仅配置客户端，则不需要 **`openldap-servers*.rpm`** 软件包。

我们将使用 **`dnf`** 软件包管理器在我们的示例系统上下载并安装 **`openldap-servers`** 软件包。步骤列如下：

1. 在以 root 身份登录时，首先通过查询 RPM 数据库来确认你已经安装了哪些包：

```bash
[root@fedora-server ~]# rpm -qa | grep -i openldap
openldap-2*
...<输出内容已截断>...
```

2. 我们的示例系统已经具备了基础的 openldap 库，因此我们将直接使用 **`dnf`** 安装 OpenLDAP 客户端和服务包。

```bash
[root@fedora-server ~]# dnf -y install openldap-servers openldap-clients
```

3. 安装成功完成后，你可以进入配置部分。

## 在 Ubuntu 中安装 OpenLDAP

可以使用高级软件包工具 (`APT`) 在基于 Debian 的 Linux 发行版（如 Ubuntu）上安装 OpenLDAP 服务器。以下是安装软件的命令：

```
master@ubuntu-server:~~$ sudo apt-get -y install slapd
```

安装过程还会通过一些问题（例如管理员密码）让你开始设置基本的 LDAP 服务器配置。OpenLDAP 服务器 (`slapd`) 进程在安装后也会自动启动。Debian 类系统的 LDAP 客户端工具由 `ldap-utils_deb` 包提供。你可以通过运行以下命令进行安装：

```
master@ubuntu-server:~ sudo apt-get install ldap-utils
```

## 配置 OpenLDAP

根据你想对目录进行的操作，配置目录可能是一件非常痛苦的事，也可以是一个简单的过程。如果你是在进行全新的部署，设置目录通常是很容易，因为你不需要担心任何遗留问题、现有用户或类似的问题。在具有现有基础设施的环境中，必须采取额外的预防措施。
