

# 图 24.46 在 Windows 资源管理器中向仓库添加代码

![](img/62596f5acc979040608a4e5111beb7d6_915_0.png)

打开 SourceTree 客户端并导航到 Test01 仓库。在“文件状态”（File Status）选项卡中，注意 Test-Function01.ps 文件列在“未暂存”（Unstaged Files）下（图 24.47）。

# 图 24.47 SourceTree 文件状态

![](img/62596f5acc979040608a4e5111beb7d6_915_1.png)

点击 *Test-Function01.ps1* 文件旁复选框，文件将移动到“已暂存”（Staged Files）区域。输入提交消息并选择“立即推送到 Origin/Master”（Push Changes Immediately To Origin/Master）（图 24.48）。点击“提交”（Commit）按钮。如果你之前没有提供 GitHub 账户的凭据，此时可能会提示你输入。

输入提交消息并点击“立即推送到 Origin/Master”。

**图 24.48**

![](img/62596f5acc979040608a4e5111beb7d6_916_0.png)

## 更新仓库中的代码

代码存储在项目后，很可能在某个时间点，代码会根据本地系统的更改而进行更新，这些更改需要提交到仓库。我们对 *Test-Function01.ps1* 文件进行修改，作为提交更新的示例。

导航到 SourceTree 中的“文件”（File）选项卡，观察发现 *Test-Function01.ps1* 文件已回到“未暂存”区域，并且在代码区域，新添加的额外代码行以绿色显示（图 24.49）。

# 第 24 章 · 控制

### 24.49 我们添加的代码行以绿色高亮。

![](img/62596f5acc979040608a4e5111beb7d6_917_0.png)

点击 Test-Function01.ps1 文件旁复选框，它将移动到“已暂存”区域。输入提交消息并勾选“立即推送到 Origin/Master”。点击“提交”按钮。

### 24.50 更新仓库中的代码

![](img/62596f5acc979040608a4e5111beb7d6_917_1.png)

## 检查仓库中的更改

与他人在同一个代码项目上工作意味着他们可能会对代码进行更改，就像我们刚刚演示的那样。以这种方式工作时，定期用其他人在项目中所做的任何更改更新你的本地系统非常重要。对于此示例，来自另一个系统（通过另一个用户）对仓库代码的某些更改更新了 Test-Function01.ps1 文件，并添加了一个新文件 Test-Function02.ps1。使用 SourceTree 而非 TortoiseSVN 的优势在于，当仓库中有待处理更改时，它会在你的系统上显示——查看拉取（Pull）工具按钮上方包含更改数量的红色通知。

要用这些更改更新你的本地系统，点击工具栏上的“拉取”（Pull）按钮然后点击“确定”（图 24.51）。

图 24.51 检查仓库中的更改

![](img/62596f5acc979040608a4e5111beb7d6_918_0.png)

> **提示** 注意，当你在有多个贡献者的项目上工作时，可能有多人在提交更改之间更新、移动或删除同一个代码文件。查看视频“使用 SourceTree  Git 冲突”了解如何处理可能出现的冲突：https://vimeo.com/73802696

## 回滚仓库中的更改

假设你想回到代码文件的早期版本。GitHub 支持此需求。你可以使用 SourceTree 客户端进行 Git 回滚，并将代码恢复到之前的良好版本。在本示例中，我们将 Test-Function01.ps1 文件回滚到初始版本。

从 SourceTree 客户端导航到“文件状态”选项卡，并将视图更改为“所有文件”（All Files）➤ 排序状态（Sorted Status）。右键点击 Test-Function01.ps1 文件并选择“日志”（Log）（图 24.52）。

# 图 24.52 回滚仓库中的更改

![](img/62596f5acc979040608a4e5111beb7d6_919_0.png)

当日志打开时，查看此文件的不同版本以及注释和更改。右键点击你想回滚的版本并选择“重置到提交”（Reset To Commit）（图 24.53）。

# 图 24.53 重置到提交

![](62596f5acc979040608a4e5111beb7d6_920_0.)

点击“确定”确认重置（图 24.54）。

# 图 24.54 点击确定。

