

# 设置您的 vCENTER 服务器 目录结构

来源：Automating vSphere Administration

.PARAMETER FolderType
要创建的文件夹类型

.PARAMETER DC
创建文件夹结构的数据中心

.PARAMETER Filename
导入时使用的 CSV 文件路径

.EXAMPLE
Import-Folders -FolderType "Blue" -DC "DC01" 
-Filename "C:\BlueFolders.csv"

.EXAMPLE
Import-Folders -FolderType "Yellow" -DC "Datacenter" 
-Filename "C:\YellowFolders.csv" 
#>

```powershell
param(
[String]$FolderType,
[String]$DC,
[String]$Filename
)
```

```powershell
process{
$vmfolder = Import-Csv $filename | 
Sort-Object -Property Path
If ($FolderType -eq "Yellow") {
$type = "host"
} Else {
$type = "vm"
}
foreach ($folder in $VMfolder){
$key = @())
$key = ($folder.Path -split "\\")[-2]
if ($key -eq "vm") {
Get-Datacenter $dc | Get-Folder $type | 
New-Folder -Name $folder.Name
} else {
Get-Datacenter $dc | Get-Folder $type | 
Get-Folder $key | 
}
```

# 第 1 章 自动化 VCENTER 服务器的部署与配置

New-Folder -Name $folder.Name

```powershell
}
}
}
Import-Folders -FolderType "blue" -DC "DC01" ``
-Filename "C:\BlueFolders.csv"
```

# 导出目录结构

黄色和蓝色文件夹视图都可以导出到 CSV 文件。当您从头开始重建 vCenter Server 或为当前的虚拟基础设施创建灾备备（DR）副本时，你会发现这种技术非常有用。

列表 1.6 中的脚本可用于将蓝色或黄色目录结构导出到 CSV。它还可用于导出当前虚拟机的位置，以确保在导入结构时保持结构的一致性。

- 列表 1.6 将 vCenter 结构导出到 CSV 文件

```powershell
filter Get-FolderPath {
#
.SYNOPSIS
汇集完整的文件夹路径
.DESCRIPTION
该函数将查找完整的文件夹路径并返回名称和路径
.NOTES
来源：Automating vSphere Administration

#
$ | Get-View | % {
$row = "" | select Name, Path
$row.Name = $$ .Name

$current = Get-View $$ .Parent
$path = $$ .Name
do {
$parent = $$current
if($parent.Name -ne "vm") {*
```

# 设置您的 vCENTER 服务器 目录结构

```powershell
$path = $parent.Name + "" + $path
$$current = Get-View $current.Parent
} while ($current.Parent -ne $null)
$row.Path = $path
$row
```

```powershell
function Export-Folders {
<#
.SYNOPSIS
创建 vCenter Server 中文件夹的 CSV 文件。
.DESCRIPTION
该函数将从 vCenter Server 导出文件夹并添加到 CSV 文件中。
.NOTES
来源：Automating vSphere Administration
.PARAMETER FolderType
要出的文件夹类型
.PARAMETER DC
文件夹所在的数据中心
.PARAMETER Filename
导出时使用的 CSV 文件路径
.EXAMPLE
Export-Folders -FolderType "Blue" -DC "DC01" -Filename "C:\BlueFolders.csv"
.EXAMPLE
Export-Folders -FolderType "Yellow" -DC "Datacenter" -Filename "C:\YellowFolders.csv"
#>
```

```powershell
param(
[String]$FolderType,
[String]$DC,
[String]$Filename
)
nProcess {
```

```powershell
If ($Poldertype -eq "Yellow") {
  $type = "host"
} Else {
  $type = "vm"
}
$report = @())
$report = Get-Datacenter $dc | Get-Folder $type |
  Get-Folder | Get-FolderPath
$report | ForEach-Object {
    if ($type -eq "vm") {
      $_.Path = ($_.Path).Replace($dc + "\","$type\")
    }
    $report | Export-Csv $filename -NoTypeInformation
  }
}
```

```powershell
function Export-VMLocation {
#
.SYNOPSIS
  创建一个包含每个文件夹位置的 CSV 文件。
.DESCRIPTION
  该函数将从 vCenter Server 导出虚拟机位置并添加到 CSV 文件中。
.NOTES
  来源：Automating vSphere Administration
.PARAMETER DC
  文件夹所在的数据中心
.PARAMETER Filename
  导出时使用的 CSV 文件路径
.EXAMPLE
  Export-VMLocation -DC "DC01" -Filename "C:\VMocations.csv"
#>
param(
[String]$DC,
```

# 设置您的 vCENTER 服务器 目录结构

```powershell
[String]$Filename
)
Process {
  $report = @()
  $report = Get-Datacenter $dc | Get-VM | Get-FolderPath
  $report | Export-Csv $filename -NoTypeInformation
}
```

Export-Folders "Blue" "DC01" "C:\BlueFolders.csv"
Export-VMLocation "DC01" "C:\VMocations.csv"
Export-Folders "Yellow" "DC01" "C:\YellowFolders.csv"

# 导入目录结构

您可以使用列表 1.5 显示的 Import-Folders 函数将现有的蓝色或黄色目录结构导入到 vCenter 中。您还可以使用列表 1.7 显示的 Import-VMLocation 函数来选择是否将虚拟机移动到正确的文件夹中。

# 列表 1.7 将虚拟机导入到对应的文件夹

```powershell
function Import-VMLocation {
<#
.SYNOPSIS
  根据 csv 文件中的数据将虚拟机导回其文件夹中。
.DESCRIPTION
  该函数将从 CSV 文件导入虚拟机位置并将其添加到正确的文件夹中。
.NOTES
  来源：Automating vSphere Administration

.PARAMETER DC
  文件夹所在的数据中心
.PARAMETER Filename
  导入时使用的 CSV 文件路径
.EXAMPLE
Import-VMLocation -DC "DC01" -Filename "C:\VMocations.csv"
#>

param(
[String]$Filename
[String]$Filename
)

Process {
$Report = @(
$Report = Import-Csv $filename | Sort-Object -Property Path
foreach($vmpath in $Report){
$key = @(
$key = Split-Path $vmpath.Path | Split-Leaf
Move-VM (Get-Datacenter $dc \
| Get-VM $vmpath.Name) \
-Destination (Get-Datacenter $dc | Get-Folder $key)
}
}
-}
```

Import-VMLocation "DC01" "C:\VMocations.csv"

# 定义用户及其权限

对虚拟基础设施的授权通过基于角色的控制（RBAC）系统进行。vCenter 管理员可以详细指定哪些用户或组可以执行哪些操作。RBAC 系统由三个核心概念组成：

- **权限 (Privilege)**：执行操作或读取属性的能力。示例包括开启虚拟机或添加文件夹。
- **角色 (Role)**：权限的集合。角色提供了执行许多任务所需的各种权限，例如管理主机。
- **对象 (Object)**：可以执行操作的项目。vCenter 对象包括数据中心、文件夹、资源池、集群、主机和虚拟机。

