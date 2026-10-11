
### 8. 下一个窗口允许你配置防火墙接口。你可以手动操作，或者如果运行 SNMP，可以通过发现它们。选择 `Configure interfaces manually` 并点击 `Next`。

### 9. 手动接口窗口如图 9.21 所示。为每个网络接口输入相关信息。`name` 必须与实际接口对应（与在 Linux 主机上输入 `ifconfig` 一致），如 `eth0`。`Label` 是一个友好的名称，如 `OUTSIDE`。

## 图 9.21 手动接口

![](img/b38c01dfda8509e844932f876ae148_324_0.png)

### 10. 输入所有接口信息后，点击 `Next`。

### 11. 为了允许出流量，右键点击规则 0 创建另一个规则。

### 12. 在对话框区域，选择对象树。

### 13. 现在对象已经定义，让 Firewall Builder 继续。

### 14. 右键点击 Action 列并选择 `ACCEPT`。

### 15. 在对话框区域，选择对象树。

### 16. 满意选择后，点击 `Next`。

### 17. 一旦定义了对象，你就可以将它们拖入规则中以允许或拒绝它们之间的通信。在本示例中，我们使用 Windows XP 主机运行 Firewall Builder 并配置 Linux netfilter 防火墙。

### 18. 右键点击 Action 列并选择 `ACCEPT`。

### 19. 在对话框区域的顶部面板，让我们定义允许入站流量的规则。

### 20. 对于端口 443 `HTTPS` 重复步骤 20 和 21。

### 21. 右键点击 Action 列并选择 `ACCEPT`。

### 22.

## 图 9.22 接口

![](img/b38c01dfda8509e844932f876ae148_325_0.png)

### 23. 在对话框区域的顶部面板，右键点击并选择 `Insert Rule`。

### 24. 从对象树将 HTTP 和 HTTPS 拖到规则 0 的 Service 格中。

### 25. 现在从对象面板将 HTTP 和 HTTPS 服务拖到规则 0 的 Service 单元中。

### 26. 右键点击 Action 列中的红点并选择 `Accept`。

### 27. 为了允许访问，右键点击规则 0 创建另一个规则。

### 28. 从对象树将 HTTP 和 HTTPS 拖到一个规则的 Service 列。

### 29. 将对象树中的网络对象 `INTERNAL` 拖到新规则的 Source 列。

### 30. 你的策略应该像图 9.23 所示。

## 图 9.23 示例 FWBuilder 策略

| 策略 | NAT | 路由 | 源服务 | 接口方向动作 时间 | 选项 | 注释 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | | Any | | WEB1 TCP HTTPS TCP HTTP | All | | Any | 入站 Web |
| 1 | | INTERNAL Any | TCP HTTPS TCP HTTP TCP HTTPS | All | | Any | 出站 Web |

## 工具与陷阱...

## 不要把自己锁在外面

任何花时间配置防火墙的人都通过惨痛教训了解到，配置规则时必须非常小心。在配置任何其他规则之前，创建一个允许 `PERMIT` 管理访问的规则始终是个主意。因为只要你将默认策略设置为丢 `DROP`，除非你已将其添加到访问列表中，否则你的 SSH 连接将不再被允许。如果你忘记这样做，在应用策略后，你可能会发现自己无法远程访问防火墙了。如果发生这种情况，你将无法远程更新策略并更改 ACL。

下一步是告诉 FWBuilder 在哪里找到 SSH 可执行文件，因为 FWBuilder 通过这种方式将配置上传到防火墙。你需要在防火墙和 FWBuilder 控制台上都能运行 SSH（假设它们在不同的系统上）。

### 34. 从菜单中选择 编辑（Edit） | 偏选项（Preferences）。

### 35. 选择 SSH 选项卡并点击浏览（Browse）按钮。

### 36. 导航到你所需的 SSH 工具位置（例如 `plink.exe`）并点击打开（Open）。请注意，如果你在 Windows 上作为 FWBuilder 主机，则不能选择 `PuTTY.exe`；你必须使用命令行 PuTTY 程序 `plink.exe`。

### 37. 选择 SSH 可执行文件后，点击确定（OK）。

### 38. 在对象树中右键点击 LAB01 防火墙，并选择安装（Install）。

### 39. 选择想要安装到的防火墙，并点击下一步（Next）。

### 40. 输入 SSH 连接的用户名和密码。

### 41. 所有其他字段均为可选；但建议勾选“在防火墙上存储 fwb 副本（Store a copy of the fwb on the firewall）”。对选择满意后，点击确定。

上传完成后，你将获得“成功（Success）”状态（见图 9.24）。检查你的防火墙（`iptables -L`）将显示列出的新规则。

# 第 9 章 边界安全、DMZ、远程访问和 VPN

## 图 9.24 策略安装成功

![](img/b38c01d2fda8509e8449e32f876ae148_328_0.png)

正如你可能看到的，一旦你完成了对象的准备工作，添加或修改规则就变得简单了。此外，与其他免费 GUI 工具不同，FWBuilder 允许你从一个位置集中且安全地管理你所有的（支持的）防火墙。当你使用上述策略时，图 9.25 显示了生成的 iptables 规则示例。

## 图 9.25 FWBuilder 生成的链

- Chain `FORWARD` <policy drop>

| target prot opt source destination |
| :--- | :--- | :--- | :--- | :--- |
| `ACCEPT` | all | any | anywhere | state, RELATED, ESTABLISHED |
| `RULE_0` | tcp | all | anywhere 192.168.1.0/24 any | tcp multiport dports hports,http state NEW |
| `RULE_1` | tcp | all | anywhere 192.168.1.0/24 anywhere | tcp multiport dports hports,http state NEW |

- Chain `RULE_2` <2 references>

| target prot opt source destination |
| :--- | :--- | :--- | :--- | :--- |
| `LOG` | all | anywhere | anywhere | LOG level info prefix 'RULE 2 ' |
| `ACCEPT` | all | anywhere | anywhere |

- Chain `RULE_1` <3 references>

| target prot opt source destination |
| :--- | :--- | :--- | :--- | :--- |
| `LOG` | all | anywhere | anywhere | LOG level info prefix 'RULE 1 ' |
| `ACCEPT` | all | anywhere | anywhere |

注意，默认链具有与你在 FWBuilder 中配置的规则匹配的规则，目标为 `RULE_<规则数字>`。这些额外的链用于配置日志。所有链的开头还有一条规则用于接受与已建立会话相关的流量。这通常是理想的，但仍然可以配置。要删除此自动生成的规则，请在对象树中选择防火墙并点击

## 边界安全、DMZ、远程访问和 VPN • 第 9 章

对话框区域中的防火墙设置。有一个默认选中的复选框“在第一条规则之前接受 ESTABLISHED 和 RELATED 包（Accept ESTABLISHED and RELATED packets）”。虽然你配置的 FWBuilder 策略可以处理你可能需要的任何基础规则，但仍然有一些基础工作需要完成。如果你需要使用 Linux 防火墙进行 NAT，使用 FWBuilder 配置它非常简单。按照以下步骤操作，使防火墙将来自内部网络的所有流量 NAT 到外部接口上使用的 DHCP 地址。此配置也称为源 NAT（source nat），因为更改的是源地址。

### 1. 在对话框区域选择 NAT 选项卡。

### 2. 右键点击并选择插入规则（Insert Rule）。这将添加 NAT 号 0。

### 3. 从对象树将你的 INTERNAL 网络对象拖到 NAT 策略中的原始源（Original Source）列。

### 4. 从对象树将防火墙上的外部接口拖到 NAT 策略中的“翻译后的源（Translated Source）”列。
