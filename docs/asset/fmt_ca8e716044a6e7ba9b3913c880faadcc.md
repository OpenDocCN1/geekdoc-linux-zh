
```cpp
BOOL LookupAccountName(
    LPCTSTR sysname,
    LPCTSTR accountname,
    PSID sid,
    DWORD sidsize,
    LPCTSTR domainname,
    DWORD domainnamesize,
    PSID_NAME_USE sidtype
);
```

参数 `sysname` 是一个指向空终止字符串的指针，指定系统（可以是远程计算机的名称）。如果字符串为 `NULL`，则在本地系统中查找帐户名。参数 `accountname` 是一个指定帐户或用户名的空终止字符串。参数 `sid` 是一个指向缓冲区的指针，用于接收与 `accountname` 所指向的第一个帐户名对应的 SID 结构。参数 `sidsize` 指定缓冲区的大小。如果不指定足够的缓冲区大小，`LookupAccountName` 将失败，并在该参数中返回适当的缓冲区大小。参数 `domainname` 是一个指向缓冲区的指针，用于接收发现帐户的域名称。下一个参数 `domainnamesize` 指定包含域名称的缓冲区大小。最后一个参数 `sidtype` 在函数返回时将接收一个指示账户类型的值。我们对此参数不感兴趣，指定它是为了容纳返回的信息。

## AddAllowedACE and AddDeniedACE

这些例程用于向 ACL 中添加 ACE，以允许或拒绝在 `LookupAccountName` 调用中指定的用户执行指定的操作。该操作相对于受访问控制的对象类型。这些例程具有相同的调用序列，如下所示：

```cpp
BOOL AddAllowedAce (
    PACL acl,
    DWORD aclrev,
    DWORD aclmask,
    PSID sid);
```

```cpp
BOOL AddDeniedAce (
    PACL acl,
    DWORD aclrev,
    DWORD aclmask,
    PSID sid);
```

参数 `acl` 是指向包含要添加特定访问权限的 ACL 数据结构的指针。参数 `aclmask` 必须设置为 `ACL_REVISION`。参数 `aclmask` 指定向指定 SID 允许或拒绝的权限掩码。最后一个参数 `sid` 是一个代表用户、组或帐户的指针。

## MICROSOFT WINDOWS SAMPLE PROGRAM

示例 7-1 中的程序在文件上放置了安全描述符。文件是演示微软安全性的简单对象之一。记住，你必须在 NTFS 卷上创建文件。

字体 应用于文件的基础 Windows NT/2000 安全描述符

```cpp
#include <windows.h>
#include <iostream.h>

SECURITY_ATTRIBUTES sa;
SECURITY_DESCRIPTOR sd;
BYTE aclbuf[1024], SIDbuf[100];
PACL acl=(PACL)aclbuf;
PSID psid=(PSID)SIDbuf;
DWORD domainbufSize = 100;
DWORD domainbufsz = 80;
char domainbuf[80];
SID_NAME_USE sn;
HANDLE hFile;

void main(void)
{
    InitializeSecurityDescriptor(&sd, SECURITY_DESCRIPTOR_REVISION);
    InitializeAcl(acl, sizeof(aclbuf), SECURITY_REVISION);
```

应用于文件的基础 Windows NT/2000 安全（续）

```cpp
LookupAccountName(0, "guest", psid, &domainbufSize, domainbuf, &domainbufsz, &sn);
AddAllowedAce(acl, ACL_REVISION, GENERIC_READ, psid);
SetSecurityDescriptor(&sd, TRUE, FALSE);

s.nLength=sizeof(SECURITY_ATTRIBUTES);
s.bInheritHandle = FALSE;
s.lpSecurityDescriptor = &sd;
hFile = CreateFile("testacl.txt", GENERIC_READ | GENERIC_WRITE, 0, &sa, CREATE_NEW, FILE_ATTRIBUTE_NORMAL, 0);
CloseHandle(hFile);
```

执行这些操作后，进入 Windows 资源管理器，右键点击 `testacl.txt`，点击安全选项卡，然后点击权限。你会看到 `guest` 具有特殊访问。

## 管理令牌

存在若干例程允许用户管理令牌。表 7.1 列出了其中一些例程。访问令牌是描述进程或线程安全上下文的对象。当用户登录时，系统产生一个访问令牌。执行此用户的进程拥有该令牌的副本。

| Windows 令牌管理 API |
| :--- |
| AdjustTokenPrivileges | 启用或禁用令牌中的权限。 |
| DuplicateToken | 创建一个已存在的访问令牌。 |
| GetTokenInformation | 获取有关令牌的信息。 |
| OpenThread | 打开与线程相关的令牌。 |
| OpenProcessToken | 打开与进程相关的令牌。 |
| SetTokenInformation | 为指定的令牌设置各种类型的信息。它将替换现有的信息。 |
| Windows 令牌管理 API（续） |
| :--- |
| SetThreadToken | 为线程分配伪装令牌。该函数还可以导致线程停止使用伪装令牌。 |
| GetAclInformation | 获取有关 ACL 的信息。 |
| LookupAccountSid | 接受 SID 作为输入，并检索该 SID 的帐户名以及其所在的第一个域名。 |
| CheckTokenMembership | Determine指定的 SID 是否在访问令牌中启用。 |

