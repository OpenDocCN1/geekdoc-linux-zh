Once the escli command has been converted, you might want to consider wrapping it into a PowerShell function, similar to the Get-VMHostCSIBinding and Set-VMHostCSIBindinging functions, in order to make it feel more like a native PowerShell CLI cmdlet.

# # Setting a Multipath Policy

If you are using Fibre Channel SAN, it's a good practice to use multiple HBA connections to the SAN whenever possible. With multiple HBA connections in place, should an active path to your SAN fail, a passive path is then made active so that storage traffic continues and the ESXI hosts remain connected to the storage for your VMs. Multipathing in vSphere makes it simple to use/Active Multipathing instead of Active/Passive if the array supports it. This means that not only you have resiliency in case of a failed path, you are also able to boost your storage performance by using multiple paths to the storage. The Native Multipathing Plug-in (NMP) module communicates with the Storage Array Type Plug-in (SATP) and the Path Selection Plug-in (PSP) to make these multipathing work.

> Contact your storage vendor before continuing further to support your storage array and to learn which to use SATP and PSP on the ESXi host.

Assuming your storage array is supported for multipathing and you have chosen the correct SATP to use, you need to configure the PSP on each LUN where you wish to multipathing. The PSP is per LUN and can take three values: Fixed, MostRecentlyUsed, or Robin—check your vendor documentation for which one to use. You can use a mixture of selections, it's a good idea to find what is currently used. To do that, you can use the Get-ScsLun cmdlet and select MultipathPolicy property.

```
Get-VMHost vsxi05* | Get-ScsLun | Select CanonicalName, MultipathPolicy
```

| CanonicalName | MultipathPolicy |
| --- | --- |
| mpx.vmhba32:C0:T0:L0 | Fixed |
| naa.600616019a93408059cb521a9bca22 | MostRecentlyUsed |