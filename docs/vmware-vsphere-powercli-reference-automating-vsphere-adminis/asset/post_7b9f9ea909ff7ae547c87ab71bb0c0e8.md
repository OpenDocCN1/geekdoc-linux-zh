
Based on that output, you can deduce that on this ESXi node three disk Luns and one CD-ROM drive are connected.

## vSphere View objects

The vSphere View objects are the objects that are used by vSphere internally. These objects are documented in the VMware vSphere API Reference, and will be discussed greater in Chapter 18, "The SDK." vSphere View objects are pre-sent to PowerCLI in two ways:

- Under the ExtensionData property in several places in PowerCLI objects
- As objects returned by the Get-View cmdlet

In both cases, this representation of the vSphere View objects is a read-only copy of the actual vSphere object. This means that the content of the properties is not updated automatically. You will have to get the object again or use the UpdateView method.

```
$vm.ExtensionData.Config.Hardware.NumCPU
1
Set-VM -VM $vm -NumCpu 2 -Confirm:$false
```

| Name | PowerState | Num CPUs | MemoryGB |
| --- | --- | --- | --- |
| VM1 | PoweredOff | 2 | 4.000 |

```
$vm.ExtensionData.Config.Hardware.NumCPU
1
$vm.ExtensionData.UpdateView()
$vm.ExtensionData.Config.Hardware.NumCPU
2
```

The ConvertTo-Text function from Listing 15.1 can also be used on vSphere View objects. The following short sample searches under the Config property of an ESXi node for the location where IPv6Enabled can be found.

```
ConvertTo-Text -InputObject $esx.ExtensionData.Config -Depth 2 |
```

where $_ -match 'IPv6Enabled'
IPv6Enabled - System.Nullable'1[[System.Boolean, mscorlib,
Version=4.0.0.0,
Culture=neutral,
PublicKeyToken=b77a5c561934e089] = False
AtBootIPv6Enabled - System.Nullable'1[[System.Boolean,
mscorlib,
Version=4.0.0.0,culture=neutral,
PublicKeyToken=b77a5c561934e089] = False

## ESXi Console Commands

The ESXi console has many commands available to configure and display the ESXi settings. The esxcli command, which is by far the most important console command, can easily be accessed from within a PowerCLI session. Other console commands require you to establish a Secure Shell (SSH) connection to the ESXi server.

## Esxcli

With the Get-EsXcli cmdlet you have access to the functionality that is available in all the flavors of the esxcli command. The main difference is that you don't need to SSH into the ESXi console.

To use the esxcli commands via PowerCLI, you first have to set up the ESXi object via the Get-ESXCli cmdlet.

```
$vmhost = Get-VMHost -Name esx1.local.test
$esxcli = Get-EsXcli $vmhost
```

Once you have this object, you can navigate through all available namespaces and work with the commands in all of the namespaces. In the next we are in the system.version namespace and use the get() method to obtain information regarding the ESXi version and build:

```
$esxcli.system.version.get()
```

- Build : Releasebuild-2494585
- Patch : 0
- Product : VMware ESXi
- Update : 0
- Version : 6.0.0

There are quite few available namespaces, but for some of the methods in these namespaces, it is not obvious which parameters to use. To help with that, the Get-EsXliCommand function in Listing 15.2 returns all the namespaces, the available methods, and the parameters for each method, and it includes Help text for each.

## LISTING 15.2 Returning details for Get-EsXli namespace

```
function Get-EsXliCommand {
  .SYNOPSIS
  Returns all available namespaces through the Get-EsXli object
  .DESCRIPTION
  The Get-EsXli cmdlet returns an object that can be used to access all properties and methods that are available. This function returns all available methods in these namespaces, together with a short help text and the method's parameters.
  .NOTES
  Source: Automating vSphere Administration
  Authors: Luc Dekens, Brian Graf, Arnim van Lieshout, Jonathan Medd, Alan Renouf, Glenn Sizemore, Andrew Sullivan
  .PARAMETER VMHost
  The host for which to list esxcli namespaces
  .EXAMPLE
  Get-EsXliCommand -VMHost $esx
}

[CmdletBinding()]
Param(
  [Parameter(Mandatory=$true,ValueFromPipeline=$true)]
  [PSObject]$VMHost
)

Process{
  $esxcli = $esxcli.command.list() | % {
    $steps = $_.Namespace.Split('.') + $_.Command
    $stepsHelp = $_.Namespace.Split('.') + 'help'
    # Get the namespace object
$nSpace = $esxcli
$steps | %{
  $nSpace = $(nSpace.$_))
}

# Get the namespace Help
$helpObject = $esxcli
$stepsHelp | %{
  $helpObject = $(helpObject.$_))
}

# Fetch the help for the method
if($helpObject){
  $helpobject = $helpObject.Invoke($_.Command)
}else{
  $helpobject = $null
}

# Method details
$_ Select @N='Command';E="$esxcli.($_.Name).($_.Command)"
  @N='Syntax/Parameter';E="$($nSpace.Value.ToString())"
  @N='Help';E={$helpobject}

# Parameter details
if($helpobject){
  $helpobject.Param | Select @N='Command';E={},
  @N='Syntax/Parameter';E={$DisplayName},
  @N='Help';E={$Help}```

