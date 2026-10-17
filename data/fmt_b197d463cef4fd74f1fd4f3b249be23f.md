
# Active Directory 练习题

## 1. 包含 Active Directory 中所有对象引用的 Active Directory 组件叫什么？

- a. 主数据库
- b. 中央目录
- c. 全局数据库
- d. 全局编录

## 2. 下列哪个角色是林范围的 FSMO 角色？

- a. PDC 仿真器
- b. 基础设施主
- c. 架构主
- d. 全局编录

## 3. `_gc` SRV 记录监听哪个端口？

- a. TCP 445
- b. UDP 137
- c. TCP 3268
- d. UDP 445

## 4. 你是包含一个根域和三个子域的 Active Directory 林的管理员。该林包含多少个每种 FSMO？

- a. 1 个域命名主，1 个架构主，3 个 PDC 仿真器，3 个基础设施主，3 个 RID 主
- b. 3 个域命名主，3 个架构主，3 个 PDC 仿真器，3 个基础设施主，3 个 RID 主
- c. 1 个域命名主，1 个架构主，4 个 PDC 仿真器，4 个基础设施主，4 个 RID 主
- d. 1 个域命名主，1 个架构主，1 个 PDC 仿真器，1 个基础设施主，1 个 RID 主

## 5. 你林中的架构主 FSMO 将离线几个小时，以便你的硬件供应商更换服务器的主板。为了允许你的客户端继续登录，你需要做的最少工作是什么？

- a. 在将其离线之前，将架构主 FSMO 转移到另一个域控制器。
- b. 在将其离线之前，将架构主 FSMO 夺取到另一个域控制器。
- c. 什么也不做。即使架构主离线，你的客户端仍可以登录。
- d. 在将其离线之前，从 Active Directory 用户和计算机中禁用域控制器的计算机账户。

## 6. 你是 Active Directory 网络上子域的管理员，属于 Domain Admins 组。你有一个应用程序需要配置应用程序目录分区，但你发现无法这样做。是什么阻止了你在域中创建应用程序目录分区？

- a. 你必须属于 Enterprise Admins 组才能创建应用程序目录分区。
- b. 你必须属于 Schema Admins 组才能创建应用程序目录分区。
- c. 你必须属于 Forest Admins 组才能创建应用程序目录分区。
- d. 你必须属于 DNS Admins 组才能创建应用程序目录分区。

## 7. RID 主 FSMO 以 ______ 的增量向域控制器分发 RID。

- a. 100
- b. 250
- c. 500
- d. 1,000

## 8. 你正在从运行 Windows Vista Business 的工作站登录到 Active Directory 子域。默认情况下，此工作站将查找哪里来与域同步其时钟？

- a. 子域的 PDC 仿真器
- b. 林根域的 PDC 仿真器
- c. 外部时钟
- d. 对工作站进行身份验证的域控制器

## 9. 每个对象的 SID 由两个部分组成：域部分和 ______。

- a. 远程标识符
- b. 全局唯一标识符
- c. 相对标识符
- d. 全局标识符

## 10. 你可以使用哪个实用工具查看和管理 PDC 仿真器 FSMO 角色持有者？

- a. Active Directory 用户和计算机
- b. Active Directory 架构
- c. Active Directory 站点和服务
- d. Active Directory 域和信任关系

### 案例场景

#### 场景 4-1：FSMO 角色放置—I

Contoso 制药公司在 14 个地点拥有 500 名员工。公司总部位于康涅狄格州哈特福德。所有地点都是 `contoso.com` 域的一部分，每个地点至少包含两台服务器，并可靠地连接。

- a. 你将在哈特福德地点放置哪些 FSMO 角色？
- b. 在尝试向域中添加新用户帐户时，你收到一个错误，指出无法创建这些帐户。你作为 Domain Admins 组的成员登录。最可能是什么导致了这个问题？
- c. 为了方便登录，你应该考虑在每个地点放置什么？

#### 场景 4-2：FSMO 角色放置—II

