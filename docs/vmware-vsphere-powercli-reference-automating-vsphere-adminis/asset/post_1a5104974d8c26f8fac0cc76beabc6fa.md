
# CHAPTER 1 AUTOMATING VCENTER SERVER DEPLOYMENT AND CONFIGURATION

```powershell
$row.Principal = $perm.Principal
row.Role = $perm.Role
row.IsGroup = $perm.IsGroup
row.Propagate = $perm.Propagate
row.report += $row
```

```powershell
foreach($perm in $vmperms) {
    row = "" | select EntityId, Name, Role, Principal, IsGroup, Propagate
    row.EntityId = $perm.EntityId
    row.FolderName = (Get-View -Id $perm.EntityId -Property Name).Name
    row.Name = $row.FolderName
    row.Principal = $perm.Principal
    row.Role = $perm.Role
    row.IsGroup = $perm.IsGroup
    row.Propagate = $perm.Propagate
    row.report += $row
}
$report | Export-Csv $Filename -NoTypeInformation
```

# Import Permissions

It is equally important to be able to import permissions back into your vCenter Server from which you exported them. To do so, you can use the script in Listing 1.10. Understand that the way permissions are created and stored in vCenter, you can only import back into vCenter.

# LISTING 10 Importing permissions

```powershell
function Import-Permissions {
<#
.SYNOPSIS
Imports all permissions from CSV file

.DESCRIPTION
The function will import all permissions from a CSV file and apply them to vCenter objects.

.NOTES
Source: vSphere Administration

.PARAMETER Filename
The path of the CSV file to be imported

.EXAMPLE
Import-Permissions -Filename "C:\Temp\Permissions.csv"
#>
param(
    [String]$Filename
)
process {
    $permissions = @()
    $permissions = Import-Csv $Filename
    foreach ($perm in $permissions) {
        $entity = (Get-View -Id $perm.EntityId -Property Name).Ref
        $object = Get-Inventory -Name $perm.Name | where {$Id -eq $perm.EntityId}
        if($object) {
            switch -Wildcard ($perm.EntityId) {
                Folder* {
                    $entity.Type = "Folder"
                    $entity.value = $object.Id.Trim("Folder-")
                }
                VirtualMachine* {
                    $entity.Type = "VirtualMachine"
                    $entity.value = $object.Id.Trim("VirtualMachine-")
                }
                ClusterComputeResource* {
                    $entity.Type = "ClusterComputeResource"
                    $entity.value = $object.Id.Trim("ClusterComputeResource-")
                }
                Datacenter {
                    $entity.Type = "Datacenter"
                    $entity.value = $object.Id.Trim("Datacenter-")
                }
            }
            $setperm = New-Object VMware.Vim.Permission
            $setperm.principal = $perm.Principal
            if ($perm.IsGroup -eq "True") {
                $setperm.group = $true
            } else {
                $setperm.group = $false
            }
            $setperm.role = (Get-Role $perm.Role).id
            if ($perm.propagate -eq "True") {
                $setperm.propagate = $true
            } else {
                $setperm.propagate = $false
            }
            $AuthMan = Get-View -Id 'AuthorizationManager-AuthorizationManager'
            Write-Host "Setting Permissions on $($entity.Name) for $($perm.principal)"
            $AuthMan.SetEntityPermissions($entity, $setperm)
        }
    }
}
```

# Configure Datacenters and Clusters

vCenter Server has a hierarchical management structure similar to that of Active Directory. Three main containers can be added to vCenter Server:

- Datacenters
- Clusters
- Folders

**Clusters** A cluster is defined as a group of like-configured computers that act in a fully redundant setup to ensure availability of applications and operating systems. vCenter Cluster is no different. Clusters are used in vCenter Server for three main functions: high availability, load balancing, and high-performance computing. A cluster is made of two or more physical servers that provide resources for the hosts that are assigned to that cluster.

**Folders** A folder is a logical way to define how VMs or vCenter Server objects are organized. Folders are often used to organize VMs into department owners or server functions.

# Creating Datacenters

Datacenters are generally created as part of the initial setup process. The setup can be automated using the following code, which will create a datacenter called Boston and store it in a variable. The Datacenter object held within the variable can then be referred to later in the code as you create clusters or folders:

```powershell
$BostonDC = New-Datacenter -Name Boston -Location Datacenters
```

# Creating Clusters

Clusters are more complex than datacenters; there are many configurable items available for a new cluster. Consider the options the vSphere Web Client guides us: the normal cluster options as well as configuration options for VMware High Availability (HA), VMware Distributed Resource Scheduler (DRS), VMware Enhanced vMotion Compatibility (EVC), and VMware Distributed Power Management (DPM).

To create a cluster in the datacenter you created earlier, use the following code:

```powershell
$ProductionCluster = New-Cluster -Location $BostonDC -Name "Production"
```

This code line gives you the basic settings. The sections that follow the additional cluster settings available to you.

# Configuring High Availability

When configured in a cluster, VMware HA gives you many advantages, including the following:

- Proactive monitoring of all vSphere hosts and VMs
- Automatic detection of vSphere host failure
- Rapid restart of VMs affected by host failure
- Optimal placement of VMs after server failure

Much like the configuration of a cluster through the vSphere Web Client, you can configure HA within an either cluster or as part of the initial cluster setup or you can alter an existing cluster object. For example, to configure a new cluster Production with HA enabled and HA failover level of 1 physical host failure and the HA Restart Priority as Medium, you would use the code in Listing 1.11.

# LISTING 1.11 Enabling HA with a failover host level and restart priority on a new cluster

```powershell
$ProductionCluster = New-Cluster \
-Location $BostonDC \
-Name "Production" \
-HAEnabled -HAAdmissionControlEnabled \
-HAFailoverLevel 1 \
-HARestartPriority "Medium"
```

To complete this action on an existing cluster, you will need to retrieve the cluster as an object and then push it down the pipeline into the Set-Cluster cmdlet, as shown in Listing 1.12.

# LISTING 1.12 Enabling HA with a failover level and restart priority on an existing cluster

```powershell
Get-Cluster \
-Location $BostonDC \
-Name "Production" | \
Set-Cluster -HAEnabled $true \
-HAAdmissionControlEnabled $true \
-HAFailoverLevel 1 \
-HARestartPriority "Medium"
```

# Configuring Distributed Resource Scheduler

VMware DRS is a configuration at the cluster level of the vCenter environment that balances VM workloads with available host resources. With VMware, DRS can be used to define the rules for allocation of physical resources. If the workload on one or more VMs drastically changes, DRS redistributes the VMs among the clusters. Like HA, DRS can be configured as part of the initial cluster setup or as an alteration to an existing cluster object. For example, to configure a new cluster Production with DRS and a DRS automation level of FullyAutomated set to FullyAutomated, you would use the code in Listing 1.13.

# LISTING 1.13 Configuring DRS on a new cluster

```powershell
$ProductionCluster = New-Cluster "Production" \
-Location $BostonDC \
-DrsEnabled \
-DrsAutomationLevel "FullyAutomated" \
-Confirm:$false
```

To complete this action on an existing cluster, you would again need to retrieve the cluster object and push the object through the pipe into the Set-Cluster cmdlet, as seen in Listing 1.14.

# LISTING 1.14 Configuring DRS on an existing cluster

```powershell
Get-Cluster -Location $BostonDC \
-Name "Production" | Set-Cluster -DrsEnabled $true \
-DrsAutomationLevel "FullyAutomated" \
-Confirm:$false
```