## AdjustTokenPrivileges

`AdjustTokenPrivileges` 函数启用或禁用指定访问令牌中的权限，并具有以下调用序列：

```cpp
BOOL AdjustTokenPrivileges(
    HANDLE tokenhandle,
    BOOL disableallprivs,
    TOKEN_PRIVILEGES newstate,
    DWORD buflen,
    TOKEN_PRIVILEGES *state,
    PDWORD returnlen
);
```

参数 `tokenhandle` 标识要修改权限的访问令牌。使用 `OpenProcessFunction` 获取进程的主令牌，或使用 `OpenThreadFunction` 获取伪装令牌的句柄。这些函数将在下一节中讨论。`disableallprivs` 和 `newstate` 参数对调用此例程的结果产生相互影响。表 7.2 描述了这两个参数的关系和影响。

| 表.2 AdjustTokenPrivileges API 中 disableallprivs 和 newstate 参数的影响 |
| 设置 newstate | 权限操作 |
| :--- | :--- |
| TRUE | 忽略 | 所有权限被禁用。 |
| FALSE | 指向 TOKEN_PRIVILEGES 结构，该结构指示如何修改权限 | 权限被修改。 |

# Microsoft Windows 安全：访问令牌与安全描述符

`TOKEN_PRIVILEGES` 结构包含以下元素：

```cpp
typedef struct _TOKEN_PRIVILEGES {
    DWORD privcount;
    LUID_AND_ATTRIBUTES privs[ANYSIZE_ARRAY];
} TOKEN_PRIVILEGES;
```

数据元素 `privcount` 指定了 `privs` 数组中的项数。`privs` 数组指定了一个本地唯一标识符 (`LUIDs`) 和属性结构数组。`LUID` 是一个 64 位值，保证在生成它的系统上是唯一的。`LUID` 的唯一性在系统重启之前都能得到保证。`LUID` 不用于直接操作。应用程序允许使用函数和结构来管理 `LUID` 值。对于每个权限，必须通过调用例例程序 `Lookup-PrivilegeValue` 来获取 `LUID`，该例程将在后续节中讨论。

权限的属性可以被设置为 `SE_PRIVILEGE_ENABLED` 或 `SE_PRIVILEGE_ENABLED_BY_DEFAULT`。`LUID_AND_ATTRIBUTES` 结构由以下数据元素组成：

```cpp
typedef struct _LUID_AND_ATTRIBUTES {
    LUID luid;
    DWORD attributes;
} LUID_AND_ATTRIBUTES;
```

除非你对访问令牌之前的权限状态感兴趣，否则参数 `buflen`、`prestate` 和 `returnlen` 可以设为 `NULL`。

# LookupPrivilegeValue

该例程具有以下调用序列：

```cpp
BOOL LookupPrivilegeValue(
    LPCTSTR systemname,
    LPCTSTR pname,
    PLUID privuid
);
```

参数 `systemname` 是一个以空字符终止的字符串，指定要从中查找权限的系统名称。如果设置为 `NULL`，则权限查找将在本地系统进行。参数 `pname` 是一个以空字符终止的字符串，指定在 `WINNT.H` 文件中找到的权限名称。参数 `privuid` 是指向变量的指针，该变量将接收由 `systemname` 参数指定的系统中标识该权限的 `LUID`。

# OpenProcessToken 和 OpenThreadToken

这些例程用于获取访问令牌的句柄。例程 `OpenProcessToken` 具有以下调用序列：

# 第 7 章 保护系统资源

```cpp
BOOL OpenProcessToken(
HANDLE processhandle,
DWORD desaccess,
PHANDLE tokhandle);

BOOL OpenThread(
HANDLE threadhandle,
DWORD desaccess,
BOOL openself
PHANDLE tokhandle );
```

参数 `processhandle` 包含要打开的令牌的进程句柄。参数 `desaccess` 指定一个访问掩码，列出了请求的访问令牌的类型。这些请求的访问类型将与令牌的任意访问列表 (`ACL`) 进行比较，以确定哪些访问被授予或拒绝。在例程 `OpenThreadToken` 中，参数 `openself` 指定一个标志，指示访问检查是针对调用 `OpenThread` 函数的线程的安全上下文进行的，还是针对调用线程进程的安全上下文进行的。表 7.3 列出了为访问令牌定义的所有访问权限。

| OpenProcessToken 期望的令牌访问参数 |
|---|---|
| TOKEN_ADJUST_DEFAULT | 提供用于……更改访问令牌的默认 ACL、主组或所有者。 |
| TOKEN_ADJUST_GROUPS | 更改访问令牌中指定的组。 |
| TOKEN_ADJUST_PRIVILEGES | 更改访问令牌中指定的权限。 |
| TOKEN_DUPLICATE | 复制访问令牌。 |
| TOKEN_IMPERSONATE | 为进程附加一个冒充访问令牌。 |
| TOKEN_QUERY | 查询访问令牌的内容。 |
| TOKEN_QUERY_SOURCE | 查询访问令牌的源。 |

