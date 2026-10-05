# CHAPTER 6 • CREATING VIRTUAL MACHINES

Service Automation (HP-BSA), you can benefit from automating your new VM creation. Even if you're using a basic OS provisioning tool like Windows Deployment Services, Symantec Ghost, Linux Kickstart, or Solaris JumpStart, there is still benefit. Automation ensures that the base hardware is exactly the same every time!

How can you create a virtual machine? Well, generally the way you solve problem in PowerCLI is by starting with a statement or question—for example, "I need to create an REHL6 VM with a thin-provisioned hard drive, 10 GB of RAM. I need to mount an ISO in datastore0, and the network should be on VLAN 22." From there, you parse it out into cmdlets, like in Listing 6.1.

# LISTING 6.1 Cmdlets to create a new VM

```
New-VM -Name RHEL6_01 \
-DiskMB 10240 \
-DiskStorageFormat thin \
-MemoryMB 1024 \
-GuestID rhel_64_Guest -Name VLAN 22 \
-Portgroup (Get-VDPortgroup) \
-CD \
Get-CDDrive -IsoPath "[datastore0]\u279/rhel-server-6.5-x86_64-boot.iso" \
-StartConnected:$true \
-Confirm:$false
```

> NOTE Good PowerShell code should be read as an English sentence.

Notice how that one-liner required the use of several cmdlets. The conventional wisdom would be that all aspects of creating a new VM would be performed with the New-VM cmdlet. This is not the case with PowerCLI, nor with PowerShell in general. Every cmdlet is responsible for one small task or function. There, more complex operations require multiple cmdlets to be chained into a pipeline to complete the whole task. For example, the New-VM cmdlet creates only the bare hardware. Everything beyond that—like connecting a CD—must be done after the VM has created.