You can call the function with a $VMHost parameter, and you can redirect the returned information to a file or display it onscreen (see Figure 15.1).

```
Get-EscliCommand -VMHost $Name | Out-GridView
```

This information should make it easier to use the namespace methods. Figure 15.1 you can see, for example, how the set method in the hardware.global namespace takes any type of Boolean.

## FIGURE 15.1 Get-EscliCommand sample output

| Command | Syntax/Parameter | Help |
| --- | --- | --- |
| esxcli.hardware.global | -esxcli.hardware.global.Get-cpu | Get properties that are global to all CPUs |
| esxcli.hardware.set | -boolean [hyperthreading] | Set properties that are global to all CPUs. |
| esxcli.hardware.list | -esxcli.hardware.list.Get-cpu | Returns all hardware properties |
| esxcli.p.list | -esxcli.p.list.Get-mi | List of all PCI devices on this host. |
| esxcli.p.get | Get PCI Interface (IFI) device details. | Do not return if the specified device is not present |
| include-pretty-raw | Includes a dump where each byte is separated by a space and/or is in hex |
| include-raw | Includes the value of each byte represented as hexadecimal. |
| node | Specify which bmi ID (0-3) to query, defaults to 'all' for all nodes |

When the Esclicli do not provide access to the command or data you want to access, you can always fall back on establishing a SSH connection to the limited ESXI console based on BusyBox. To allow the SSH connection, you first have to make sure the SSH service is running on the ESXi node. This can be done with a few cmdlets.

```
$EsXNames = 'es1.local.test', 'es2.local.test'
```

```
$Get-VMHost -Name $EsXNames | Get-VMHostService |
Where { $_.Key -eq "TSM-SSH" } |
Start-VMHostService -Confirm:$false
```

> For applications like this you might want to use a perhaps less known PowerShell feature known as wildcarding and matching specific characters. Wildcards, the first line of your script would look like:

```
$EsXNames = 'es[1-2].local.test'
```

or

```
$EsXNames = 'es[1-2].local.test'
```

Wildcards are documented in the PowerShell User Guide:

```
https://www.vmware.com/support/developer/PowerCLI/PowerCLI60R1/
doc/vsp_powercli_60rl_us.pdf
```

A link to this document was installed when you installed PowerCLI.

Once the SSH service is running, you need to establish an SSH connection from your script to the ESXi console. One popular way of doing this is with the help of the plink.exe application that is part of the PuTTY Suite available from

www.chiark.greenend.org.uk/-sgtatam/putty/

This collection of tools offers all kinds of functionality based on SSH.

The plink.exe application allows you to send a bash script to the ESXi node and capture the returned data. The following function (Listing 15.3) allows you, in a simple way, to use plink.exe to send commands to the ESXi console and get the output of that command in your script.

# Listing 15.3 Running a command via SSH with plink.exe

```
function Invoke-EsxSSH {
<.SYNOPSIS
  Execute an ESXi command through an SSH session
  .DESCRIPTION
  This function is a wrapper for the plink.exe command in the PuTTY Suite.
  .NOTES
  Source: Automating vSphere Administration
  Authors: Luc Dekens, Brian Graf, Arnim van Lieshout, Jonathan Medd, Alan Renouf, Glenn Sizemore, Andrew Sullivan
  .PARAMETER VMHost
  The host on which to execute a command
  .PARAMETER Command
  The command to be executed
  .PARAMETER Credential
  The credential to login to the host
  .PARAMETER PathExe
  The path to the folder where the PuTTY Suite is stored
  .PARAMETER IncludeError
  A switch to define if the returned output of the command should include eventual error messages
  .EXAMPLE
  PS> $esxssshSplat = @{
VMHost = $esx
```
