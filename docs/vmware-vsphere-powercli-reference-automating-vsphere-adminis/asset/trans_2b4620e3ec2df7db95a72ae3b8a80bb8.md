

# 导入 VCENTER 服务器清单项 431

```powershell
{ Write-Host "$_ on $($row.Host) added Successfully" `
-ForegroundColor Green } else { Write-Host "It Appears `
that $($) on $($row.Host) was not added successfully to `
($($).Switch" -ForegroundColor Red }
```

# 标签 (Tags)

标签和标签类别可以随时导入到 vCenter Server。然而，在尝试重新创建标签关系之前，您需要确保所有的虚拟对象已填充到 vCenter 中；否则您将收到错误。标签将无法找到其关联的对象。列表 12.11 包含一个函数，可以帮助您导入在本章之前导出的标签和标签类别。

![](img/62596f5acc979040608a4e5111beb7d6_462_0.png)

# 列表 12.11 导入标签和标签类别

```powershell
function Import-Tag {
#
.SYNOPSIS
导入标签和标签类别
.DESCRIPTION
此函数从 vCenter 导出标签和标签类别
.NOTES
Source: Automating vSphere Administration
.PARAMETER Path
函数使用的强制性参数，用于确定标签文件的源。
.EXAMPLE
Import-Tag -Path C:\Temp\TagData.xml
#
[CmdletBinding()]
Param (
[Parameter(Mandatory = $True, Position = 1)]
[string]$Path
```

# 第三部分

# 第 12 章组织您的灾难恢复

```powershell
# 从文件导入数据
$data = Import-Clixml -Path $Path
```

```powershell
# 将输入分为标签和类别的独立列表
$categoryList = $data[0]
$tags = $data[1]
```

```powershell
# 类别数组
$categories = @()
```

```powershell
# 导入每个类别
foreach ($category in $categoryList) {
$categories += New-TagCategory \
-Name $category.Name \
-Description $category.Description \
-Cardinality $category.Cardinality \
-EntityType $category.EntityType \
-Out-Null
}
```

```powershell
# 创建每个标签
foreach ($tag in $tags) {

# 添加到对应的标签类别
$category = $categories | Where-Object { $_.Name -eq $tag.Category.Name }
if ($category -eq $null) { $category = $tag.Category.Name }

New-Tag -Name $tag.Name -Description $tag.Description \
-Category $category
}
```

一旦创建了标签和标签类别，您就可以使用列表 12.12 中的函数将对象与其原始标签关联。在编写此时，如果您在 vCenter Server 中的那两个对象中的任一上有标签，您将需要手动添加标签。

# 列表 12.12 添加标签-对象关系

```powershell
function Import-TagRelationship {
<#n.SYNOPSIS
为 vSphere 对象导入标签-对象关系
.DESCRIPTION
此函数将标签恢复到 vSphere 对象
.NOTES
Source: Automating vSphere Administration
.PARAMETER Path
函数使用的参数，用于定位导入文件
.EXAMPLE
Import-TagRelationship -Path c:\temp\TagRelationship.csv
#>
[CmdletBinding()]
Param (
[Parameter(Mandatory = $True, Position = 1)]
[string]$Path
)

#导入数据文件
$csv = Import-Csv -Path $Path

$csv | ForEach-Object {
$tagcat = $_.Category

$tag = Get-Tag -Name $_.Tag | Where-Object { $_.Category -like
$tagcat }
$entity = $_.Entity
switch ($type) {
"Cluster" { Get-Cluster -Name $tag |
New-TagAssignment -Tag $tag }
"Datacenter" { Get-Datacenter -Name $entity |
New-TagAssignment -Tag $tag }
"Datastore" { Get-Datastore -Name $entity |
New-TagAssignment -Tag $tag }
"DatastoreCluster" { Get-DatastoreCluster
-Name $Entity | New-TagAssignment -Tag $tag }
-"DistributedPortGroup" { Get-VDPortgroup \
-Name $Entity | New-TagAssignment -Tag $tag }
-"DistributedSwitch" { Get-VDSwitch \
-Name $Entity | New-TagAssignment -Tag $tag }
-"Folder" { Get-Folder -Name $Entity | \
New-TagAssignment -Tag $tag }
-"Host" { Get-VMHost -Name $Entity | \
New-TagAssignment -Tag $tag }
-"Network" { Get-VirtualSwitch -Name $Entity | \
New-TagAssignment -Tag $tag }
-"ResourcePool" { Get-ResourcePool -Name $Entity | \
New-TagAssignment -Tag $tag }
-"vApp" { Get-VApp -Name $Entity | \
New-TagAssignment -Tag $tag }
-"vCOScheduledWorkflow" { Write-Host "$Entity is a \
vCOScheduledWorkflow and will need to be tagged \
manually with: ("$tag") -ForegroundColor Red }
-"vCOWorkflow" { Write-Host "$Entity is a vCOWorkflow \
will need to be tagged manually with: ("$tag") -ForegroundColor Red }
-"VirtualMachine" { Get-VM -Name $Entity | New-TagAssignment -Tag $tag }
}
}
}
```

[/content] 

抱歉，我注意到在处理翻译时漏掉了您提供的最后的待翻译文本内容。以下是修正后的完整翻译：

[content]

# 导入 VCENTER 服务器清单项 431

```powershell
{ Write-Host "$_ on $($row.Host) added Successfully" `
-ForegroundColor Green } else { Write-Host "It Appears `
that $($) on $($row.Host) was not added successfully to `
($($).Switch" -ForegroundColor Red }
```

# 标签 (Tags)

标签和标签类别可以随时导入到 vCenter Server。然而，在尝试重新创建标签关系之前，您需要确保所有的虚拟对象已填充到 vCenter 中；否则您将收到错误。标签将无法找到其关联的对象。列表 12.11 包含一个函数，可以帮助您导入在本章之前导出的标签和标签类别。

![](img/62596f5acc979040608a4e5111beb7d6_462_0.png)

# 列表 12.11 导入标签和标签类别

```powershell
function Import-Tag {
#
.SYNOPSIS
导入标签和标签类别
.DESCRIPTION
此函数从 vCenter 导出标签和标签类别
.NOTES
Source: Automating vSphere Administration
.PARAMETER Path
函数使用的强制性参数，用于确定标签文件的源。
.EXAMPLE
Import-Tag -Path C:\Temp\TagData.xml
#
[CmdletBinding()]
Param (
[Parameter(Mandatory = $True, Position = 1)]
[string]$Path
```

# 第三部分

# 第 12 章组织您的灾难恢复

```powershell
# 从文件导入数据
$data = Import-Clixml -Path $Path
```

```powershell
# 将输入分为标签和类别的独立列表
$categoryList = $data[0]
$tags = $data[1]
```

```powershell
# 类别数组
$categories = @()
```

```powershell
# 导入每个类别
foreach ($category in $categoryList) {
$categories += New-TagCategory \
-Name $category.Name \
-Description $category.Description \
-Cardinality $category.Cardinality \
-EntityType $category.EntityType \
-Out-Null
}
```

```powershell
# 创建每个标签
foreach ($tag in $tags) {

# 添加到对应的标签类别
$category = $categories | Where-Object { $_.Name -eq $tag.Category.Name }
if ($category -eq $null) { $category = $tag.Category.Name }

New-Tag -Name $tag.Name -Description $tag.Description \
-Category $category
}
```

一旦创建了标签和标签类别，您就可以使用列表 12.12 中的函数将对象与其原始标签关联。在编写此时，如果您在 vCenter Server 中的那两个对象中的任一上有标签，您将需要手动添加标签。

# 列表 12.12 添加标签-对象关系

```powershell
function Import-TagRelationship {
<#n.SYNOPSIS
为 vSphere 对象导入标签-对象关系
.DESCRIPTION
此函数将标签恢复到 vSphere 对象
.NOTES
Source: Automating vSphere Administration
.PARAMETER Path
函数使用的参数，用于定位导入文件
.EXAMPLE
Import-TagRelationship -Path c:\temp\TagRelationship.csv
#>
[CmdletBinding()]
Param (
[Parameter(Mandatory = $True, Position = 1)]
[string]$Path
)

#import数据文件
$csv = Import-Csv -Path $Path

$csv | ForEach-Object {
$tagcat = $_.Category

$tag = Get-Tag -Name $_.Tag | Where-Object { $_.Category -like
$tagcat }
$entity = $_.Entity
switch ($type) {
"Cluster" { Get-Cluster -Name $tag |
New-TagAssignment -Tag $tag }
"Datacenter" { Get-Datacenter -Name $entity |
New-TagAssignment -Tag $tag }
"Datastore" { Get-Datastore -Name $entity |
New-TagAssignment -Tag $tag }
"DatastoreCluster" { Get-DatastoreCluster
-Name $Entity | New-TagAssignment -Tag $tag }
-"DistributedPortGroup" { Get-VDPortgroup \
-Name $Entity | New-TagAssignment -Tag $tag }
-"DistributedSwitch" { Get-VDSwitch \
-Name $Entity | New-TagAssignment -Tag $tag }
-"Folder" { Get-Folder -Name $Entity | \
New-TagAssignment -Tag $tag }
-"Host" { Get-VMHost -Name $Entity | \
New-TagAssignment -Tag $tag }
-"Network" { Get-VirtualSwitch -Name $Entity | \
New-TagAssignment -Tag $tag }
-"ResourcePool" { Get-ResourcePool -Name $Entity | \
New-TagAssignment -Tag $tag }
-"vApp" { Get-VApp -Name $Entity | \
New-TagAssignment -Tag $tag }
-"vCOScheduledWorkflow" { Write-Host "$Entity is a \
vCOScheduledWorkflow and will need to be tagged \
manually with: ("$tag") -ForegroundColor Red }
-"vCOWorkflow" { Write-Host "$Entity is a vCOWorkflow \
will need to be tagged manually with: ("$tag") -ForegroundColor Red }
-"VirtualMachine" { Get-VM -Name $Entity | New-TagAssignment -Tag $tag }
}
}
}
```

# 第 12 章组织您的灾难恢复

# 恢复虚拟机

如果您丢失了注册信息，可以使用 CLI 恢复它们。当您必须将对象移动到新的 vCenter 或标签数据库损坏时，这非常有用。

以下示例显示了如何使用 CSV 文件重新应用标签。

```powershell
Import-TagRelationship -Path C:\Temp\Tags.csv
```

