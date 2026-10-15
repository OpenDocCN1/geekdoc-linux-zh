
`display` 指定到 X 服务器的连接。

`timeout_return` 返回超时时间（单位：秒），直到屏幕保护程序开启。

`interval_return` 返回屏幕保护程序每次调用之间的间隔。

`prefer_blanking_return` 返回当前的屏幕留白偏好（`DontPreferBlanking`、`PreferBlanking` 或 `DefaultBlanking`）。

`allow_exposures_return` 返回当前的屏幕保护控制值（`DontAllowExposures`、`AllowExposures` 或 `DefaultExposures`）。

# 控制主机访问

本节讨论了如何：

- 从访问控制列表中添加、获取或删除主机
- 更改、启用或禁用访问

X 不为单个窗口提供任何保护。如果你找到了某个资源的 ID（`resource ID`），你就可以对其进行操作。然而，为了提供最小程度的保护，仅允许来自受信任机器的连接。这对于单用户工作站是足够的，但显然在共享时间时代会失效。尽管 X 协议中存在适当的连接身份验证机制，但由于缺乏标准的身份验证服务器，主机级访问控制成为唯一的通用机制。

初始允许建立连接的主机列表通常包括：

- 运行主机窗口系统的主机。
- 在符合 POSIX 的系统上，`/etc/X?.hosts` 文件列出的每个主机。`?` 表示显示数量。该文件应由换行符分隔的主机组成。DECnet 节点必须以 `::` 结尾，以与 Internet 主机区分。

当启用访问控制机制时，如果主机不在访问控制列表中且该主机尝试建立连接，服务器将拒绝连接。要更改访问列表，客户端必须留在同一台服务器上，和/或者在初始授权设置中已获得许可。

服务器除了此主机访问功能外，还实施了其他的访问控制策略。有关其他访问控制实现的更多信息，请参阅《X System Protocol》。

## 添加、获取或删除主机

Xlib 提供了供你从访问控制列表中添加、获取或删除主机函数。所有主机控制函数都使用 `XHostAddress` 结构，该结构包含：

```
typedef struct {
    int family;            /* 例如 FamilyInternet */
    int length;             /* 地址的长度，单位：字节 */
    char *address;         /* 指向查找地址的指针 * */
} XHostAddress;
```

`family` 成员指定使用哪种协议（例如 `FamilyInternet`），可以是 `FamilyInternet`、`FamilyInterpreted` 或 `DECNet`。`length` 成员指定地址的字节长度。`address` 成员是指向查找地址的指针。对于 TCP/IP，地址应为网络字节。对于 IP 版本 4，长度为 4 字节。对于 IP 版本 6，长度为 16 字节。对于 DECNet，长度为 2 字节。第一个字节包含节点号。第二个字节包含节点号的高位。`address` 成员是一个指向 `XHostAddress` 结构的指针，该结构包含：

```
typedef struct {
    int length;             /* 类型字符串的长度 */
    int valuelength;        /* 值字符串的长度 */
    char *type;             /* 指向类型字符串的指针 */
} XHostAddress;
```

`type` 和 `value` 成员指向表示类型和值的字符串。这些字符串可能没有以 NULL 结尾，因此访问时需要注意。`length` 和 `valuelength` 指定字符串的长度。

要添加单个主机，使用 `XAddHost`。

```
XAddHost(display, host);
```

`display` 指定到 X 服务器的连接。

`host` 指定要添加的主机。

`XAddHost` 函数将主机添加到该显示器的访问控制列表中。服务器必须与执行客户端位于同一台主机上，否则将产生 `BadAccess` 错误。

`XAddHost` 可能产生 `BadAccess` 和 `BadValue` 错误。

要一次性添加多个主机，使用 `XAddHosts`。

```
XAddHosts(display, hosts, num_hosts);
```

`display` 指定到 X 服务器的连接。

`hosts` 指定要添加的主机列表。

`num_hosts` 指定主机数量。

`XAddHosts` 函数将每个主机添加到该显示器的访问控制列表中。服务器必须与执行客户端位于同一台主机上，否则将产生 `BadAccess` 错误。

`XAddHosts` 可能产生 `BadAccess` 和 `BadValue` 错误。

要获取列表，使用 `XListHosts`。

```
XHostAddress* XListHosts(display, nhosts_return, state_return);
```

`display` 指定到 X 服务器的连接。

`nhosts_return` 返回访问控制列表中当前的主机数量。

`state_return` 返回访问控制的状态。

`XListHosts` 函数返回当前的访问控制列表，以及在连接设置时是否启用或禁用列表。`XListHosts` 允许程序查找哪些机器可以建立连接。它返回一个指向由函数分配的主机结构列表的指针。当不再需要时，应调用 `XFree` 释放这些内存。

要删除单个主机，使用 `XRemoveHost`。

```
XRemoveHost(display, host);
```

`display` 指定到 X 服务的器的连接。

`host` 指定要移除的主机。

`XRemove` 函数从该显示器（`display`）的访问控制列表中移除指定的主机。服务器必须与客户端进程位于同一台主机上，否则将产生 `BadAccess` 错误。如果你从访问列表中删除了你的机器，你将无法连接到该服务器，除非重置服务器，否则此操作是不可逆的。

`XRemoveHost` 可能会产生 `BadAccess` 和 `BadValue` 错误。

要一次性移除多个主机，请使用 `XRemoveHosts(display, hosts, num_hosts)`。

`display` 指定到 X 服务的器的连接。

`hosts` 指定每个要移除的主机。

`num_hosts` 指定主机的数量。

`XRemoveHosts` 函数从该显示器（`display`）的访问控制列表中移除指定的主机。服务器必须与客户端进程位于同一台主机上，否则将产生 `BadAccess` 错误。如果你从访问列表中删除了你的机器，你将无法连接到该服务器，除非重置服务器，否则此操作是不可逆的。

`XRemoveHosts` 可能会产生 `BadAccess` 和 `BadValue` 错误。

## 窗口与会话管理器函数

`display` 指定到 X 服务的器的连接。

`host` 指定要移除的主机。

# 修改、启用或禁用访问控制

Xlib 提供了可以用来启用、禁用或更改访问控制的函数。

为了使这些函数成功执行，客户端应用程序必须与 X 服务器位于同一台主机上，并且或者在设置时的初始化授权中被授权。

要更改访问控制，请使用 `XSetAccessControl(display, mode)`。

`display` 指定到 X 服务的器的连接。

`mode` 指定模式。你可以传递 `EnableAccess` 或 `DisableAccess`。

`XSetAccessControl` 函数会在每次连接设置时启用或禁用访问控制列表。

`XSetAccessControl` 可能会产生 `BadAccess` 和 `BadValue` 错误。

要启用访问控制，请使用 `XEnableAccessControl(display)`。

`display` 指定到 X 服务的器的连接。

## 窗口与会话管理器函数

`XEnableAccessControl` 函数会在每次连接设置时启用访问控制列表。

`XEnableAccessControl` 可能会产生 `BadAccess` 错误。

要禁用访问控制，请使用 `XDisableAccessControl`。

```
XDisableAccessControl(display);
```