Contoso 制药公司正在扩展，包括几家公司新近收购的公司。虽然它们都将成为 `contoso.com` 林的一部分，但每家公司都希望保持自己的去中心化管理策略。为了满足这一要求，你将这些子公司安装为独立的域结构。其中一家名为 `litwareinc.com`。

- a. 这个新域需要适应哪些角色？
- b. 如果 `litwareinc.com` 决定在其域中为几位用户设置一个小型卫星办公室，而不将登录流量使用到父域的可用带宽，他们应该怎么做？
- c. 在 `contoso.com` 中，充当域命名主的服务器因电源浪涌而故障。直到此服务器重新在线之前，你无法为新的地点创建新的子域。目前预计域命名主问题无法在合理的时间内解决。你应该采取什么步骤来解决这个问题并创建必要的子域？

# 工作就绪

## 使用 Repadmin 查询域控制器

Daniel Weisman 是 Northwind Traders（`www.northwindtraders.com`）的 Active Directory 管理员。在 Daniel 将架构主控 `Schema Master` FSMO 角色 `seizing` 到另一个域控制器之前，他必须确保将持有该新角色的域控制器已与故障角色持有者上执行的更新保持同步。这可以通过使用 `repadmin` 命令行工具来实现。由于 Northwind Traders 域中 Active Directory 信息复制的自然延迟，目标域控制器可能尚未与最新更新完全同步。为避免在 `seizing` 操作期间丢失数据，目标域控制器必须拥有前一个角色持有者持有的最新信息。可以使用 `repadmin.exe` 命令行工具来检查域控制器的更新状态。

为了了解 Daniel 如何确定目标域控制器是否已更新，请考虑以下示例。

Northwind Traders 的域包含三个域控制器。`ServerA` 是域 `northwindtraders.com` 的 RID 主控，如果 `ServerA` 故障，`ServerB` 是 Daniel 计划中的新 RID 主控，而 `ServerC` 是该域中唯一的另一个域控制器。Daniel 需要确定 `ServerA` 停止运行前最后一次更新是什么。为此，Daniel 使用 Repadmin 工具并配合 `/showrepl` 开关来确定 `ServerB` 是否拥有最新的信息。在这个示例中，Daniel 在命令行提示符中输入以下命令（并收到相应的输出）：

```
C:\> repadmin /showreplv serverB.blueyonderairlines.com dc=blueyonderairlines, dc=com

New-York\serverA     @ USN 2604    @ Time 2003-07-03 12:50:44
San-Francisco\serverC @ USN 2706    @ Time 2003-07-03 12:53:36
```

```
C:\> repadmin /showreplv serverC.blueyonderairlines.com dc=blueyonderairlines, dc=com

New-York\serverA     @ USN 2590    @ Time 2003-07-03 12:50:44
Chicago\serverB      @ USN 3110    @ Time 2003-07-03 12:57:55
```

上述命令反映了对两个未受故障影响的域控制器的复制信息进行查询。`ServerA` 的输出是最重要的信息。在 `ServerB` 上，从 `ServerA` 收到的最后更新编号为 2604，这比第二条命令行结果中显示在 `ServerC` 上的更新编号 2590 更新。这意味着关于 `ServerA`，`ServerB` 拥有比 `ServerC` 更新的信息。如果这些信息相反且 Daniel 仍希望由 `ServerB` 接管该角色，他可以等到下一个复制周期或强制立即同步。关键在于，他已确保想要在该域中接管 RID 主控角色的域控制器拥有最新的信息。

# Active Directory 管理

### 目标领域矩阵

| 技术技能 | 目标领域 | 目标领域编号 |
| :--- | :--- | :---: |
| 创建用户、计算机和组 | 维护 Active Directory 账户。 | 4.2 |
| 创建用户、计算机和组 | 自动化创建 Active Directory 账户。 | 4.1 |

### 关键术语

- 访问令牌 `access token`
- 匿名登录 `Anonymous Logon`
- 身份验证 `authenticate`
- 身份验证 `authentication`
- 授权 `authorization`
