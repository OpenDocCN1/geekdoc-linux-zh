# CHAPTER 7 • USING TEMPLATES AND CUSTOMIZATION SPECIFICATIONS

Notice in Listing 7.10 that the New-VM object is piped into Start-VM. This is strongly advised because customization information isn't in the guest yet—and not until VM is powered on for the first time. Once the new virtual machine is powered for the first time, vCenter waits for VMware Tools to report in. After the Tools report for the first time, vCenter Servers copies an OS customization script to the guest VM and then calls a series of finalization scripts that perform the guest customization.

Although completely functional, both of the previous examples had one critical flaw: they modified the customization specification stored on vCenter Server. This behavior is especially troublesome as it will permanently modify the source specification. To work around this, using nonresident OS customization specifications. The process looks identical to the process in Listing 7.10 with one exception: before making any modifications, the customization specification is cloned to a nonpersistent specification. This step enables the modification of the specification without affecting the copy stored on vCenter Server. The code contained in Listing 7.11 deploys another Windows Server performing the same customization as before but this time leaving the master copy on vCenter Server unaffected.

# LISTING 7.11 Cloning a customization to a nonpersistent specification

```
# Clone our Spec
$Spec = Get-OSCustomizationSpec 'Win2012R2' |
New-OSCustomizationSpec -Name 'tmp01' -Type NonPersistent
# Update Spec with our desired IP information
Get-OSCustomizationNiMapping -Spec $Spec |
Set-OSCustomizationNiMapping -IPMode Static|
-IpAddress '192.168.2.42' |
-SubMask '255.255.255.0' |
-DefaultGateway '192.168.2.1' |
-Dns '192.168.2.8', '192.168.2.1'

# Get updated Spec Object
$Spec = Get-OSCustomizationSpec -Name 'tmp01'
# Get Template to deploy from
$Template = Get-Template -Name 'Win2012R2'
# GetVMHost to deploy new VM on
$VMHost = Get-VMHost -Name 'vSphere'
# Deploy VM
New-VM -Name 'WEB001' \
-VMHost $VMHost
```