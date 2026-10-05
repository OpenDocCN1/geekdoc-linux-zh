
# CHAPTER 8 • CONFIGURING VIRTUAL MACHINE HARDWARE

To reset the memory limit on a VM (set it to Unlimited), use the following:

```
Get-VM VM001 | Get-VMResourceConfiguration | \
Set-VMResourceConfiguration -MemLimitMB $null
```

The third mechanism to configure memory resources is shares. Shares come into play when there's memory contention on a host. When memory contention is encountered, shares determine the VM's entitlement to memory for the amount of memory shared with the reservation and the limit (see Figure 8.1). To change the number of memory shares, use the -SharesLevel parameter. Possible enumeration values are Custom, High, Low, and Normal. Because this parameter accepts an enumerator, it is also possible to specify an index from 0 to 3, where an index value of 0 Custom, 1 High, 2 Low, and 3 Normal. Table 8.1 contains an overview of the available memory shares levels. It is rare to fine-tune the memory shares before the factory presets (High, Low, and Normal), but if you have to, set the share level to Custom and specify the number with the -NumShares parameter.

# TABLE 8.1 Memory shares

| Shares level | Shares/MB | Index |
|---|---|---|
| Custom | 1-1,000,000 | 0 |
| High | 20 | 1 |
| Low | 5 | 2 |
| Normal | 10 | 3 |

To set the share level to a custom value of 1,500, use the following:

```
Get-VM VM001 | Get-VMResourceConfiguration | \
Set-VMResourceConfiguration -MemSharesLevel "Custom" | \
-NumShares 1500
```

# Changing the Number of vCPUs

After addressing the performance issues by adding additional memory, it wouldn't be surprising to find that the VM now has increased CPU utilization. To ensure performance stays at an acceptable level, you can allocate additional CPU to the VM. (Be sure to confirm with the application vendor that the application is multi-threaded and can benefit from an extra CPU.) To change the number of vCPUs assigned to a VM, use the Set-VM cmdlet again as with changing the amount of memory.

This time, however, use the -NumCpu parameter to specify the new number of vCPUs. To add a vCPU to a VM named VM001, use the following:

```
Set-VM VM001 -NumCpu 2 -Confirm:$false
```

Again, remember the VM needs to support CPU hot plug or be powered off. Listing 2 contains a function based on the code in Listing 8.1 that automate the process of changing the number of vCPUs or amount of memory when a VM doesn't support hot plug. This kind of meta-scripting is common in PowerShell, and it's one of the reasons the language is so popular with virtualization administrators.

# LISTING 8.2 Changing VM memory and vCPU offline

```powershell
function Set-VMOffline
{
    .SYNOPSIS
    Changes the vCPU and memory configuration of the virtual machine Offline

.DESCRIPTION
    This function changes the vCPU and memory configuration of the virtual machine Offline

.NOTES
    Source: Automating vSphere Administration
    Authors: Luc Dekens, Arnim van Lieshout, Jonathan Medd, Alan Renouf, Glenn Sizemore, Brian Graf, Andrew Sullivan. PARAMETER VM
    Specify the virtual machine
    .PARAMETER MemoryMB
    Specify the memory size in MB
    .PARAMETER NumCpu
    Specify the number of virtual vCPUs
    .PARAMETER TimeOut
    Specify the number of seconds to wait for the vm to shut down gracefully. Default timeout is 300 seconds
    .PARAMETER Force
    Switch parameter to forcibly shutdown the virtual machine after timeout
    .EXAMPLE

PS> Get-VM VM001 | Set-VMOffline -memoryMB 4096 -numCpu 2
```

```powershell
Param (
    [parameter(ValueFromPipeline) = $true, Mandatory = $true, HelpMessage = "Enter a vm entity"]
    [VMware.VAutomation.ViCore.Impl.V1.Inventory.VirtualMachineImpl]$VM,
    [int64]$memoryMB,
    [int32]$numCpu,
    [int32]$timeOut = 300,
    [switch]$force
)
```

