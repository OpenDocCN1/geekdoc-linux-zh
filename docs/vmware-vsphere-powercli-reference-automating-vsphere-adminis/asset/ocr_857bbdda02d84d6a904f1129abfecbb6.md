# FIGURE 19.2 Imported VMs with vApp

![](bbox=[0.287, 0.133, 0.882, 0.351])

# # Power Commands

PowerCLI gives you the ability to start, stop, restart, restart, suspend the vApps using the Start-CIVAApp, Stop-CIVAApp, Restart-CIVAApp, and Suspend-CIVAApp commands respectively. Running any of these four commands invokes the action on specified every virtual machine found within the vApp container. We recommend that all virtual machines within the vApp be powered off when using these cmdlets, rather than performing the action against specific virtual machines inside the vApp. This ensures that the vApp will start or shut down properly using the configuration that has been given.

The Stop-CIVAApp and Restart-CIVAApp cmdlets do not perform their actions gracefully. By means that using those commands is equivalent to hitting the power button or restart on your computer chassis; it does not actually initiate shutdown or restart at the guest operating system level. To be able to shut or restart your vApps gracefully, you can use the Stop-CIVAAppGuest and Restart-CIVAAppGuest cmdlets, respectively. To execute properly, these cmdlets require that VMware Tools be installed and running within the virtual machines. These commands will perform the action on each virtual machine within the vApp.

If it is determined that a vApp needs to be restarted (we recommend that you apply a power setting to the entire vApp rather than that specific virtual machines), it is best to restart it gracefully:

```
Get-CIVAApp -Name TestvApp | Restart-CIVAAppGuest -Confirm:$false
```

You can replace Restart-CIVAAppGuest with Stop-CIVAAppGuest in this code if you decide to shut the vApp down rather than restart it.