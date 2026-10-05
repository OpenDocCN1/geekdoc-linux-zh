

## 第 12 章 • 组织你的灾难恢复

这是你的清单中始终存在的对象。你可以使用 `Get-Folder` 命令来检索清单中的所有文件夹。要仅检索根文件夹，请使用 `-NoRecursion` 参数。

```
Get-Folder -NoRecursion
```

| Name | Id |
|---|---|
| Datacenters | Folder-group-d1 |

如你所见，根文件夹始终命名为 Datacenters。这是因为在这一层级，你可以创建的对象（除子文件夹外）是数据中心对象。要检索子文件夹，你需要使用根文件夹对象并将其传递给管道，以再次使用 `Get-Folder` 命令进行创建：

```
Get-Folder -NoRecursion | Get-Folder -NoRecursion
```

| Name | Id |
|---|---|
| EMEA | Folder-group-d2058 |
| US | Folder-group-d2059 |

你可以对每个子文件夹反复执行此递归过程，以检索完整的文件夹结构。这在第 12.2 列表中创建的 `Get-FolderStructure` 函数中得到了体现。

## 第 12.2 列表 检索文件夹结构

```
function Get-FolderStructure {
<#n.SYNOPSIS
  检索文件夹结构
.DESCRIPTION
  此函数检索给定容器下方的文件夹结构
.NOTES
  来源：Automating vSphere Administration
.EXAMPLE
  Get-Datacenter DC01 | Get-FolderStructure
>
```

```
process {
$folder = "" | select Name,Children
$folder.Name = $_.Name
$folder.Children = @($_ | Get-Folder -NoRecursion | \
Get-FolderStructure)
}
}
```

你只需要提供此文件夹或数据中心对象，它将会返回该对象下方的完整文件夹结构。让我们尝试一下，并在名为 `$folderStructure` 的哈希表中显示根文件夹的结构：

```
$folderStructure={}
Get-Folder -NoRecursion | Get-FolderStructure | \
%($folderStructure[$_.name] = $_.Children)
```

由于你提供了根文件夹作为输入对象，因此你检索到的是数据中心文件夹，而不是数据中心下方的文件夹。现在，使用相同的函数检索你清单中每个数据中心下方的文件夹结构。要检索数据中心，请再次使用 `Get-Datacenter` 命令。首先，查看数据中心下方的根文件夹：

```
Get-Datacenter DC01 | Get-Folder -NoRecursion
Name Id
-- ---
vm Folder-group-v2081
host Folder-group-h2082
dastore Folder-group-s2083
```

注意，返回的三个文件夹在你的清单中是不可见的。这些特殊的根文件夹就像数据中心根文件夹一样。位于 `vm` 文件夹内的虚拟机在清单中显示为蓝色文件夹。`host` 文件夹包含你的集群和主机，其子文件夹在清单中显示为黄色文件夹。`datastore` 文件夹用于数据存储。

现在，让我们再次使用 `Get-FolderStructure` 函数检索数据中心下方的文件夹结构，并将其存储在 `$folderStructure` 哈希表中：

```
Get-Datacenter | Get-Folder-Structure | %{
$folderStructure[$_.name] = $_.Children
}
```

## 第 12 章 组织你的灾难恢复

所有的文件夹结构现在都已捕获到 `$folderStructure` 哈希表中。你现在只需要将此哈希表导出为文件。存储对象合适的格式是 XML。因此，使用 `Export-Clixml` 命令将 `$folder-structure` 对象导出到 XML 文件：

```
$folderStructure | Export-Clixml C:\Export\Folders.xml
```

## 数据中心

数据中心是你清单中的一个容器，就像文件夹一样。它可以包含文件夹、集群和主机。虽然在大多数情况下，清单中只有两个数据中心对象，手动重新创建它们很快也很痛苦，但使用 PowerShell 脚本导出它们允许你在无需用户干预的情况下实现整个过程自动化。要检索数据中心，再次使用 `Get-Datacenter` 命令：

```
Get-Datacenter
```

| Name | Id |
|---|---|
| DC01 | Datacententer-datacenter-2080 |
| DC02 | Datacententer-datacenter-2 |

与数据中心一样，所有清单对象在清单中都有特定的位置。当你以后想要重建任何对象时，可以使用 `-Location` 参数指定对象的清单位置。要检索对象的完整路径，你可以使用类似列表 12.2 中 `Get-FolderStructure` 函数的方法，但你需要向上直到根文件夹。在列表 12.3 中，你将找到一个名为 `Get-VIPath` 的函数来检索路径。

## 第 12.3 列表 检索对象路径

```
function Get-VIPPath {
  <#n  .SYNOPSIS
  检索清单对象的完整路径
  .DESCRIPTION
  此函数检索给定清单对象的完整路径
  .NOTES
  来源：Automating vSphere Administration

```## 导出 VCENTER 清单项

.PARAMETER inputObject
要从中检索完整路径的清单对象
.PARAMETER childPath

函数在递归调用自身时使用的可选参数

```
.EXAMPLE
Get-Datacenter DC01 | Get-Folder
#>
Param (
  [Parameter(Mandatory=$true)]
  $inputObject,

  $childPath
)

Process {
  $inputObject = $inputObject
  $path = $inputObject.Path
  if ($childPath) {
    $path = "$path\$childPath"
  }
  return $path
}
```

img/6259 第 12 章 组织你的灾难恢复

所有的文件夹结构现在都已捕获到 `$folderStructure` 哈希表中。你现在只需要将此哈希表导出为文件。存储对象合适的格式是 XML。因此，使用 `Export-Clixml` 命令将 `$folder-structure` 对象导出到 XML 文件：

```content
$folderStructure = @()
foreach ($dc in Get-Datacenter) {
    $folderStructure[$dc.name] = $dc | Get-Folder-Structure
}
$folderStructure | Export-Clixml C:\Export\Folders.xml
```

## 数据中心

数据中心是你清单中的一个容器，就像文件夹一样。它可以包含文件夹、集群和主机。虽然在大多数情况下，清单中只有两个数据中心对象，手动重新创建它们很快也很痛苦，但使用 PowerShell 脚本导出它们允许你在无需用户干预的情况下实现整个过程自动化。要检索数据中心，再次使用 `Get-Datacenter` 命令：

```
Get-Datacenter
```

| Name | HAEnabled | Hailover | DRSEnabled |
|---|---|---|---|
| CL01 | True | 1 | False |
| CL02 | True | 1 | True |
| CL03 | False | 1 | False |

除了所有的集群属性外，你还需要知道它属于哪个数据中心，以便在正确的数据中心进行重建。为了实现这一点，首先遍历数据中心并检索集群。然后可以将数据中心添加到集群中。你可以使用 `Get-Folder` 函数来检索集群的路径。

```content
$clusters = @()
foreach ($dc in Get-Datacenter) {
    foreach ($cluster in ($dc | Get-Cluster)) {
        $clusters[$cluster.name] = $cluster 
    }
}
$clusters | Export-Clixml C:\Export\Clusters.xml
```

