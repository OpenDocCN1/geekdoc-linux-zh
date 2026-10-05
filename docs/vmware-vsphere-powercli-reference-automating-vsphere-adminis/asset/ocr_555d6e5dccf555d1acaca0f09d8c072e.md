Name of the DRS Rule

.PARAMETER Cluster

Name of the vSphere Cluster to create the rule on

.PARAMETER VM

Name of the VM(s) to add to the Rule

.PARAMETER KeepTogether

Keep the VMs together or not

.PARAMETER vCenter

Name of the vCenter to connect to

.PARAMETER Username

Username to connect to vCenter with

.PARAMETER Password

Password to connect to vCenter with

.INPUTS

String

.OUTPUTS

None.

.EXAMPLE

/New-ClusterDRSRule.ps -Name TestRule01 -Cluster Cluster01

-VM Server01,Server02 -KeepTogether
-vCenter vcenter05.sunnydale.local -Username sunnydale\vcosvc

-Password P@ssword1

```
#
[CmdletBinding()]
```

Param

```
(
[parameter(Mandatory=$true)]
[ValidateNotNullOrEmpty()]
[String]$Name,
```

```
[parameter(Mandatory=$true)]
[ValidateNotNullOrEmpty()]
[String]$Cluster
```

```
[nparameter(Mandatory=$true)]
[ValidateNotNullOrEmpty()]
[String[]]$VM,
```