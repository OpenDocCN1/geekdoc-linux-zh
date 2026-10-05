# # If it's not part of vCenter add it back in.
Get-Datastore |

```
Search-Datastore -Pattern *.vmx |
Where-Object { $RegisteredVMs -notcontains $_.path }
Where-Object { $_.path -match "(?<Name>\w+)..vmx" }
ForEach-Object {
$VMHost = Get-Datastore -Name $_.Datastore |
Get-VMHost -State Connected
Get-Random
New-VM -Name $matches.Name `
-VMHost $VMHost `
-VMFilePath $_.Path
}
```

At this point, we can all agree that the New-VM cmdlet is very powerful and for the most part can accommodate all your virtual machine creation needs. We urge you to use the built-in supported cmdlets if doing so requires more work than using the SDK. It is infinitely easier for a novice to read and understand a snippet written with the supported cmdlets. However, if you find yourself in a situation where the cmdlets can't quite meet your requirements, remember there is always the SDK.

# Perform a Mass Deployment

Shortly after realizing the power, space, and cloud savings that virtualization brings to the table, organizations usually need the speed of deployment. This discovery isn't all roses, though, as it brings with it the need to pump out virtual many times faster than is feasible in the physical world. Fear not! As you'll soon learn, with PowerCLI no project is too big!

# Preparing for Mass Deployment

egardless of whether you are planning to use a third-party provisioning tool (such as SCCM) or you have established a gold master image, PowerCLI enables you to effortlessly scale to any size deployment. The real question is, how unique is each virtual machine? If you're deploying 1,000 blank Linux virtual machines to load from Kickstart, it's one line (see Listing 6.9)!