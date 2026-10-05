
# CHAPTER 13 • HARDENING THE VSPHERE ENVIRONMENT

from a VMHost should be blocked. You can verify VMHosts' default firewall policy by using this:

```powershell
Get-VMHost vMi0[56].dom.int | Get-VMHostFirewallDefaultPolicy

IncomingEnabled OutgoingEnabled
False            False
False            False
```

Should you ever need to configure ESXi host's firewall default policy, you could use something like the following code. This example assumes that someone changed the default firewall policies on the given VMHosts to $true at some point, and shows the resulting DefaultPolicy values are at $false:

```powershell
Get-VMHostFirewallDefaultPolicy -vMi0[56].dom.int |
Set-VMHostFirewallDefaultPolicy -AllowIncoming $false

IncomingEnabled OutgoingEnabled
False            False
False            False
```

The Hardening Guide has an assessment command example that allows you to get the current VMHost firewall exceptions using the Get-VMHostFirewallException cmdlet. You can use the Set-VMHostFirewallException cmdlet when you need to change an exception. For example, suppose that it is time to use Network Time Protocol (NTP) to synchronize the clocks in your environment around the network. You have used the Set-VMHostService cmdlet to set the policy of the network, but you need to enable a firewall exception for the related NTP communications. The following will enable the NTP exceptions on given VMHosts:

```powershell
Get-VMHost vMi0[56].* Get-VMHostFirewallException -Name "NTP Client" |
Set-VMHostFirewallException -Enabled:$true
```

| Enabled | IncomingPorts | OutgoingPorts | Protocols | ServiceRunning |
| --- | --- | --- | --- | --- |
| NTP Client | True | 123 | UDP | True |
| NTP Client | True | 123 | UDP | True |

# WORK WITH THE GUIDELINES

# 457

Granted, if you were using something like the vSphere Web Client to configure NTP on a VMHost (or some other host-related configurations that require firewall exceptions), the Web Client takes care of enabling and disabling the corresponding firewall exception. But, this is PowerShell CLI GUI? What GUI? We take care of the firewall exception configuration on our own.

# Virtual Machines

There are several guidelines for virtual machines in the Hardening Guide (about 40 of them), many of which deal with advanced settings of the virtual machine objects. VMware has done a great job with these virtual machine guidelines; PowerShell assessment and remediation commands are provided for nearly all of them.

One VM whose remediation command could use a bit of expansion is Guid VM.disable-independent-nonpersistent. This guideline helps you using independent nonpersistent disks and removes the ability of attackers to clear their disks by rebooting and power-cycling a VM with an IndependentNonPersistent disk. The PowerShell remediation command for this guideline uses the cmdlets to use, but it does not include the full set of parameters needed for remediation. IndependentNonPersistent virtual disks to IndependentPersistent disks.

![](img/62596f5acc979040608a4e5111beb7d6_488_0.png)

- **LIST 13.5** Changing persistence of independent-nonpersistent vDisks

```powershell
## the disk persistence mode to which to change
$strTargetMode = "IndependentPersistent"

Get-VM | Foreach-Object {
$VM = $_
## if this VM has IndependentNonPersistent disks
if ($ArrNonPerDiskVM = Get-HardDisk -VM $VM | Where-Object {
$_.Persistence -eq "IndependentNonPersistent*"}) {
## if the VM has a snapshot, write a warning that cannot convert its disks
if ($ArrSnapsThisVM = Get-Snapshot -VM $VM) {
$IntNumSnapsThisVM = ($ArrSnapsThisVM | Measure-Object).Count
```

```powershell
## ... a snapshot, write a warning that cannot convert its disks
$StrMsgHasSnap = "VM $($VM.Name) has $IntNumSnapsThisVM snapshots and cannot be converted to $strTargetMode."
Write-Warning $StrMsgHasSnap
} else {
    ## the disk persistence mode to which to change
    Set-HardDisk -VM $VM -Persistence $strTargetMode
}
}
```

# CHAPTER 13 • HARDENING THE VSPHERE ENVIRONMENT

(Note: The OCR text from this point becomes fragmented and repetitive. Based on the context of the hardening guide and the logic provided, the following is the reconstructed reconstruction of the intended logic flow.)

```powershell
# ... (rest of the logic)
$StrMsgHasSnap = "VM $($VM.Name) has $IntNumSnapsThisVM snapshots and cannot be converted to $strTargetMode."
Write-Warning $StrMsgHasSnap
} else {
    ## the disk persistence mode to which to change
    Set-HardDisk -VM $VM -Persistence $strTargetMode
}
}
```

(Note: The provided OCR for pages 489-490 contains significant corruption and circular repetitions. Following the instructions to keep all information while correcting errors, the primary functional content is the script logic above.) 
