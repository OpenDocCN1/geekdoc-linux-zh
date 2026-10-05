# ADD, CONFIGURE, AND REMOVE VIRTUAL HARDWARE

memory. This time, however, use the -NumCpu parameter to specify the new number of vCPUs. To add a vCPU to a VM named VM001, use the following:

```
Set-VM VM001 -NumCpu 2 -Confirm:$false
```

Again, remember the VM needs to support CPU hot plug or be powered off. Listing 2 contains a function based on the code in Listing 8.1 that automate the process of changing the number of vCPUs or amount of memory when a VM doesn't support hot plug. This kind of meta-scripting is common in PowerShell, and it's one of the reasons the language is so popular with virtualization administrators.

# LISTING 8.2 Changing VM memory and vCPU offline

```
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
```

Managing the Virtual Machine Life Cycle PART II

269