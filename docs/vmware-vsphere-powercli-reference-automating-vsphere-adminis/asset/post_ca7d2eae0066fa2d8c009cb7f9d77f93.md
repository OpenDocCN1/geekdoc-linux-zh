
When a cmdlet can perform one or more functions, PowerShell groups the parameters for each function into a parameter set. The New-VM cmdlet includes four parameters, or four separate types of operations:

- -NewVM
- Template
- RegisterVM
- CloneVM

Each parameter set is a grouping of parameters that perform a specific function. Unfortunately, mixing and matching parameters from different parameter sets is not allowed. For clarity, and because they perform four functions, we will cover each parameter set independently.

This raises a question: How does PowerCLI choose which parameter to use? Each parameter set has at least one unique parameter. The default parameter set is assumed until PowerCLI finds that one unique parameter differentiates the current application from the configured default. In the case of the New-VM cmdlet, the New-VM parameter is assumed until a parameter used elsewhere is found.

Regardless of the parameter set, there are two mandatory parameters: Name and VMHost. When connected directly to a vSphere host, PowerCLI assumes the VMHost parameter. That means when connected directly to a vSphere host, creating a new VM is as easy as New-VM -Name VM01.

Although this is a cool demo, it is not very useful in the real world. Nevertheless, it is useful to understand why that works. PowerCLI inferred both the VMHost and the parameter set. It then chose the remaining mandatory parameter, Name, and created a new VM using the defaults outlined in Table 6.1. The point here is because PowerCLI and its underlying engine, PowerShell, to go to "help" 99.9% of the time is correct. Keep in mind that without explicit instructions, PowerCLI will always use those defaults.

## Creating a New Virtual Machine

Amazing, PowerCLI is not often used to create new virtual machines. Somehow, the community at large missed the huge advantage PowerCLI offers in this arena. If an organization makes use of enterprise provisioning systems, such as Microsoft’s System Center Configuration Manager (SCCM) or HP’s Business Service Automation (HP-BSA), you can benefit from automating your new VM creation. Even if you're using a basic OS provisioning tool like Windows Deployment Services, Symantec Ghost, Linux Kickstart, or Solaris JumpStart, there is still benefit. Automation ensures that the base hardware is exactly the same every time!

How can you create a virtual machine? Well, generally the way you solve problem in PowerCLI is by starting with a statement or question—for example, "I need to create an RHEL6 VM with a thin-provisioned hard drive, 10 GB of RAM. I need to mount an ISO in datastore0, and the network should be on VLAN 22." From there, you parse it out into cmdlets, like in Listing 6.1.

### LISTING 6.1 Cmdlets to create a new VM

```
New-VM -Name RHEL6_01 \
-DiskMB 10240 \
-DiskStorageFormat thin \
-MemoryMB 1024 \
-GuestID rhel_64_Guest -Name VLAN 22 \
-Portgroup (Get-VDPortgroup) \
-CD \
Get-CDDrive -IsoPath "[datastore0]\rhel-server-6.5-x86_64-boot.iso" \
-StartConnected:$true \
-Confirm:$false
```

> NOTE: Good PowerShell code should be read as an English sentence.

Notice how that one-liner required the use of several cmdlets. The conventional wisdom would be that all aspects of creating a new VM would be performed with the New-VM cmdlet. This is not the case with PowerCLI, nor with PowerShell in general. Every cmdlet is responsible for one small task or function. There, more complex operations require multiple cmdlets to be chained into a pipeline to complete the whole task. For example, the New-VM cmdlet creates only the bare hardware. Everything beyond that—like connecting a CD—must be done after the VM has created.

For the most part, this is straightforward. However, sometimes a parameter may require a value that is not as clear. For example, consider the rather cryptic -GuestId parameter. You can check the vSphere API documentation—visit this site:

```
http://pubs.vmware.com/vphere-60/index.jsp#com.vmware.wssdk.apidire.doc/vim.vm.GuestOsDescriptor
```

Chances are, it will be more convenient to keep this data in PowerShell where it can be manipulated. Listing 6.2 contains a function that does that. The Get-VMGuestID query vCenter Server for supported operating systems and responding guest IDs.

### LISTING 6.2 Querying vCenter Server for operating systems and guest IDs

