

## 23.4.17.1 命令触发

有三个命令可使 CAA 评估应用程序资源的放置和平衡：

-   caa_balance 命令。
-   caa_start 命令（参见第 23.4.14 节）。
-   caa_relocate 命令（参见第 23.4.16 节）。

从 V5.1B 开始，可以随时使用 caa_balance 命令重新评估集群中应用程序资源的放置。

-   重新评估集群中的所有应用程序资源。

    ```
# caa_balance -all
Attempting to stop `cluster_lockd` on member `alph11`
Stop of `cluster_lockd` on member `alph11` succeeded.
Attempting to start `cluster_lockd` on member `alph12`
Start of `cluster_lockd` on member `alph12` succeeded.
Resource clustercron is already well placed
Resource memberUP is already well placed
clustercron is placed optimally. No relocation is needed.
memberUP is placed optimally. No relocation is needed.
powerUP is placed optimally. No relocation is needed.
    ```

-   重新评估特定集群成员上的资源。

    ```
# caa_balance -s molari
Attempting to stop `cluster_lockd` on member `alph13`
Stop of `cluster_lockd` on member `alph13` succeeded.
Attempting to start `cluster_lockd` on member `alph11`
Start of `cluster_lockd` on member `alph11` succeeded.
Resource memberUP is already well placed
Resource powerUP is already well placed
memberUP is placed optimally. No relocation is needed.
powerUP is placed optimally. No relocation is needed.
    ```

-   重新评估特定的应用程序资源。

    ```
# caa_balance memberUP powerUP
Resource memberUP is already well placed
Attempting to stop `powerUP` on member `alph11`
Stop of `powerUP` on member `alph11` succeeded.
Attempting to start `powerUP` on member `alph12`
Start of `powerUP` on member `alph12` succeeded.
memberUP is placed optimally. No relocation is needed.
    ```

有关应用程序资源负载平衡的更多信息，请参阅 caa_balance(8) 参考手册页以及《TruCluster Server 集群高可用应用程序指南》。

## 23.4.17.2 集群触发

当集群形成，或有成员加入或离开集群时，CAA 将根据以下条件平衡应用程序资源的负载：

-   集群形成时，资源的启动和负载平衡基于：
    -   AUTO_START 属性。
    -   ACTIVE_PLACEMENT 属性。
    -   PLACEMENT 和 HOSTING_MEMBERS 属性。
    -   REQUIRED_RESOURCES 和 OPTIONAL_RESOURCES 属性。

-   如果成员加入集群，资源的负载平衡基于：
    -   AUTO_START 属性。
    -   ACTIVE_PLACEMENT 属性。
    -   PLACEMENT 和 HOSTING_MEMBERS 属性。
    -   REQUIRED_RESOURCES 和 OPTIONAL_RESOURCES 属性。

-   如果成员离开集群，资源将根据以下属性进行故障转移（并平衡负载）：
    -   PLACEMENT 和 HOSTING_MEMBERS 属性。
    -   REQUIRED_RESOURCES 和 OPTIONAL_RESOURCES 属性。

### 23.4.17.2.1 集群形成时的资源放置与负载平衡

CAA 按如下方式确定要启动哪些资源：

-   如果资源的 TARGET 状态为 ONLINE，则启动该资源。
-   如果资源的 TARGET 状态为 OFFLINE，但 AUTO_START 设置为 1，则启动该资源。

当 CAA 启动资源时，必须将资源放置在满足资源配置文件中所设定条件的成员上，并考虑集群中当前运行的资源数量。

确定资源的 PLACEMENT。如果 PLACEMENT 为 "favored" 或 "restricted"，则确定有哪些 HOSTING_MEMBERS 可用。

-   PLACEMENT 为 "balanced"
    -   无依赖

        将资源放置在在线资源数量最少的成员上。
    -   OPTIONAL_RESOURCES

        将资源放置在有所需资源可用且正在运行的资源数量最少的成员上。如果没有成员具有所需的可用资源，则在运行资源数量最少的成员上启动。

