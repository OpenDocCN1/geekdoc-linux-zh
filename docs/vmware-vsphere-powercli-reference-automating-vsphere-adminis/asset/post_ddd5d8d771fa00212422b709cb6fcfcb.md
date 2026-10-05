
708 CHAPTER 20 • VCLOUD AIR

<style>
TD {border-width: 2px;padding: 3px;
border-style: solid;border-color: black;
Tr-Child(Even) {Background-Color: #ddddddd};
</style>
@

# Add Titles for each section
$Pre = "<h1>vApp Overview</h1>"
$Post = "<br><br><br><h1>VM Overview</h1>"

# Combine all pieces of the report
$VMReport = "<h1>VM Overview</h1>"
$VMReport += Convert-To-Html -Head Header

# Export report to destination filepath
$Objects | ConvertTo-HTML -Head Header -PreContent $Pre
-PostContent $VMReport | Out-File $Filename -Force

}
}

# API Tasks

Not only can the Get-CIView cmdlet (corrected from OCR) retrieve information about objects in your environment, but it can be used to invoke tasks on those objects using the methods that are available. Each object can be piped to Get-Member (or gm for short) to retrieve a list of actions (also known as methods) you can take on the specified object.

To achieve this, you will need to specify the CIView of an object. In this example, we'll select the Jumpbox virtual machine from the "nested" vApp referred to in the "Extension Data" section of this chapter.

```powershell
$vm = Get-PIVM Jumpbox | Get-CIView
```

You can then retrieve the methods in one of two ways. The first retrieves member types of the object, whereas the second filters the results to show only the methods:

```powershell
$vm | Get-Member
```

# GET-CIVIEW 709

or

$vm | Get-Member -MemberType Method
TypeName: VMware.VimAutomation.Cloud.Views.Vm

| Name | MemberType | Definition |
| :--- | :--- | :--- |
| AcquireMksTicket | Method | VMware.VimAutomation.Cloud.Views.Mks... |
| AcquireTicket | Method | VMware.VimAutomation.Cloud.Views.Scr... |
| Attach | Method | void Attach(System.Nullable[int] bus... |
| Attach_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| CheckCompliance | Method | void CheckCompliance() |
| CheckCompliance_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| Consolidate | Method | void Consolidate() |
| Consolidate_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| ControlAccess | Method | VMware.VimAutomation.Cloud.Views.Con... |
| CreateMetadata | Method | void CreateMetadata(VMware.Metadata(VimAutuma... |
| CreateMetadata_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| CreateSnapshot | Method | void CreateSnapshot(System.Nullable[...... |
| CreateSnapshot_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| CustomizeNextPowerOn | Method | void CustomizeNextPowerOn() |
| Delete | Method | void Delete() |
| Delete_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| Deploy | Method | void Deploy(System.Nullable[bool] po... |
| Deploy_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| Detach | Method | void Detach(System.Nullable[int] bus... |
| Detach_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |

Let's say that you wanted to create a snapshot of this virtual machine. No cmdlet available that can do this for you, but you do have the CreateSnapshot method. See the information required to run the CreateSnapshot method, add the method name to the end of your:

$vm.CreateSnapshot

OverloadDefinitions

```powershell
void CreateSnapshot(System.Nullable[bool] memory, System.Nullable[bool] quiesce, string name, string description)
```

Integration PART V

In the OverloadDefinitions property you can see how the method needs to be formed. For all intents and purposes, to make this work you only need a name for the snapshot, the description is optional, but if you do not add a description, you should use $null as a placeholder. To create the virtual machine snapshot, your command would look like this:

```powershell
$vm.CreateSnapshot($null, $null,"Snapshot Name", $null)
```

As you dive deeper into the Get-Member methods of objects in vCloud Air, you open the door to do great things—as well as potentially do great harm. It is important that you understand what each method will do before invoking it.

# CHAPTER 21

# vRealize Orchestrator

IN THIS CHAPTER, YOU WILL LEARN TO:

- REQUIREMENTS 712
- vRO ................................................................. . . . . . . . . . . . . . 712
- PowerShell .......................................................................... . . . . 712
- PowerShell Host. ..................................................................... . 713
- Configuration ........................................................................ . . . 713

- RUNNING AN EXTERNAL SCRIPT 719
- RECEIVING A RETURN CODE FROM AN EXTERNAL SCRIPT 721
- USE CASES 727
- vSphere Tagging .......................................................................... . . 727
- vSphere DRS Rule .......................................................................... . . 727

- ALTERNATIVE METHOD TO POWERSLL 749
- Requirements .................................................................... 750
- Configuration .................................................................... . 750
- Use Case ........................................................................ . 756

- CALLING WORKFLOWS FROM POWERSLL 767
- Retrieving Details ................................................................ 767
- Invoking a Workflow ............................................................ 772
- Querying a State ................................................................ 779
- Retrieving Output ................................................................ 782
- Querying Executions ................................................................ 786

# CHAPTER 21

vRealize Orchestrator (vRO) (formerly vCenter) has been part of VMware for a long time but was known as 'vCenter'. Those who know about it were able to simplify IT tasks.

# Requirements

If you want to integrate vRO, there are a number of requirements above those for vRO.

# vRO

vRO 6.0 is available in two flavors: a Linux appliance or Windows-based installation. For the purposes of this book, we will be using Windows-based. This also meets the PowerShell host requirement if vRO Linux appliance is being used.

# PowerShell

vRO needs to communicate with a PowerShell host to execute PowerShell commands and scripts. If you are using the Windows install of vRO, it is possible to use vRO as a PowerShell host. However, for the purposes of this book, we are using another Windows Server 2012 machine as a PowerShell host.

# Configuration

You must take a number of steps to correctly configure the remote PowerShell Host and vRO before you use the PowerShell-in. These are primarily based on what protocol and authentication methods you will use to communicate with the remote PowerShell host. The nature of such decisions is beyond the scope of this book. For our purposes, we will be using HTTP and Kerberos.

# Time Sync

Since we will be using Kerberos for our authentication, it is important to ensure that all servers being used are synchronized to the same time source.

# PowerShell

On the PowerShell host, PowerShell v4 is required either by using Windows Server 2012 R2, where it is built in, or by installing the Windows Management Framework 4.0 for previous versions of Windows. Additionally, the PowerShell Execution Policy should be set to one that permits running scripts on the system.
