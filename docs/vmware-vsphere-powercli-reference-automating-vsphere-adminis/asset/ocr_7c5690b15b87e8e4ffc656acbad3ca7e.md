# CHAPTER 12 ORGANIZE YOUR DISASTER RECOVERY

```
-Name $Entity | New-TagAssignment -Tag $ \
-"DistributedPortGroup" { Get-VDPortgroup \
-Name $Entity | New-TagAssignment -Tag $ \
-"DistributedSwitch" { Get-VDSwitch \
-Name $Entity | New-TagAssignment -Tag $ \
-"Folder" { Get-Folder -Name $Entity | \
New-TagAssignment -Tag $ \
-"Host" { Get-VMHost -Name $Entity | \
New-TagAssignment -Tag $ \
-"Network" { Get-VirtualSwitch -Name $Entity | \
New-TagAssignment -Tag $ \
-"ResourcePool" { Get-ResourcePool -Name $Entity | \
New-TagAssignment -Tag $ \
-"vApp" { Get-VApp -Name $Entity | \
New-TagAssignment -Tag $ \
-"vCOScheduledWorkflow" { Write-Host "$Entity is a \
vCOScheduledWorkflow and will need to be tagged \
manually with: ("$tag") -ForegroundColor Red \
-"vCOWorkflow" { Write-Host "$Entity is a vCOWorkflow \
will need to be tagged manually with: \
("$tag") -ForegroundColor Red \
-"VirtualMachine" { Get-VM -Name $Entity | \
New-TagAssignment -Tag $ \
}
}
```

# Recover Virtual Machines

If you've lost the ESXI host and have to reinstall or restore it, you've also lost all VM registrations. So, you'll need register your VMs before you can restore your VMs to their original location. To register a VM, you'll need the exact path of its VMX file. You could browse your datastores using the vSphere Client and register every VMX file found at one, or use PowerCLI to do this daunting task for you.
Browsing the datastores from the PowerCLI console is very easy, because PowerCLI includes a datastore provider. To view all installed providers, use the Get-PSProvider cmdlet, and to view mapped drives, use the Get-PSDrive cmdlet.