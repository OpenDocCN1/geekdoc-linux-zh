
为了保持集群中的时钟同步，我们在管理节点上安装了时间服务器（`xntpd`）。如果你有另一个时间源，你可能想在管理节点上配置 `xntpd` 以与该时间源同步。重要的是所有节点上的时钟必须一致，而不是它们显示的时间必须正确。如果你没有外部时间源，默认的 Red Hat 配置可以正常工作。要启动服务，请使用命令：

```bash
# /etc/rc.d/init.d/xntpd start
# /sbin/chkconfig xntpd on
```

### 7.2.2 域名系统 (DNS)

名称服务器的设置可能具有很强的站点特定性。如果你计划为集群中的所有节点使用真实名称，那么与你的网络管理员讨论如何配置名称服务器，以及你是否应该在管理节点上运行名称服务器是非常关重要的。此类细节超出了本红书的范围。

`xCAT` 要求名称服务器能够解析集群中节点的地址。如果你知道如何操作，你可以选择配置名称服务器以解析集群内部和外部的地址。同样，这超出了本红书的范围。如果你决定为所有地址配置名称服务器，请注意 `makedns` 会生成名为 `named.conf` 的名称服务器配置文件。建议先运行 `makedns` 然后仅进行本地定制。

如果你已正确设置了 `/etc/hosts` 和 `site.tab`，那么为集群地址配置名称服务器只需运行 `makedns`：

```bash
# /usr/local/xcat/sbin/makedns
```

`makedns` 会在运行过程中重启你的名称服务器。通过查询本地名称服务器获取集群内节点的名称和 IP 地址来验证其工作情况。在示例 7-7 中，我们使用 `host` 命令查询本地名称服务器（比连接到 `localhost` 效率更高）。

```bash
Example 7-7 查询本地名称服务器的 host 命令
[root@master]# host node1.cluster.austin.ibm.com 0
Using domain server 0.0.0.0:
node1.cluster.austin.ibm.com has address 192.168.0.1
nodel1.cluster.austin.ibm.com mail is handled (pri=10) by
nodel1.cluster.austin.ibm.com
[root@root ~] host 192.168.0.1 0
Using domain server 0.0.0.0:
1.168.192.IN-ADDR.ARPA domain name node1.cluster.austin.ibm
```

如果上述测试失败，请返回检查 `syslog` (`/var/log/messages`) 中来自名称服务器的任何错误，并验证 `/etc` 中 `makedns` 创建的 `.db` 文件。你可能在 `site.tab` 或 `/etc/hosts` 中存在错误。

### 7.2.3 用户 ID/网络信息系统 (NIS)

出于作业调度目的，将任何用户节点的用户 ID 复制到整个集群中是非常重要的。`xCAT` 支持 NIS，尽管已证明这种支持在较大的集群中会遇到扩展性问题。在集群中分发用户 ID 的推荐方法是从用户节点将 `/etc/passwd` 和 `/etc/group` 复制到所有计算节点。注意不应复制 `/etc/shadow`，因为这将允许用户登录到计算节点；运行批处理作业只需要用户 ID 存在。

如果你想使用 NIS，你应该现在根据你的站点环境设置它。否则，在你设置好用户节点后，你应该使用 `pcp` 复制文件。

## 网络文件系统 (NFS)

NFS 用于集群中的 Kickstart 安装和分发主目录。为了让这些过程运行，我们必须将某些目录添加到 `/etc/exports` 包含导出列表中。我们集群的配置如示例 7-8 所示，所示地址和选项之间不能有空格。

示例 7-8 `/etc/exports`

```text
/install/rh62 192.168.0.0/255.255.255.0(ro,no_root_squash)
/install/post 192.168.0.0/255.255.255.0(ro,no_root_squash)
/usr/local 192.168.0.0/255.255.255.0(ro,no_root_squash)
/home 192.168.0.0/255.255.255.0(rw)
```

你也可以通过主机名指定你的网络是否是非连续的，尽管这会有轻微的性能损失。例如：

```text
# /home node*(rw)
```

一旦修改了 `/etc/exports`，使用以下命令启动 NFS：

```bash
# /etc/rc.d/init.d/nfs start
```

通过查询 NFS 服务器验证文件系统是否已正确导出，如示例 7-9 所示。

```bash
Example 7-9 showmount -e 输出
[root@master ~] showmount -e
Export list for master:
/home 192.168.0.0/255.255.255.0
/usr/local 192.168.0.0/255.255.255.0
/install/post 192.168.0.0/255.255.255.0
/install/rh62 192.168.0.0/255.255.255.0
```

如果列表与你的 `/etc/exports` 不匹配，可能是文件中存在错误。如果命令失败，说明 NFS 未正常工作。一旦 NFS 工作，使用命令将其配置为启动：

```bash
# /sbin/chkconfig nfs on
```

### 7.2.4 动态主机配置 (DHCP)

可以使用 `xCAT` 提供的 `gendcp` 脚本自动配置 DHCP。注意此脚本会在适配器上设置别名。如果在 `site.tab` 中指定了 `eth1`，`gendcp` 将创建 `eth1:0`。不要手动使用此别名，否则会被覆盖。

`gendcp` 命令在 `/tmp` 中创建一个 `dhcpd.conf` 骨架：

```bash
# gendcp
```

脚本输出将建议你通过为设备（如你的 Myrinet 交换机）添加 IP 地址来编辑 `dhcpd.conf`。注意：你需要删除不需要的条目。在我们的实验中，删除了一些不需要的条目。要添加静态主机条目，需要知道设备的 MAC 地址。确保条目与你的管理网络匹配。静态主机的示例见示例 7-10。

```nginx
Example 7-10 dhcpd.conf 中的子网声明
# subnet for management network
subnet 192.168.2.0 mask 255.255.255.0 {
    # Static host entry for Myrinet switch
    host myril {
        hardware ethernet 00:60:dd:7f:94:b0;
        fixed-address myril;
    }
}
```

完成 `dhcpd.conf` 编辑后，将其复制到 `/etc` 并使用命令重启 DHCP 服务器：

```bash
# cp -f /tmp/dhcpd.conf /etc
# /sbin/chkconfig dhcpd on
```

如果 `dhcpd.conf` 中存在错误，服务器将无法启动并产生错误消息。检查 `dhcpd.conf` 和你的 `site.tab`，必要时重新运行 `gendcp`。同时也检查 `/var/log/messages` 中的错误。

提示：避免在所有接口 (`eth0`, `eth1`...) 中让 DHCP 提供并分配 IP 地址的替代方法是在修改 `dhcpd` 启动脚本时添加接口名称。脚本位于 `/etc/rc.d/dhcpd`。例如：

```bash
# Start daemons.
echo -n "Starting dhcpd: " /sbin/dhcpd eth1
```

## 7.3 收集 MAC 地址

一旦设置好 DHCP 服务器，我们就准备好收集节点的 MAC 地址了。在收集之前必须运行两个脚本：

- `# /usr/local/xcat/stage/mkstage`
- `# /usr/local/xcat/ks62/mks`

这些脚本的工作部分是验证。如果它们报告缺少文件或类似的错误，可能意味着你错过了安装过程某个步骤。它们的主要任务是从远程启动过程在 `/tboot` 中创建各种文件。

如果 `mkstage` 和 `mks` 正常运行，则收集 MAC 地址。这是使用 `getmacs` 脚本完成的，如示例 7-11 所示。