```powershell
Process {
    if ($memoryMB -or $numCpu) {
        if ((Get-VM $VM).PowerState -eq "PoweredOn") {
            $powerState = "On"
            Stop-VM $VM -Confirm:$false | Out-Null
        }
        $startTime = Get-Date
        while (((Get-VM $VM).PowerState -eq "PoweredOn") -and ((Get-Date) - $startTime).totalseconds -lt $timeOut)) {
            Start-Sleep -Seconds 2
        }
        if ((Get-VM $VM).PowerState -eq "PoweredOff" -or $force) {
            if ((Get-VM $VM).PowerState -eq "PoweredOn") {
                Write-Warning "The shutdown guest operation timed out"
                Write-Warning "Forcing shutdown"
                Stop-VM $VM -Confirm:$false | Out-Null
            }
        }
    }
    $Splat = @{'VM'=$VM; 'Confirm'=$false}
    if ($memoryMB) {
        $Splat['MemoryMB'] = $memoryMB
    }
}
```

```powershell
if ($numCpu)
{
    $Splat['NumCpu'] = $numCpu
    Set-VM @Splat | Out-Null
    if ($powerState -eq "On")
{
        Start-VM VM
    }
    else
{
        Write-Error "The shutdown guest operation timed out"
    }
}else
{
    Write-Error "No value for -memoryMB or -numCpu supplied"
}
```

![](img/62596f5acc979040608a4e5111beb7d6_302_0.png)

# Changing vCPU Resources

With memory resources, CPU resources can be influenced by tuning the CPU resource entitlement of a VM with reservations, limits, and shares. Reservations and limits are specified in megahertz (MHz). Reserves are used to guarantee a minimal level for important allocation and to reserve a certain number of MHz. On the other hand, it may be necessary to prevent badly behaving from hogging valuable CPU by configuring a CPU limit. To change vCPU reservations, limits, and shares, use the Get-VMResourceConfiguration and Set-VMResourceConfiguration cmdlets as described in "Changing Memory Resources". To set a vCPU reservation, use the -CpuReservationMhz parameter. Use the following to set a vCPU reservation of 4000 on a VM named VM001:

```
Get-VM VM001 | Get-VMResourceConfiguration | Set-VMResourceConfiguration -CpuReservationMhz 4000
```

To change the number of CPU shares, uses the -CpuSharesLevel parameter. Possible enumeration values are Custom, High, Low, and Normal. Because this accepts an enumerator value, you can also specify an index value from 0 to 3, where index value 0 means Custom, 1 means High, 2 means Low, and 3 means Normal. Table 8.2 contains an overview of the shares. To fine-tune the shares level beyond the factory presets (High, Low, and Normal), set the share level to Custom and specify the number of shares with the -CpuShares parameter.

# TABLE 8.2 CPU shares

| Shares | Shares/vCPU | Index |
|---|---|---|
| Custom | 1,100,000 | 0 |
| High | 2,000 | 1 |
| Low | 500 | 2 |
| Normal | 1,000 | 3 |

To set a vCPU share for High, use the following:

```
Get-VM VM001 | Get-VMResourceConfiguration | Set-VMResourceConfiguration -CpuSharesLevel "High"
```

Resource limits, both CPU and memory, are real performance killers. Memory limits cause the affected VM to start ballooning and swapping in almost all cases. How to generate a report containing all VMs that have CPU and memory limits is covered in Chapter 15, "Reporting and Auditing."

# Adding or Removing a Network Adapter

Networking design requirements are one of the most fluid elements of a virtual infrastructure. Often network adapters must be added and reassigned almost on demand. Additional network adapters can be added to an existing VM with the New-NetworkAdapter cmdlet undergone several iterations as the ability to manage distributed virtual switches was switched to PowerCLI. To maintain backward compatibility, the old parameters have been maintained, but when writing code today the ConnectToPortgroup parameter set should be used because
