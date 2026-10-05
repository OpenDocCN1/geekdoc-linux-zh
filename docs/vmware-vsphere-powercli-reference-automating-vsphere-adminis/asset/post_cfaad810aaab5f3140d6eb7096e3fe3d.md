
# CHAPTER 7 • USING TEMPLATES AND CUSTOMIZATION SPECIFICATIONS

```powershell
Write-Host "Updating Tools..." -NoNewLine
#Wait for the update to finish
while ($VM.ExtensionData.Guest.ToolsStatus -ne "ToolsOk")
{
    Start-Sleep -Seconds 1
    Write-Host ""," -NoNewLine
    $VM.ExtensionData.UpdateViewData("Guest")
}
Write-Host "DONE" -ForegroundColor 'Green'
Write-Host "Tools upgrade complete"
Write-Host "Starting hardware Upgrade"
}
else {
    Write-Host "ToolsOK Starting hardware Upgrade" -ForegroundColor 'Green'
}

# Shut the VM back down
Write-Host "Shut down guest"
$VM = Stop-VMGuest -VM VM -Confirm:$false | Wait-VMGuest Shutdown
$VM.ExtensionData.Upgrade($Version)
Write-Host "VM Hardware updated..."
Write-Host "Starting VM please log in and verify"
$VM = Start-VM -VM VM

else {
    Write-Host "VM Hardware is up to date." -ForegroundColor 'Green'
    $VM = Set-VM -VM VM -ToTemplate -Confirm:$false
}
```

## Patching

Once a well-established template is developed, there is no reason to make many modifications. It is necessary, however, to keep the template up to date. Several techniques are available for this purpose.

For example, a Windows shop might leverage Windows Server Update Services (WSUS) or System Center Configuration Manager (SCCM) to patch their Windows VMs. A RedHat shop might use Puppet in conjunction with a Satellite server. Smaller organizations might use a unified patch platform like Shavlik.

Whatever the chosen process, PowerCLI is here to help. By integrating the existing patch management infrastructure with the virtual infrastructure, it is possible to maintain the best of both worlds. For instance, if an organization manually updates all servers, then more than likely it will manually update its templates as well. PowerCLI can still automate the conversions and power operations, but someone will have to log in and manually install any patches (see Listing 7.20).

### Listing 7.20 Automating the template patch life cycle

```powershell
Get-Template 'w2k8R2' |
  Set-Template -ToVM |
  Start-VM |
  Wait-VMGuest Startup |
  # here you would log in and patch the guest
  Wait-VMGuest Shutdown |
  Set-VM -ToTemplate -Confirm:$false
```

The preceding script used PowerCLI to convert the template into a VM, start the VM, and wait until the guest was updated. PowerCLI then detected the power-off, used as a cache that the update was finished, and converted the VM back into a template. This approach has the benefit of organizing the patch process, making repeatable across any number of VMs, while not requiring a completely automated solution.

Of course it is possible to take this process step further and automate the whole patch life cycle. The script in Listing 7.21 does just that. This time the code takes a snapshot beforehand, and pre-stages any required updates by triggering detection within the guest. Finally, the VM is cloned back into a new template, thereby fulfilling any failback requirements from the change management processes.

### LISTING 7.21 Automating the template patch life cycle

```powershell
$HostCredential = Get-Credential
$GuestCredential = Get-Credential
$DTG = Get-Date -Format s
#Convert template back into VM
$VM = Get-Template 'w2012r2' |
  Set-Template -ToVM
#Take a snapshot before we alter our template
$Snapshot = New-Snapshot -VM $VM `
  -Name Units_DTG `
  -Description "scheduled updates $DTG"
#Power on the VM, and wait for tools to report in
$VM = Start-VM -VM $VM | Wait-VMGuest 'Startup'
#kick off the Windows Update detection agent within the system
Invoke-VMScript -VM $VM `
  -Credential $GuestCredential
  -HostCredential $HostCredential `
  -ScriptText '%windir%system32\wauauct.exe /reportnow /detectnow'
wait for the VM to be powered off
$VM = Wait-VMGuest -VM $VM -Operation 'Shutdown'
# Create a new template for testing
$Template = New-Template -VM $VM -Name "{0}_{1}" -f $VM.Name, $DTG
```

The next step would be to fully automate the installation of patches. Using a combination of Invoke-VMScript and some guest scripting, it is possible to build a hands-free update process. The decision of whether or not depends on the organization.