![](62596f5acc979040608a4e5111beb7d6_920_1.png

你可以验证 `Test-Function01.ps1` 文件已回滚到你通过 `Write-Host` 选择的内容：

```
Get-Content C:\GitHub\Test01\Test-Function01.ps1
```
```powershell
function Test-Function01 {
    Write-Host "This is test 1"
}
```

此本地更改需要提交到仓库，使其成为所有人（目前的）最终版本。导航到“文件状态”选项卡，将视图切换回“待处理文件”（Pending Files），并验证 `Test-Function01.ps1` 文件位于“未暂存”区域（图 24.55）。

# 第 24 章 · 控制

# 图 24.55 验证 Test-Function01.ps1 文件在“未暂存”区域。

![](img/62596f5acc979040608a4e5111beb7d6_921_0.png

点击 Test-Function01.ps1 文件旁复选框，它将移动到“已暂存”区域。输入提交消息并选择“立即推送到 Origin/Master”。点击“提交”按钮（图 24.56）。

# 图 24.56 点击提交回滚仓库中的更改。

![](img/62596f5acc979040608a4e5111beb7d6_921_1.png

## 从仓库移除代码

最后，在这一系列仓库操作中，让我们如何从仓库中移除 Test-Function02.ps1 文件。

导航到 C:\GitHub\Test01 文件夹并删除 Test-Function02.ps1 文件。在 SourceTree 客户端中，导航到“文件状态”选项卡，验证 Test-Function02.ps1 文件位于“已暂存”文件，并带有一个红色图标（图 24.57）。

图 24.57 删除文件后检查文件状态

![](img62596f5acc979040608a4e5111beb7d6_922_0.png

点击 Test-Function02.ps1 文件旁复选框，它将移动到“已暂存”区域。输入提交消息并选择“立即推送到 Origin/Master”。点击“提交”按钮（图 24.58）。

# 图 24.58 点击提交从仓库中移除文件。

![](62596f5acc979040608a4e5111beb7d6_923_0.png

## 使用 PowerShell 自动化 GitHub 客户端操作

我们正在使用的 SourceTree 客户端实际上是通过作为 SourceTree 客户端安装一部分的 Git 命令行工具来为 GitHub 执行命令。如果你在客户端中提交更改（例如）时查看完整输出，可能会注意到列出的这些命令。在 SourceTree 客户端中，可以打开终端窗口使用这些工具管理仓库中的代码。终端窗口包含许多视觉增强（包括颜色），以提供更好的体验。其中某些功能在 PowerShell 控制台中是不可用的。然而，PowerShell 社区伸出了援手，通过使用一个名为 posh-git 的知名项目，你可以将这些功能带到 PowerShell 控制台中。

## 要求

你需要以下内容：

- 预安装的 Git 命令行工具。你可以从 http://git-scm.com/download/win 获取。
- posh-git，可以从 dahlbyk.github.io/posh-git/ 获取。

## 安装 Git 命令行工具

在下载的安装过程中，接受所有默认设置，修改 Windows PATH 环境变量除。在命令提示符中选择使用 Git（图 24.59）。

**图 24.59 安装 Git 命令行工具**

![](62596f5acc979040608a4e5111beb7d6_924_0.png

## 安装 posh-git

安装-git 最简单的方法是通过 PsGet (http://psget.net)，这是一个管理 PowerShell 模块的工具。你可以通过以下两行代码安装 PsGet 以及后续 posh-git。请确保在具有管理员权限的 PowerShell 会话中运行这两行：

```powershell
(New-Object Net.WebClient).DownloadString("http://psget.net/GetPsGet.ps1") | Invoke-Expression
Install-Module posh-git
```

安装成功后，**pos-git** 将自动激活位于 Git 仓库文件夹中的 PowerShell 控制台。会出现提示颜色，Git 命令的 Tab 补全功能将可用（图 24.60）。

**图 24.60 激活了 posh-git 的 PowerShell 控制台**

```
C:\GitHub\Test (master *)> git status
(on branch master)
Your branch is up-to-date with 'origin/master'.
Untracked files:
  "git add <file>" to include in what will be committed
Test-Function03.ps1
nothing to commit untracked files present (use "git add" to track)
```
