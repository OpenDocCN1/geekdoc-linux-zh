
## Time periods

As the name indicates, this page lets you configure different time periods to which Nagios can refer. By default some standard time periods are already defined, such as `24x7`, work hours, and non-work hours. These can be handy if you want to monitor certain services only during certain hours.

## Groups

On this page you can configure particular groups within the GroundWork interface. These groups would contain groups of hosts, contact groups, and other settings. With these groups defined you can easily change a particular setting (such as add a new service check) and deploy it to all of the hosts within a particular group. This is really handy when you manage large numbers of hosts and want to be able to change entire groups at a time.

## Control

The control page is where you go whenever you want to commit your changes. Here you can also view the Nagios configuration and test your current changes before you commit them.

+ 工具
+ 工具页面提供了一些额外的 GroundWork 工具。在这里你可以将设置导出到文件，也可以根据模式删除一组主机或服务。
+ 性能
+ 在性能页面你可以配置图表和其他指标的选项。

## 将更改提交到 Nagios

由于 GroundWork 将其设置维护在单独的数据库中，你在 Web 界面中做的更改不会直接加载到 Nagios。只要你在 Web 界面中进行更改，就必须提交它。提交过程会将 GroundWork 的配置转换为有效的 Nagios 文件。要提交更改，请从主选项卡中选择配置，然后在页面顶部选择控制选项卡。从那里在左侧窗格中选择提交链接。你可以选择备份旧配置；否则点击提交按钮来更新 Nagios 配置并重启 Nagios。

## 配置联系人列表

在设置好初始主机集后，你需要配置一个联系人来接收警报。选择配置选项卡，然后选择联系人选项卡。点击左侧窗格中的联系人链接进行展开，显示新建、复制和修改选项。由于我们要添加一个新联系人，请点击新建。图 8-5 给出了一个联系人条目的示例。填写你的联系人信息，并手动设置通知时段和其他选项，或从下拉菜单中选择适合你的联系人模板。如果没有可用的选项适合你，你也可以从左侧窗格添加一个新的联系人模板，使用你想要的设置。我选择了 `generic-contact-2`，因为它为 `24x7` 监控提供了很好的默认设置。

GroundWork 会设置一个名为 `nagiosadmin` 的默认联系人组。GroundWork 已预先设置好的默认模板将使用此联系人组进行通知，因此如果你不想做太多调整，

![](img/304f637afcecc491b152ee8ac5afadee_344_0.png)

**图 8-5** 示例联系人属性页面

点击左侧窗格中的“联系人组”链接进行展开，点击修改，选择 `nagiosadmin` 并更改设置以将你添加到该组并删除任何默认联系人，然后点击保存。或者，你也可以创建自己的联系人组；只需确保将该组添加到你监控的主机上，这样你就能收到警报。一旦更改了所有联系人设置，记得提交更改。

## 为 Nagios 启用通知

即使你设置了联系人并且它属于正确的联系人组，默认情况下 GroundWork 也不会发送通知，直到你明确告诉它开始。这是一个很好的默认值，因为你可以先设置所有主机并调整服务检查，使一切在线后再触发通知。这样在你准备好之前就不会收到不必要的电子邮件或页面。当你准备好启用通知时，点击任何配置页面的顶部控制选项卡，然后在加载的页面左侧窗格中选择“ Nagios 主配置”

在右侧窗格中间附近你会看到一个名为“启用通知”的选项。选中该选项，然后滚动到底部点击保存并下一步。你需要点击保存并下一步通过几屏，直到看到并点击保存并完成。现在在左侧窗格中点击提交并将更改提交到 Nagios。现在你将开始向任何已配置的联系人发送警报。

> **注意** 如果你通过电子邮件设置通知，请确保你的主机已配置了功能正常的本地邮件服务器；否则通知永远也收不到。有关如何在 Ubuntu 上配置邮件服务器的更多信息，请查看第 5 章的邮件服务器部分。

## 为主机添加服务检查