```
#
SYNOPSIS
    Query VMHost for a list of the supported operating systems, and their
    Guest IDs.
DESCRIPTION
    Query VMHost for a list of the supported operating systems, and their
    Guest IDs.
.PARAMETER VMHost
    VMHost to query the list of Guest IDs
.PARAMETER Version
    Virtual Machine Hardware version, if not supplied the default for that
    host will be returned. e.g. ESX3.5 = 4, vSphere = 7
.EXAMPLE
    Get-VMGuestId -VMHost vSphere
.EXAMPLE
    Get-VMGuestId -VMHost vSphere | Where {$_.family -eq 'windowsGuest'}
#
function Get-VMGuestId {
    [CmdletBinding()]
    Param(
        [parameter(Mandatory=$true
        ValueFromPipeline=$true

[VMware.VimAutomationViCore.Impl.V1.Inventory.VMHostImpl]
$VMHost

[int]
$Version
Process

```
$HostSystem = Get-View -VIObject $VMHost -Property Parent
$compResource = Get-View -Id $HostSystem.Parent `
-Property EnvironmentBrowser
$EnvironmentBrowser = Get-View -Id $compResource.EnvironmentBrowser `
$VMConfigOptionDescriptors = =
$EnvironmentBrowser.QueryConfigOptionDescriptor
```

```
if ($Version)
{
Key = $VMConfigOptionDescriptors |
Where-Object {$_.key -match "$($Version)"} |
Select-Object -ExpandProperty Key
```

```
else
{
Key = $VMConfigOptionDescriptors |
Where-Object {$_.DefaultConfigOption} |
Select-Object -ExpandProperty Key
$EnvironmentBrowser.QueryConfigOption($Key,
$HostSystem.MoRef) |
Select-Object -ExpandProperty GuestOSDescriptor |
Select-Object @(
Name='GuestId'
Expression={$_.Id}
@(
Name='Family'
Expression={$_.Family}
@{
Name='FullName'
Expression={$_.FullName)
}
```

When run, the Get-VMGuest returns a collection of all the supported guest objects. The Out-Grid cmdlet was built for situations like this. The easiest method is to pipe the output to Out-Grid, as shown in Figure 6.1.

Figure 6.1 Get-VM piped to Out-Grid![](img/62596f5acc97904068a4511beb7d6.png)

Now, about a more complex VM—say a SQL Server 2012 virtual machine with the following specifications:

* 4 vCPUs
* 8 GB of RAM
* A thin-provisioned 40 GB hard drive
* 100 GB thick and 10 GB thick hard drive
* Two e1000 network adapters on the Public and VLAN100 port groups

you must place the VM within the SQL resource pool on Cluster1. Listing 6.3 shows how to accomplish this.

### LISTING 6.3 Creating a complex machine

```
$Cluster = Get-Cluster -Name 'Cluster1'
$ResourcePool = Get-ResourcePool -Name 'SQL' -Location $Cluster
$VM = New-VM -Name 'SQL01'
-NumCpu 4 \
-MemoryGB 8 \
-DiskStorageFormat 'Thin' \
-DiskGB 40 \
-GuestId 'windowsServer64Guest' \
-VMHost (-Get-VMHost -Location $Cluster -State Connected |
Get-Random) \
-ResourcePool $ResourcePool
#Add additional e100e Network Adapters
New-NetworkAdapter -Portgroup (Get-VDPortgroup -Name VLAN22) \
-StartConnected \
-Type 'e100e' \
-VM $VM
#Add additional hard drives
New-HardDisk -CapacityGB 100 -VM $VM
New-HardDisk -CapacityGB 10 -VM $VM
```

Listing 6.3 is slightly more complicated than the previous listing, but it's still easy to comprehend.

## Cloning a Virtual Machine

There are many reasons to clone a virtual machine. Perhaps the most popular is to create a test instance of a production VM. Clones can serve as a form of backup. We've even clones implemented as an inexpensive DR solution. Whatever your reason, PowerCLI can accommodate you.

For example, here's how to clone the SQL Server recently deployed to the Test cluster and name it SQL01_Clone:

```
# Get source VM Object
$SourceVM = Get-VM -Name SQL01
#Get a connected host within the Test cluster
```
