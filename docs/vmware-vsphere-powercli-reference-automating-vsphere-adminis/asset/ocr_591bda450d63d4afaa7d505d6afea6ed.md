# CHAPTER 7 • USING TEMPLATES AND CUSTOMIZATION SPECIFICATIONS

to make it writable. Then, VMware Tools need to be upgraded. Once upgraded, the VM needs to be powered off. Then, the hardware version can be upgraded. For good measure, the template should be powered back on to see how it went.

Listing 7.18 breaks that process into code.

# LISTING 7.18 Safely upgrading the VM hardware

```
# get our template, convert it to a VM, and power said VM on.
$VM = Get-Template 'vm01' |
Set-Template -ToVM |
Start-VM |
Wait-VMGuest Startup
# kick off a tools update and wait for it to finish.
Update-Tools -VM $VM
Stop-VMGuest -VM $VM -Confirm:$false |
Wait-VMGuest Shutdown Out-Null
# Perform the hardware upgrade
$vm.ExtensionData.UpgradeVM("vmx-11")
# Power on our VM
Start-VM -VM $VM
# Log in and make sure the upgrade went okay.
# Power our VM back down
$VM = Stop-VMGuest -VM $VM -Confirm:$false |
Wait-VMGuest Shutdown
# Convert back to template
Set-VM -VM $VM -ToTemplate -Confirm:$false
```

Very straightforward! Given enough templates to justify the investment, it is possible to fully automate the complete upgrade life cycle. The Update-TemplateHardware function in Listing 7.19 does just that. This script handles the complete upgrade cycle and performs checks before making any modification to ensure it's only affecting templates that require an update.

# LISTING 7.19 Update-TemplateHardware

```
function Update-TemplateHardware {

[CmdletBinding()]
param(
```