> TIP: When automating any system, keep in mind that there are barriers. It is possible to take automation too far, making it too complex or delicate. Ultimately, you need to assess whether additional automation would provide a measurable savings. (img/62596f5acc979040608a4e5111beb7d6_295_0)

## Configuring Virtual Machine

IN THIS CHAPTER, YOU WILL LEARN TO:

| Task | Page |
| --- | --- |
| - ADD, CONFIGURE, AND REMOVE VIRTUAL HARDWARE | 266 |
| Changing Virtual Memory | 266 |
| Changing Memory Resources | 267 |
| Changing the Number of vCPUs | 268 |
| Changing vCPU Resources | 271 |
| Adding or Removing a Network Adapter | 272 |
| Assigning a Network | 274 |
| Adding a Virtual Disk | 275 |
| Removing a Virtual Disk | 278 |
| Extending a Virtual Disk | 285 |
| Changing Other Hardware | 287 |
| - OPTIMIZE STORAGE USAGE WITH THIN PROVISIONING | 288 |
| Converting a Virtual Disk Using vMotion | 289 |
| Converting a Virtual Disk in Place | 289 |

## Add, Configure, and Remove Virtual Hardware

Once the virtualization environment is up, comes a time when a virtual machine needs to be reconfigured. Perhaps performance is lacking and an additional vCPU or more memory is needed. A disk might be running into its capacity and needs to be extended. All of these tasks and some other tasks are covered in this chapter. This section focuses on changing virtual machine (VM) hardware like memory, network adapters, and virtual disks.

### Changing Virtual Memory

It's as old as virtualization itself. A VM pushed into production with 1024 MB of RAM, and you quickly notice that performance is lacking due to memory exhaustion. The fix is simple: increase the amount of memory on the VM. To do so, use the Set-VM cmdlet. It accepts a -MemoryMB parameter, which allows modification of the VM's size:

```powershell
Set-VM VM001 -MemoryMB 2048 -Confirm:$false
```

Everything else in vSphere, the ability to modify a VM is based on the rules and the VM configuration. The VM in question must either be powered off or support memory plug. If the VM doesn't support memory plug, it can only be shut down during maintenance hours; it might be advantageous to schedule the upgrade process.

Listing 8.1 completes the process. First, the VM is gracefully shut down, and after the memory is upgraded, the VM is powered on. Using this simple script, it is possible to schedule the upgrade during maintenance hours when the impact on end users is minimal.

### LISTING 8.1 Changing virtual machine memory offline

```powershell
Get-VM VM001 | Stop-VMGuest -Confirm:$false
While ((Get-VM VM001).PowerState -ne "PoweredOff") {
  Sleep -2 Seconds
}
Get-VM VM001 | Set-MemoryMB 2048 -Confirm:$false
Get-VM VM001 | Start-VM -Confirm:$false
```

## Changing Memory Resources

To guarantee memory entitlement, a memory reservation must be configured for the VM. Memory reservations guarantee that the reserved memory will always be backed by physical memory, even during times of memory contention. This is often configured to ensure some level of performance for a VM. Memory reservations also determine the size of the VM's swap file on the vSphere host, as the swap file's size is equal to the VM's configured memory minus its.

There are times when it is necessary to artificially cap a VM to prevent it from using too much machine memory. This is accomplished by configuring a memory limit. Memory limits force any memory requirements above the limit to be provided from the VM's swap file on the host. Memory provided from the swap file doesn't perform very well and should only be used in situations where extreme memory pressure is degrading the performance of all VMs.

All elements of VM resource configuration are configurable with the Get-VMResourceConfiguration and Set-VMResourceConfiguration cmdlets.

To set a memory reservation, use the -MemReservationMB parameter. The value of this parameter ranges from 0 to the value of the memory limit, or if no limit is set, the amount of configured memory. To set a memory limit, use the -MemLimitMB parameter. The value for this parameter ranges from the value of the memory reservation to the maximum amount of configured memory. Figure 8.1 is a general representation of these parameter ranges.

To set the memory reservation to 1,024 MB and the memory limit to 1,536 MB on your virtual machine, use the following:

```powershell
Get-VM VM01 | Get-VMResourceConfiguration | 
    Set-VMResourceConfiguration -MemReservationMB 1024 |
    -MemLimitMB 1536
```

Figure 8.1 Memory reservation and limit ranges

![](img/62596f5acc979040608a4e5111beb7d6_298_0.png)
