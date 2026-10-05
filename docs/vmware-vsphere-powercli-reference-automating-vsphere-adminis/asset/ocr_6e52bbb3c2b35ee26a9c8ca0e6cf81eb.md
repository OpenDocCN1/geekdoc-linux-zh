# LISTING 6.20 Updating VMware Tools for a Linux guest

```
$cmd = Get-Content \installTools.sh | Out-String
Mount-Tools -VM $VM `
Invoke-VMScript -VM $VM \
  -GuestCredential $guestCreds \
  -HostCredential $hostCreds \
  -ScriptText $cmd
Dismount-Tools -VM $VM`
```

> **WARNING** Be sure to coordinate with the virtual machine owner before triggering a VMware Tools update. Exploiting this connection to the VM is shaky at best—and potentially illegal. Be up front and tell the truth; most admins appreciate the help and will work with you.

# Automatically Updating VMware Tools

Of course there is the option to simply allow VMware Tools to automatically update upon the next power cycle. This is not an option for all, as some organizations require strict control over all installed software. However, if you are able, the simplest method is to set the tools upgrade policy to Upgrade At Power Cycle, as we did in Listing 6.21.

# LISTING 6.21 Set the tools upgrade policy to Upgrade At Power Cycle

```
$spec = New-Object VMware.Vim.VirtualMachineConfigSpec
$spec.tools = New-Object VMware.Vim.ToolsConfigInfo
$spec.tools.toolsUpgradePolicy = "upgradeAtPowerCycle"
$VM = Get-VM App04
$VM.ExtensionData.ReconfigVM($spec)
```