对于大多数主机，你至少应该做某种 ping 探测来查看服务器是否在线。大多数人希望监控的不止于此。GroundWork 开箱即用提供了许多不同的服务检查，以及你可以参考以创建自己的自定义服务检查的命令。首先，我将带你逐步添加一个新的服务检查到主机，以检查 SSH 是否存活。

首先选择配置选项卡，然后选择主机选项卡。在左侧窗格中展开主机树，直到找到你想要更改的主机。展开该主机后，你会看到一个详细信息链接，可以点击它来配置该主机的所有设置。每组选项在右侧窗格中组织成不同的选项卡，因此点击服务选项卡来配置此主机上监控的服务。`ssh_alive` 服务可用于测试 SSH 是否可用，因此我选择该服务以及在此页面上可能想要添加的其他服务，然后点击添加服务按钮将其添加到列表中。然后点击主机详细信息选项卡，滚动到该选项卡底部，点击保存以保存更改。现在将更改提交到 Nagios 以使其生效。

## 添加新主机

要在不进行自动扫描的情况下向 GroundWork 添加新主机，请选择配置选项卡，然后点击页面顶部的 `hosts` 选项卡。在左侧窗格中，找到名为“主机向导”的链接并点击它。用主机名、别名、IP地址和

用于主机的主机配置文件。如果您尚未配置任何自定义主机配置文件，`host-profile-service-ping` 选项是一个安全的默认值。完成后，点击 `Next`。

下一页让您选择可能已配置的任何主机模板以及主机可能拥有的任何父级。选择 `generic-host` 模板，除非您已设置自定义模板。`parents` 字段让您选择先前配置的主机作为此主机的父级。当一台主机是另一台主机的父级时，如果它宕机，Nagios 也会将子主机视为宕机。这有助于您从网络设备到主机构建依赖树。如果您不确定要配置哪些父级，留空也可以。

在下一页中，您可以将新主机分配给已定义的主机组。如果您想使用 Nagios 的映射功能，也可以在此处输入地图坐标。此页面也是您在已定义的情况下选择任何升级树的地方。如果您刚开始使用，您可能会将这些选项大部分留空。

下一页是配置在此主机上要监控哪些服务的地方。如果您配置了任何服务配置文件，可以在此处添加它们；否则您可以手动选择服务。点击 `Next` 后，您将到达向导的最后一页。您可以选择将所有设置保存为配置文件。如果您知道要对一组主机重复此向导，并且它们将具有相同的选项集，这会很有用。您可以将其保存为配置文件，然后在添加下一台主机时选择它。点击 `Continue` 完成向 GroundWork 添加主机。完成后不要忘记提交您的更改。

## 高级配置

Nagios 中的选项实在太多，无法在此全部描述，但我讨论了一些原则，这些原则将在您浏览漫长的设置列表时有所帮助。我从主机设置开始，然后描述如何在 GroundWork 中添加新的自定义服务检查。

当您查看主机的自定义选项时，您会注意到每个选项左侧都有一个复选框；右侧有一个复选框、下拉菜单或文本输入框；以及一个小问号。图 8-6 显示了示例主机配置页面。右侧的复选框、文本输入或菜单会显示特定设置的当前状态。

左侧的复选框告诉您此特定设置当前是否从模板获取其值。如果该框被选中，您将无法手动更改该设置。当您更改它并保存更改时，您会注意到它会恢复为模板中设置的内容。因此，如果您想覆盖设置，请取消选中左侧的复选框；只是要意识到，如果您在模板中更新该选项，它将不再传递给此主机。一般来说，除非您要做例外，否则使用模板进行更改比逐个主机进行更改更简单。

问号伴随着 GroundWork 中的大多数配置选项，如果您将鼠标悬停在其上，您将获得对特定选项的更深入解释。选项如此之多，像这样的提示绝对派上用场。

您也可以覆盖主机上特定服务检查的默认设置。只需在主机下方的左侧窗格中点击该服务检查，然后

![](img/304f637afcecc491b152ee8ac5afadee_347_0.png)

图 8-6 GroundWork 主机配置选项
