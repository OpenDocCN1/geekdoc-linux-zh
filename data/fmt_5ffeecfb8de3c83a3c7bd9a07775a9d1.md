
```powershell
Health = $VSANHostStatus.Health

NodeState = $VSANHostStatus.NodeState

NodeUUID = $VSANHostStatus.NodeUUID

VSANClusterUUID = $VSANHostStatus.Uuid

}

Write-Output $Object

}

catch [Exception] {

throw "Unable to get VMHost VSAN Status"

}
```

该函数的典型用法类似于下面的示例：

```powershell
PS C:\> Get-Cluster 'VSAN01' | Get-VMHost | Get-VMHostVSANStatus

Name : vsanesxi01.sunnydale.local

Health : healthy

NodeState : agent

NodeUUID : 54d240a0-c96a-13f9-2382-0050568aa2a0

VSANClusterUUID : 526c9db1-800a-052b-7dfd-8a7775ef0d01

Name : vsanesxi02.sunnydale.local

Health : healthy

NodeState : backup

NodeUUID : 54d241bb-8b28-19d6-b97c-0050568a354d

VSANClusterUUID : 526c9db1-800a-052b-7dfd-8a7775ef0d01

Name : vsanesxi03.sunnydale.local

Health : healthy

NodeState : master

NodeUUID : 54d24201-dd98-cc4e-52bb-0050568a9c59

VSANClusterUUID : 526c9db1-800a-052b-7dfd-8a7775ef0d01
```

列表 4.31 中的 `Get-VMHostVSANDDisks` 是一个查询配置了 vSAN 的 ESXi 主机上使用的磁盘状态的函数。

### 列表 4.31 `Get-VMHostVSANDiskDetails`

```powershell
function Get-VMHostVSANDiskDetails {

.SYNOPSIS

获取 ESXi Host 的 VSAN 磁盘详情

.DESCRIPTION

获取 ESXi Host 的 VSAN 磁盘详情

.PARAMETER VMHost

一个 vSphere ESXi Host 对象

.INPUTS

VMware.VimAutomation.ViCore.Impl.V1.Inventory.VMHostImpl

.OUTPUTS

System.Management.Automation.PSObject.

.EXAMPLES>

Get-VMHostVSANDiskDetails -VMHost ESXi01,ESXi02

.EXAMPLE

PS> Get-VMHost ESXi01,ESXi02 | Get-VMHostVSANDiskDetails

[CmdletBinding()]

[OutputType('System.Management.Automation.PSObject')]

Param

[parameter(Mandatory=$true,ValueFromPipeline=$true)]

[ValidateNotNullOrEmpty()]

[PSObject []]$VMHost

)

begin {

# --- Import VMware Storage Module

try {

  if (-not (Get-Module VMware.VimAutomation.Storage)) {

    Import-Module VMware.VimAutomation.Storage \

    -ErrorAction Stop | Out-Null

  }

  Write-Verbose "Successfully imported the VMware \

  Storage Module"

} catch [Exception] {

  throw "Unable to import the VMware Storage Module"

}

$OutputObject = @()

process {

  try {

  foreach ($ESXiHost in $VMHost) {

    if ($ESXiHost.GetType().Name -eq "string") {

      try {

        $ESXiHost = Get-VMHost $ESXiHost -ErrorAction Stop

      }

      catch [Exception] {

        Write-Warning "VMHost $ESXiHost does not exist"

        continue

      }

    }

  }

  elseif ($ESXiHost -isnot [VMware.Vim.Automation.ViCore.Impl.V1.Inventory.VMHostImpl]) {

    Write-Warning "You did not pass a \

    string or a VMHost object"

    continue

  }

}

# --- Get VSAN Disks of Host

$VSANDisks = Get-VsanGroup -VMHost $ESXiHost

# --- Get VSAN Disk Details

$VMHostView = Get-View $ESXiHost \

-Property Name,ConfigManager.VsanSystem

$VSANSystem = Get-View \

-Id $VMHostView.ConfigManager.VsanSystem

foreach ($Disk in $VSANDisks) {

  $VSANDisk = $VSANSystem.QueryDiskForVsan($Disk.CanonicalName)

  # --- Create Output Object

  $Object = [pscustomobject@{

    Host = $ESXiHost.Name

    DisplayName = $VSANDisk.DisplayName

    Vendor = $VSANDisk.Vendor

    Model = $VSANDisk.Model

    CanonicalName = $VSANDisk.CanonicalName

    LocalDisk = $VSANDisk.LocalDisk

    SSD = $VSANDisk.SSD

    State = $VSANDisk.State

    QueueDepth = $VSANDisk.QueueDepth

    Uuid = $VSANDisk.Uuid

    SerialNumber = $VSANDisk.SerialNumber

  }]

  $OutputObject += $Object

}

catch [Exception] {

  throw "Unable to get VMHost VSAN Disk Details"

}
```

该函数的典型用法类似于下一个示例（为了简洁进行了省略）：

```powershell
PS C:\> Get-Cluster 'VSAN01' | Get-VMHost | Get-VMHostVSANDetails

Host : vsanesxi01.sunnydale.local

DisplayName : VMware Disk(naa.600029ca9f33c5241dc6a77a)

Vendor : VMware

Model : Virtual disk

CanonicalName : naa600029ca9f33c5241dc6a77a

LocalDisk : True

SSD : False

State : inUse

QueueDepth : 32

Uuid : 020000000600029ca9f33c5241dc6a77a

SerialNumber : unavailable

Host : vsanesxi01.sunnydale.local

DisplayName : VMware Disk(naa.600029bb4ca80c4be819e6420)

Vendor : VMware

Model : Virtual disk

CanonicalName : naa600029bb4ca80c4be819e6420

LocalDisk : True

SSD : False
```