参数 `tokhandle` 是指向句柄的指针，当函数返回时，它标识新打开的访问令牌。

`SetThreadToken` 函数为线程分配一个冒充令牌。该函数还可以导致线程停止使用冒充令牌，并具有以下调用序列：

```cpp
BOOL SetThreadToken(
HANDLE thread,
HANDLE token);
```

参数 `thread` 是指向线程句柄的指针，该函数向该线程分配冒充令牌。如果 `thread` 为 `NULL`，则函数将冒充令牌分配给调用线程。参数 `token` 是指向要分配给线程的冒充令牌的已打开句柄。该句柄必须以 `TOKEN_IMPERSONATE` 访问权限打开。如果 `token` 为 `NULL`，该函数导致线程停止使用冒充令牌。

# Microsoft Windows 安全：访问令牌与安全描述符 233

# CheckTokenMembership

此函数确定指定的 SID 是否在访问令牌中启用，并具有以下调用序列：

```cpp
BOOL CheckTokenMembership(
    HANDLE handle,
    PSID sidcheck,
    PBOOL ismember
);
```

参数 `handle` 代表指向访问令牌的句柄。如果此参数为 `NULL`，则该例程使用调用线程的冒充令牌。如果线程没有进行冒充，该函数将复制主令牌以创建冒充令牌。`sidcheck` 参数是指向 SID 的指针。该例程检查此 SID 是否在访问令牌的用户 SID 和组 SID 中存在。参数 `ismember` 是一个指向 `BOOL` 变量的指针，该变量将接收检查结果。如果该 SID 存在且具有 `SE_GROUP_ENABLED` 属性，则 `ismember` 返回 `TRUE`；否则，返回 `FALSE`。

# GetTokenInformation

该例程检索有关访问令牌的特定类型信息，并具有以下调用序列：

```cpp
BOOL GetTokenInformation(
    HANDLE hToken,
    TOKEN_INFORMATION_CLASS TokenInfo,
    LPVOID TokenInfo,
    DWORD TokenLen,
    PDWORD ReturnLength
);
```

参数 `hToken` 是从从中检索信息的访问令牌的句柄。`TokenInfo` 参数包含指定要信息类型的值。`TokenInfo` 参数是指向缓冲区的指针，函数向其中填充请求的信息。填充的结构取决于 `TokenInfo` 指定的。如果 `TokenInfo` 参数为 `NULL`，`GetTokenInformation` 可用于确定接收信息缓冲区的大小。在这种情况下，仅指定 `ReturnLength`。

# 表 7.4 Token 类参数值及含义

| Token 类参数 | 返回信息 |
| --- | --- |
| TokenUser | 缓冲区接收包含令牌用户的 `TOKEN_USER` 结构。 |
| TokenGroups | 缓冲区接收与令牌相关的组账户 `TOKEN_GROUPS` 结构。 |
| TokenPrivileges | 缓冲区接收令牌权限的 `TOKEN_PRIVILEGES` 结构。 |
| TokenOwner | 缓冲区接收新创建对象的默认所有者 `TOKEN_OWNER` 结构。 |
| TokenDefaultDacl | 缓冲区接收新创建对象的默认 DACL 的 `TOKEN_DEFAULT_ACL` 结构。 |
| TokenStatistics | 缓冲区接收各种令牌统计信息的 `TOKEN_STATISTICS` 结构。 |

# LookupAccountSid

此函数接受 SID 作为输入，并检索该 SID 的帐户名称以及发现该 SID 的第一个域名称。该例程具有以下调用序列：

```cpp
BOOL LookupAccountSid(
    LPCTSTR sysname,
    PSID sid,
    LPCTSTR account,
    LPDWORD accounts,
    LPCTSTR refdomainName,
    LPDWORD refdomainNamesz,
    PSID_NAME_USE sidtype
);
```

参数 `sysname` 是指向以空字符终止的字符串的指针，指定远程计算机名称，也可以设置为 `NULL`，则将在本地系统中查找 SID。参数 `sid` 是指向安全描述符结构的指针，用于查找帐户名称。参数 `account` 是指向缓冲区的指针，接收与 `sid` 参数对应的以空字符终止的帐户名称。参数 `accounts` 是指向双字变量的指针，指定缓冲区的大小。参数 `refdomainName` 是指向缓冲区的指针，该缓冲区将接收以空字符终止的字符串，给出发现帐户的域名称。参数 `refdomainNamesz` 是指向双字的指针，包含 refdomain 缓冲区的大小。参数 `sidtype` 由此函数返回并指定安全类型信息。

## GetACLInformation

此例程检索有关 ACL 的信息，其调用序列如下：

```cpp
BOOL GetAclInformation(
 PACL acl,
 LPVOID aclinfo,
 DWORD aclInfoSize,
 ACL_INFORMATION_CLASS aclinfoClass
);
```
