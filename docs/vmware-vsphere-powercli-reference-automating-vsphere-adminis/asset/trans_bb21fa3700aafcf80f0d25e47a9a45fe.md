
APACHE SUBVERSION 861

为了完整起见，回到 C:\Code\Project01\trunk 文件夹，验证 `Test-Function01.ps1` 文件现在是否显示为带有绿色勾标记的图标，并确认该文件没有任何需要提交到项目的待处理更改（图 24.26）。

# 图 24.26 确认没有待处理的更改。

![](img/62596f5acc979040608a4e5111beb7d6_892_0.png)

## 使用 TortoiseSVN 检查项目中的更改

在同一个代码项目上与其他人工作意味着他们可能也会对代码进行更改。以这种方式工作时，定期更新本地系统以获取其他人在项目中做的任何更改是非常重要的。为了继续此示例，请使用另一个系统通过与已使用的不同的用户账户连接到此项目，并进行一些更改。我们以另一个用户登录并增加了一行 `Write-Host` 进行更新：

```powershell
function Test-Function01 {
    Write-Host "This is test 01"
    Write-Host "This is test 01"
    Write-Host "This is test 01"
}
```

PowerCLI 和 DevOps 第六

回到 C:\Code\Project01\trunk 文件夹，观察新文件 `Test-Function02.ps1` 是否存在，并且两个文件都显示为绿色勾标记图标（图 24.29）。

# 图 24.28 更新完成

![](img/62596f5acc979040608a4e5111beb7d6_894_0.png)

# 图 24.29 更新后，两个文件都显示为绿色勾图标。

![](img/62596f5acc979040608a4e5111beb7d6_894_1.png)

你可以通过查看 TortoiseSVN 提交日志验证其他用户对这些文件进行的更改。在 C:\Code\Project01\trunk 文件夹中右键点击并选择 TortoiseSVN ➤ 显示日志（Show Log）。当日志对话框打开时，观察更改和任何相关的注释。在示例中，我们的用户 xander.harris 添加了新文件 `Test-Function02.ps1` 并对现有的文件 `Test-Function02.ps1` 进行了更改（图 24.30）。

# 第 24 章 • 源码

# 图 24.30 检查提交日志

![](img/62596f5acc979040608a4e5111beb7d6_895_0.png)

除了依赖注释，你还可以通过查看版本之间的差异来识别更改。我们右键点击 `Test-Function01.ps1` 文件并选择“与之前的版本对比 SVN 差异（Diff SVN With Previous Version）”。文件版本 4 与当前版本之间的差异如图 24.31 所示。增加了一行 `Write-Host`。

# 图 24.31 观察版本之间的差异

![](img/62596f5acc979040608a4e5111beb7d6_895_1.png)

提示：在与多人协作的项目工作时要留心，在项目提交更改之间，可能有多于一个人更新、移动或删除了同一个代码文件。请参阅 TortoiseSVN 网站上关于解决冲突的信息，以了解如何处理可能发生的任何冲突：http://tortoisesvn.net/docs/release/TortoiseSVN_en/tsvn-dug-conflicts.html。

## 在 TortoiseSVN 中回滚更改

有许多原因导致需要对已提交的代码进行回滚。例如，代码更改可能没有经过充分测试并随后导致了问题，或者可能是功能需求发生了变化。使用 TortoiseSVN 客户端，你可以将代码回滚到先前的已知版本。

在本示例中，我们将把 `Test-Function01.ps1` 文件从版本 5 回滚到版本 3。

导航到 C:\Project01\trunk 文件夹，右键点击 `Test-Function01.ps1` 文件并选择 TortoiseSVN > 显示日志（Show Log）。在日志对话框中，右键点击版本 3，从大量的选项中选择“回滚到此版本（Revert To This Revision）”（图 24.32）。

# ## 24.32 回滚项目中的更改

![](img/62596f5acc979040608a4e5111beb7d6_896_0.png)

* 注意*

第 24 章 • 源码

在“回滚更改（Reverting Changes）”对话框中，选择“回滚 Test-Function01.ps1 的所有更改”并返回版本 3（图 24.33）。

# 图 24.33 回滚确认

![](img/62596f5acc979040608a4e5111beb7d6_897_0.png)

当“合并完成（Merge Finished）”对话框打开时，观察更改（图 24.34）。

# 图 24.34 合并！

![](img/62596f5acc979040608a4e5111beb7d6_894_1.png)

注意：在此处我们已经回滚了本地。检查 `Test-Function01.ps1` 的内容，确认版本 5 添加的 `Write-Host` 已删除：

```powershell
function Test-Function01 {
    Write-Host "This is test 01"
    Write-Host "This is test 01"
    Write-Host "This is test 01"
}
```

如果你能看到想要保留的代码，需要将其提交到项目。导航到 C:\Code\Project01\trunk 文件夹，右键点击 `Test-Function01.ps1` 并选择提交。当提交对话框打开时，观察更改摘要（图 24.35）。

# 24.35 版本号已递增。

![](img/62596f5acc979040608a4e5111beb7d6_894_0.png)

## TortoiseSVN 从项目中删除代码

我们已经涵盖了添加、更新和回滚。为了结束工作，让我们看看删除操作。在 C:\Code\Project01\trunk 文件夹中，右键点击 `Test-Function02.ps1` 文件并选择 TortoiseSVN ➤（图 24.36）。

# 图 24.36 从项目中删除代码

![](img/62596f5acc979040608a4e5111beb7d6_898_0.png)

第 24 章 • 源码

# 图 24.37 点击确定以提交删除。

![](img/62596f5acc979040608a4e5111beb7d6_899_0.png)

现在你需要向项目提交删除。在 C:\Code\Project01\trunk 文件夹的空白处右键点击并选择 SVN 提交（Commit）。当提交对话框打开时，添加一条说明删除的消息（图 24.38）。

# 24.38 我们到了版本 7！

![](img/62596f5acc979040608a4e5111beb7d6_900_1.png)

> 提示：如果另一个用户意外删除了你的代码并提交了更改，不要恐慌。只需打开日志并将项目回滚到代码存在的版本。

## 使用 VisualSVN 服务器浏览器界面

VisualSVN 包含一个用于操作 VisualSVN 仓库的浏览器界面。要访问它，导航到 https://servername 并使用访问仓库的凭据登录。虽然功能有限，但它可以用于参考。如图 24.39 所示，点击“历史（History）”按钮可以深入项目并查看更改历史。

**图 24.39 在 VisualSVN 服务器界面中，你可以查看项目历史。**

![](img/62596f5acc979040608a4e5111beb7d6_901_0.png)

## 使用 PowerShell 自动化 VisualSVN Server

目前所有的 SVN 操作都是通过 GUI 工具完成的。你会高兴的，可以通过命令行与 SVN 工作。VisualSVN Server 管理控制基于基于 Windows 的 WMI 接口。因此可以使用 PowerShell 自动化任务。

> 提示：在 VisualSVN Server 上使用 WMI 探器工具（例如来自 http://wmie.codplex.com/ 的 WMI Explorer）来检查 root\VisualSVN WMI 命名空间中的可用类，并确定哪些是可以自动化的。在本节中，我们只是冰山一角。

列表 24.1 和列表 24.2 中的 `New-VisualSVNRepository` 和 `Set-VisualSVNADecurity` 函数使用了 root\VisualSVN WMI 命名空间，将使你能够

