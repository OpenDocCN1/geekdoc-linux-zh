
`bash#tail -f /var/log/messages`

```
```

- 3. 从菜单中选择 System Administration, Integrate Hardware into the System, Configure ISDN Hardware。YaST ISDN 设置窗口出现（见图 23.14）。

FIGURE 23.14
YaST ISDN hardware setup menu.

![](img/659f91d9da7b29976c0625e2e9628511_460_0.png)

- 4. 从此对话框中，您需要输入以下详细信息：
  - Start I4L—如果您想激活 ISDN，请勾选此框，您确实需要这样做。
  - ISDN Protocol—此框指示您的电话公司使用哪种 ISDN。Euro-ISDN (EDSS1) 对大多数用户来说是合适的，但 1TR6 可能是许多德国用户的选择。如果您不知道电话公司使用哪一种，您应该联系他们或进行一些试错检查。
  - Type of ISDN Card—从此列表中选择您的 ISDN 控制器。如果您在列表中找不到您的 ISDN 控制器，请选择 Generic ISDN Controller。
  - Controller identification—保持此框不变。
  - Interrupt—从您之前获得的设置中填写此值。如果您有 PnP 卡，您应该从 `/etc/isapnp.conf` 文件中获取此值以及 ISAC 和 HSCX。
  - Memory Base Address—从您之前获得的设置中填写此值。如果您有 PnP 卡，您应该从 `/etc/isapnp.conf` 文件中获取此值以及 ISAC 和 HSCX。
  - IO Port—从您之前获得的设置中填写此值。
  - Values of IO0 and IO1—如果您有 PnP ISDN 控制器，您将在 `/etc/isapnp.conf` 文件中找到这些值。
  - ISDN Module Options—此框在大多数情况下应保持为空。

填写完值后，按 Start。如果一切顺利，按 Save。如果出现问题，请通过查看之前打开的终端来检查内核消息。您可以考虑以下事项：
- **模块可能已在内存中加载**—如果您已在内存中加载了 HiSax 模块，您应该先卸载它，然后使用您刚刚设置的新设置启动它。为此，您必须输入以下内容：

```
bash# rmmod hisax.
```

然后再次按 Start。
- **IRQ 设置不正确**—不要使用 IRQ 12 或 15。不要允许您的 ISDN 控制器与 IRQ 共享。

## 其他 ISDN 配置

ISDN 可以做一些 YaST 尚未配置的事情。一个 YaST 未配置的重要功能是日志记录。另一个重要功能是检查来电显示。结合起来，它们对于拨入和故障排除很重要。

### 设置日志记录

`isdnlog` 的配置文件是 `/etc/isdn/isdnlog.conf`。此文件必须根据您的电话公司进行配置。GLOBAL 部分的主要输入如下：
- `COUNTRYPREFIX`—输入此值是可选的：您可以保持原样。国家前缀的默认值是 = +。
  `COUNTRYPREFIX = +`
- `COUNTRYCODE`—此值也是可选的。
- `AREACODE`—这是本节中最重要的。此值等于去掉前导零后的区号。这意味着如果您的区号是 0111，您应该输入 111。

`isdnlog` 选项位于 `/etc/isdn/isdnlog/isdnctrlx.options`。您可以通过设置此文件中的选项来设置记录 ISDN 活动的灵敏度。通常，这是不必要的。

### 设置来电显示

来电显示的配置文件是 `/etc/isdn/callerid.conf`。此文件的格式非常简单：

```
[MSN]

Number=      #Number of the caller

Alias=       #Name of the caller

Zone=        #Zone of the caller
```
