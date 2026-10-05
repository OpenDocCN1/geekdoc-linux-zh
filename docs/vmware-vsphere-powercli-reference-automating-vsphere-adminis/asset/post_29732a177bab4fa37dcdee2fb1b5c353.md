
enough to work in such an environment should keep doing what they do. For the rest of us, there are customization specifications.

OS customization specifications are the glue that make templates whatever they are. To illustrate, the next section will go through a series of deployments, gradually cranking up the complexity. To begin a standard Windows Server deployment using a static IP address via the customization specification, see 7.10.

## LISTING 7.10 Assigning a static IP address to a Windows Server using a customization specification

```powershell
# Update Spec Customization with our desired IP information
Get-OSCustomizationSpec -Name 'Win2012R2' |
  Get-OSCustomizationNicMapping |
    Set-OSCustomizationNicMapping -IPMode UseStaticIP \
      IpAddress '192.168.2.165' \
      SubnetMask '255.255.255.0' \
      DefaultGateway '192.168.2.1' \
      Dns '192.168.2.8','192.168.2.1'
# Get updated Spec Object
$Spec = Get-OSCustomizationSpec -Name 'Win2012R2'
# Get Template to deploy from
$Template = Get-Template -Name 'WS2012R2'
# Get VMHost to deploy new VM on
$VMHost = Get-VMHost -Name 'vSphere1'
# Deploy VM
New-VM -Name 'WEB001' \
  -VMHost $VMHost \
  -Template $Template \
  -OSCustomizationSpec $Spec \
  Start-VM
```

The workflow is somewhat backward, but it makes sense once the underlying mechanism is explained. First, the customization specification was modified to use the desired IP address. Here is where it gets a little crazy: the update is applied to the actual customization specification—this isn an an object in memory. Once the new modified customization object is retrieved from vCenter Server with the template and VMHost object, a simple call of the New-VM cmdlet will deploy the new virtual machine.

# CHAPTER 7 • USING TEMPLATES AND CUSTOMIZATION SPECIFICATIONS

Notice in Listing 7.10 that the New-VM object is piped into Start-VM. This is strongly advised because customization information isn't in the guest yet—and not until VM is powered on for the first time. Once the new virtual machine is powered for the first time, vCenter waits for VMware Tools to report in. After the Tools report for the first time, vCenter Servers copies an OS customization script to the guest VM and then calls a series of finalization scripts that perform the guest customization.

Although completely functional, both of the previous examples had one critical flaw: they modified the customization specification stored on vCenter Server. This behavior is especially troublesome as it will permanently modify the source specification. To work around this, using nonresident OS customization specifications. The process looks identical to the process in Listing 7.10 with one exception: before making any modifications, the customization specification is cloned to a nonpersistent specification. This step enables the modification of the specification without affecting the copy stored on vCenter Server. The code contained in Listing 7.11 deploys another Windows Server performing the same customization as before but this time leaving the master copy on vCenter Server unaffected.

## LISTING 7.11 Cloning a customization to a nonpersistent specification

```powershell
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
-Template $Template 
-OSCustomizationSpec $Spec |
Start-VM
```

> WARNING When you use a nonpersistent customization specification, it is stored in the memory of that PowerCLI session. Other PowerCLI sessions have no knowledge of access to the cloned customization specification. However, within the session where the customization is created, the nonpersistent specification is managed as if it were a persistent specification—meaning you cannot have two specs with the same name.

![](img/62596f5acc979040608a4e5111beb7d6_284_0.png)

Thus, all of our examples have only a single network adapter. What about a machine with multiple network adapters? Well, as it turns out, the process is almost exactly the same. The only difference is that each adapter must be specifically targeted by position. Therefore, the current Nic position must be known for each Nic. This information can be retrieved by running the Get-OSCustomizationNicMapping cmdlet for the spec you have modified:

| SpecId | Position | IPMode | IPAddress | DefaultGateway |
|---|---|---|---|
| Win2012R2_IIS | 1 | UseStaticIP | 192.168.2.165 | 192.168.2.1 |
| Win2012R2_IIS | 2 | Static | 192.168.2.42 | 192.168.2.1 |

# CHAPTER 7 • USING TEMPLATES AND CUSTOMIZATION SPECIFICATIONS

```powershell
# Update Spec Customization with our desired IP information
Get-OSCustomizationSpec -Name 'Win2012R2' |
  Get-OSCustomizationNicMapping |
    Set-OSCustomizationNicMapping -IPMode UseStaticIP \
      IpAddress '192.168.2.165' \
      SubnetMask '255.255.255.0' \
      DefaultGateway '192.168.2.1' \
      Dns '192.168.2.8','192.168.2.1'
# Get updated Spec Object
$Spec = Get-OSCustomizationSpec -Name 'Win2012R2'
# Get Template to deploy from
$Template = Get-Template -Name 'WS2012R2'
# Get VMHost to deploy new VM on
$VMHost = Get-VMHost -Name 'vSphere1'
# Deploy VM
New-VM -Name 'WEB001' \
  -VMHost $VMHost \
  -Template $Template \
  -OSCustomizationSpec $Spec \
  Start-VM
```

The workflow is somewhat backward, but it makes sense once the underlying mechanism is explained. First, the customization specification was modified to use the desired IP address. Here is where it gets a little crazy: the update is applied to the actual customization specification—this isn an an object in memory. Once the new modified customization object is retrieved from vCenter Server with the template and VMHost object, a simple call of the New-VM cmdlet will deploy the new virtual machine.

Notice in Listing 7.10 that the New-VM object is piped into Start-VM. This is strongly advised because customization information isn't in the guest yet—and not until VM is powered on for the first time. Once the new virtual machine is powered for the first time, vCenter waits for VMware Tools to report in. After the Tools report for the first time, vCenter Servers copies an OS customization script to the guest VM and then calls a series of finalization scripts that perform the guest customization.

Although completely functional, both of the previous examples had one critical flaw: they modified the customization specification stored on vCenter Server. This behavior is especially troublesome as it will permanently modify the source specification. To work around this, using nonresident OS customization specifications. The process looks identical to the process in Listing 7.10 with one exception: before making any modifications, the customization specification is cloned to a nonpersistent specification. This step enables the modification of the specification without affecting the copy stored on vCenter Server. The code contained in Listing 7.11 deploys another Windows Server performing the same customization as before but this time leaving the master copy on vCenter Server unaffected.

## LISTING 7.11 Cloning a customization to a nonpersistent specification

```powershell
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
-Template $Template 
-OSCustomizationSpec $Spec |
Start-VM
```

> WARNING When you use a nonpersistent customization specification, it is stored in the memory of that PowerCLI session. Other PowerCLI sessions have no knowledge of access to the cloned customization specification. However, within the session where the customization is created, the nonpersistent specification is managed as if it were a persistent specification—meaning you cannot have two specs with the same name.

![](img/62596f5acc979040608a4e5111beb7d6_284_0.png)

Thus, all of our examples have only a single network adapter. What about a machine with multiple network adapters? Well, as it turns out, the process is almost exactly the same. The only difference is that each adapter must be specifically targeted by position. Therefore, the current Nic position must be known for each Nic. This information can be retrieved by running the Get-OSCustomizationNicMapping cmdlet for the spec you have modified:

| SpecId | Position | IPMode | IPAddress | DefaultGateway |
|---|---|---|---|
| Win2012R2_IIS | 1 | UseStaticIP | 192.168.2.165 | 192.168.2.1 |
| Win2012R2_IIS | 2 | Static | 192.168.2.42 | 192.168.2.1 |

# CHAPTER 7 • USING TEMPLATES AND CUSTOMIZATION SPECIFICATIONS

```powershell
# Update Spec Customization with our desired IP information
Get-OSCustomizationSpec -Name 'Win2012R2' |
  Get-OSCustomizationNicMapping |
    Set-OSCustomizationNicMapping -IPMode UseStaticIP \
      IpAddress '192.168.2.165' \
      SubnetMask '255.255.255.0' \
      DefaultGateway '192.168.2.1' \
      Dns '192.168.2.8','192.168.2.1'
# Get updated Spec Object
$Spec = Get-OSCustomizationSpec -Name 'Win2012R2'
# Get Template to deploy from
$Template = Get-Template -Name 'WS2012R2'
# Get VMHost to deploy new VM on
$VMHost = Get-VMHost -Name 'vSphere1'
# Deploy VM
New-VM -Name 'WEB001' \
  -VMHost $VMHost \
  -Template $Template \
  -OSCustomizationSpec $Spec \
  Start-VM
```

The workflow is somewhat backward, but it makes sense once the underlying mechanism is explained. First, the customization specification was modified to use the desired IP address. Here is where it gets a little crazy: the update is applied to the actual customization specification—this isn an an object in memory. Once the new modified customization object is retrieved from vCenter Server with the template and VMHost object, a simple call of the New-VM cmdlet will deploy the new virtual machine.

Notice in Listing 7.10 that the New-VM object is piped into Start-VM. This is strongly advised because customization information isn't in the guest yet—and not until VM is powered on for the first time. Once the new virtual machine is powered for the first time, vCenter waits for VMware Tools to report in. After the Tools report for the first time, vCenter Servers copies an OS customization script to the guest VM and then calls a series of finalization scripts that perform the guest customization.

Although completely functional, both of the previous examples had one critical flaw: they modified the customization specification stored on vCenter Server. This behavior is especially troublesome as it will permanently modify the source specification. To work around this, using nonresident OS customization specifications. The process looks identical to the process in Listing 7.10 with one exception: before making any modifications, the customization specification is cloned to a nonpersistent specification. This step enables the modification of the specification without affecting the copy stored on vCenter Server. The code contained in Listing 7.11 deploys another Windows Server performing the same customization as before but this time leaving the master copy on vCenter Server unaffected.

## LISTING 7.11 Cloning a customization to a nonpersistent specification

```powershell
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
-Template $Template 
-OSCustomizationSpec $Spec |
Start-VM
```

> WARNING When you use a nonpersistent customization specification, it is stored in the memory of that PowerCLI session. Other PowerCLI sessions have no knowledge of access to the cloned customization specification. However, within the session where the customization is created, the nonpersistent specification is managed as if it were a persistent specification—meaning you cannot have two specs with the same name.

![](img/62596f5acc979040608a4e5111beb7d6_284_0.png)

Thus, all of our examples have only a single network adapter. What about a machine with multiple network adapters? Well, as it turns out, the process is almost exactly the same. The only difference is that each adapter must be specifically targeted by position. Therefore, the current Nic position must be known for each Nic. This information can be retrieved by running the Get-OSCustomizationNicMapping cmdlet for the spec you have modified:

| SpecId | Position | IPMode | IPAddress | DefaultGateway |
|---|---|---|---|
| Win2012R2_IIS | 1 | UseStaticIP | 192.168.2.165 | 192.168.2.1 |
| Win2012R2_IIS | 2 | Static | 192.168.2.42 | 192.168.2.1 |

# CHAPTER 7 • USING TEMPLATES AND CUSTOMIZATION SPECIFICATIONS

```powershell
# Update Spec Customization with our desired IP information
Get-OSCustomizationSpec -Name 'Win2012R2' |
  Get-OSCustomizationNicMapping |
    Set-OSCustomizationNicMapping -IPMode UseStaticIP \
      IpAddress '192.168.2.165' \
      SubnetMask '255.255.255.0' \
      DefaultGateway '192.168.2.1' \
      Dns '192.168.2.8','192.168.2.1'
# Get updated Spec Object
$Spec = Get-OSCustomizationSpec -Name 'Win2012R2'
# Get Template to deploy from
$Template = Get-Template -Name 'WS2012R2'
# Get VMHost to deploy new VM on
$VMHost = Get-VMHost -Name 'vSphere1'
# Deploy VM
New-VM -Name 'WEB001' \
  -VMHost $VMHost \
  -Template $Template \
  -OSCustomizationSpec $Spec \
  Start-VM
```

The workflow is somewhat backward, but it makes sense once the underlying mechanism is explained. First, the customization specification was modified to use the desired IP address. Here is where it gets a little crazy: the update is applied to the actual customization specification—this isn an an object in memory. Once the new modified customization object is retrieved from vCenter Server with the template and VMHost object, a simple call of the New-VM cmdlet will deploy the new virtual machine.

Notice in Listing 7.10 that the New-VM object is piped into Start-VM. This is strongly advised because customization information isn't in the guest yet—and not until VM is powered on for the first time. Once the new virtual machine is powered for the first time, vCenter waits for VMware Tools to report in. After the Tools report for the first time, vCenter Servers copies an OS customization script to the guest VM and then calls a series of finalization scripts that perform the guest customization.

Although completely functional, both of the previous examples had one critical flaw: they modified the customization specification stored on vCenter Server. This behavior is especially troublesome as it will permanently modify the source specification. To work around this, using nonresident OS customization specifications. The process looks identical to the process in Listing 7.10 with one exception: before making any modifications, the customization specification is cloned to a nonpersistent specification. This step enables the modification of the specification without affecting the copy stored on vCenter Server. The code contained in Listing 7.11 deploys another Windows Server performing the same customization as before but this time leaving the master copy on vCenter Server unaffected.

## LISTING 7.11 Cloning a customization to a nonpersistent specification

```powershell
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
-Template $Template 
-OSCustomizationSpec $Spec |
Start-VM
```

> WARNING When you use a nonpersistent customization specification, it is stored in the memory of that PowerCLI session. Other PowerCLI sessions have no knowledge of access to the cloned customization specification. However, within the session where the customization is created, the nonpersistent specification is managed as if it were a persistent specification—meaning you cannot have two specs with the same name.

![](img/62596f5acc979040608a4e5111beb7d6_284_0.png)

Thus, all of our examples have only a single network adapter. What about a machine with multiple network adapters? Well, as it turns out, the process is almost exactly the same. The only difference is that each adapter must be specifically targeted by position. Therefore, the current Nic position must be known for each Nic. This information can be retrieved by running the Get-OSCustomizationNicMapping cmdlet for the spec you have modified:

| SpecId | Position | IPMode | IPAddress | DefaultGateway |
|---|---|---|---|
| Win2012R2_IIS | 1 | UseStaticIP | 192.168.2.165 | 192.168.2.1 |
| Win2012R2_IIS | 2 | Static | 192.168.2.42 | 192.168.2.1 |

# CHAPTER 7 • USING TEMPLATES AND CUSTOMIZATION SPECIFICATIONS

```powershell
# Update Spec Customization with our desired IP information
Get-OSCustomizationSpec -Name 'Win2012R2' |
  Get-OSCustomizationNicMapping |
    Set-OSCustomizationNicMapping -IPMode UseStaticIP \
      IpAddress '192.168.2.165' \
      SubnetMask '255.255.255.0' \
      DefaultGateway '192.168.2.1' \
      Dns '192.168.2.8','192.168.2.1'
# Get updated Spec Object
$Spec = Get-OSCustomizationSpec -Name 'Win2012R2'
# Get Template to deploy from
$Template = Get-Template -Name 'WS2012R2'
# Get VMHost to deploy new VM on
$VMHost = Get-VMHost -Name 'vSphere1'
# Deploy VM
New-VM -Name 'WEB001' \
  -VMHost $VMHost \
  -Template $Template \
  -OSCustomizationSpec $Spec \
  Start-VM
```

The workflow is somewhat backward, but it makes sense once the underlying mechanism is explained. First, the customization specification was modified to use the desired IP address. Here is where it gets a little crazy: the update is applied to the actual customization specification—this isn an an object in memory. Once the new modified customization object is retrieved from vCenter Server with the template and VMHost object, a simple call of the New-VM cmdlet will deploy the new virtual machine.

Notice in Listing 7.10 that the New-VM object is piped into Start-VM. This is strongly advised because customization information isn't in the guest yet—and not until VM is powered on for the first time. Once the new virtual machine is powered for the first time, vCenter waits for VMware Tools to report in. After the Tools report for the first time, vCenter Servers copies an OS customization script to the guest VM and then calls a series of finalization scripts that perform the guest customization.

Although completely functional, both of the previous examples had one critical flaw: they modified the customization specification stored on vCenter Server. This behavior is especially troublesome as it will permanently modify the source specification. To work around this, using nonresident OS customization specifications. The process looks identical to the process in Listing 7.10 with one exception: before making any modifications, the customization specification is cloned to a nonpersistent specification. This step enables the modification of the specification without affecting the copy stored on vCenter Server. The code contained in Listing 7.11 deploys another Windows Server performing the same customization as before but this time leaving the master copy on vCenter Server unaffected.

## LISTING 7.11 Cloning a customization to a nonpersistent specification

```powershell
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
-Template $Template 
-OSCustomizationSpec $Spec |
Start-VM
```

> WARNING When you use a nonpersistent customization specification, it is stored in the memory of that PowerCLI session. Other PowerCLI sessions have no knowledge of access to the cloned customization specification. However, within the session where the customization is created, the nonpersistent specification is managed as if it were a persistent specification—meaning you cannot have two specs with the same name.

![](img/62596f5acc979040608a4e5111beb7d6_284_0.png)

Thus, all of our examples have only a single network adapter. What about a machine with multiple network adapters? Well, as it turns out, the process is almost exactly the same. The only difference is that each adapter must be specifically targeted by position. Therefore, the current Nic position must be known for each Nic. This information can be retrieved by running the Get-OSCustomizationNicMapping cmdlet for the spec you have modified:

| SpecId | Position | IPMode | IPAddress | DefaultGateway |
|---|---|---|---|
| Win2012R2_IIS | 1 | UseStaticIP | 192.168.2.165 | 192.168.2.1 |
| Win2012R2_IIS | 2 | Static | 192.168.2.42 | 192.168.2.1 |

# CHAPTER 7 • USING TEMPLATES AND CUSTOMIZATION SPECIFICATIONS

```powershell
# Update Spec Customization with our desired IP information
Get-OSCustomizationSpec -Name 'Win2012R2' |
  Get-OSCustomizationNicMapping |
    Set-OSCustomizationNicMapping -IPMode UseStaticIP \
      IpAddress '192.168.2.165' \
      SubnetMask '255.255.255.0' \
      DefaultGateway '192.168.2.1' \
      Dns '192.168.2.8','192.168.2.1'
# Get updated Spec Object
$Spec = Get-OSCustomizationSpec -Name 'Win2012R2'
# Get Template to deploy from
$Template = Get-Template -Name 'WS2012R2'
# Get VMHost to deploy new VM on
$VMHost = Get-VMHost -Name 'vSphere1'
# Deploy VM
New-VM -Name 'WEB001' \
  -VMHost $VMHost \
  -Template $Template \
  -OSCustomizationSpec $Spec \
  Start-VM
```

The workflow is somewhat backward, but it makes sense once the underlying mechanism is explained. First, the customization specification was modified to use the desired IP address. Here is where it gets a little crazy: the update is applied to the actual customization specification—this isn an an object in memory. Once the new modified customization object is retrieved from vCenter Server with the template and VMHost object, a simple call of the New-VM cmdlet will deploy the new virtual machine.

Notice in Listing 7.10 that the New-VM object is piped into Start-VM. This is strongly advised because customization information isn't in the guest yet—and not until VM is powered on for the first time. Once the new virtual machine is powered for the first time, vCenter waits for VMware Tools to report in. After the Tools report for the first time, vCenter Servers copies an OS customization script to the guest VM and then calls a series of finalization scripts that perform the guest customization.

Although completely functional, both of the previous examples had one critical flaw: they modified the customization specification stored on vCenter Server. This behavior is especially troublesome as it will permanently modify the source specification. To work around this, using nonresident OS customization specifications. The process looks identical to the process in Listing 7.10 with one exception: before making any modifications, the customization specification is cloned to a nonpersistent specification. This step enables the modification of the specification without affecting the copy stored on vCenter Server. The code contained in Listing 7.11 deploys another Windows Server performing the same customization as before but this time leaving the master copy on vCenter Server unaffected.

## LISTING 7.11 Cloning a customization to a nonpersistent specification

```powershell
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
-Template $Template 
-OSCustomizationSpec $Spec |
Start-VM
```

> WARNING When you use a nonpersistent customization specification, it is stored in the memory of that PowerCLI session. Other PowerCLI sessions have no knowledge of access to the cloned customization specification. However, within the session where the customization is created, the nonpersistent specification is managed as if it were a persistent specification—meaning you cannot have two specs with the same name.

![](img/62596f5acc979040608a4e5111beb7d6_284_0.png)

Thus, all of our examples have only a single network adapter. What about a machine with multiple network adapters? Well, as it turns out, the process is almost exactly the same. The only difference is that each adapter must be specifically targeted by position. Therefore, the current Nic position must be known for each Nic. This information can be retrieved by running the Get-OSCustomizationNicMapping cmdlet for the spec you have modified:

| SpecId | Position | IPMode | IPAddress | DefaultGateway |
|---|---|---|---|
| Win2012R2_IIS | 1 | UseStaticIP | 192.168.2.165 | 192.168.2.1 |
| Win2012R2_IIS | 2 | Static | 192.168.2.42 | 192.168.2.1 |

# CHAPTER 7 • USING TEMPLATES AND CUSTOMIZATION SPECIFICATIONS

```powershell
# Update Spec Customization with our desired IP information
Get-OSCustomizationSpec -Name 'Win2012R2' |
  Get-OSCustomizationNicMapping |
    Set-OSCustomizationNicMapping -IPMode UseStaticIP \
      IpAddress '192.168.2.165' \
      SubnetMask '255.255.255.0' \
      DefaultGateway '192.168.2.1' \
      Dns '192.168.2.8','192.168.2.1'
# Get updated Spec Object
$Spec = Get-OSCustomizationSpec -Name 'Win2012R2'
# Get Template to deploy from
$Template = Get-Template -Name 'WS2012R2'
# Get VMHost to deploy new VM on
$VMHost = Get-VMHost -Name 'vSphere1'
# Deploy VM
New-VM -Name 'WEB001' \
  -VMHost $VMHost \
  -Template $Template \
  -OSCustomizationSpec $Spec \
  Start-VM
```

The workflow is somewhat backward, but it makes sense once the underlying mechanism is explained. First, the customization specification was modified to use the desired IP address. Here is where it gets a little crazy: the update is applied to the actual customization specification—this isn an an object in memory. Once the new modified customization object is retrieved from vCenter Server with the template and VMHost object, a simple call of the New-VM cmdlet will deploy the new virtual machine.

Notice in Listing 7.10 that the New-VM object is piped into Start-VM. This is strongly advised because customization information isn't in the guest yet—and not until VM is powered on for the first time. Once the new virtual machine is powered for the first time, vCenter waits for VMware Tools to report in. After the Tools report for the first time, vCenter Servers copies an OS customization script to the guest VM and then calls a series of finalization scripts that perform the guest customization.

Although completely functional, both of the previous examples had one critical flaw: they modified the customization specification stored on vCenter Server. This behavior is especially troublesome as it will permanently modify the source specification. To work around this, using nonresident OS customization specifications. The process looks identical to the process in Listing 7.10 with one exception: before making any modifications, the customization specification is cloned to a nonpersistent specification. This step enables the modification of the specification without affecting the copy stored on vCenter Server. The code contained in Listing 7.11 deploys another Windows Server performing the same customization as before but this time leaving the master copy on vCenter Server unaffected.

## LISTING 7.11 Cloning a customization to a nonpersistent specification

```powershell
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
-Template $Template 
-OSCustomizationSpec $Spec |
Start-VM
```

> WARNING When you use a nonpersistent customization specification, it is stored in the memory of that PowerCLI session. Other PowerCLI sessions have no knowledge of access to the cloned customization specification. However, within the session where the customization is created, the nonpersistent specification is managed as if it were a persistent specification—meaning you cannot have two specs with the same name.

![](img/62596f5acc979040608a4e5111beb7d6_284_0.png)

Thus, all of our examples have only a single network adapter. What about a machine with multiple network adapters? Well, as it turns out, the process is almost exactly the same. The only difference is that each adapter must be specifically targeted by position. Therefore, the current Nic position must be known for each Nic. This information can be retrieved by running the Get-OSCustomizationNicMapping cmdlet for the spec you have modified:

| SpecId | Position | IPMode | IPAddress | DefaultGateway |
|---|---|---|---|
| Win2012R2_IIS | 1 | UseStaticIP | 192.168.2.165 | 192.168.2.1 |
| Win2012R2_IIS | 2 | Static | 192.168.2.42 | 192.168.2.1 |

# CHAPTER 7 • USING TEMPLATES AND CUSTOMIZATION SPECIFICATIONS

```powershell
# Update Spec Customization with our desired IP information
Get-OSCustomizationSpec -Name 'Win2012R2' |
  Get-OSCustomizationNicMapping |
    Set-OSCustomizationNicMapping -IPMode UseStaticIP \
      IpAddress '192.168.2.165' \
      SubnetMask '255.255.255.0' \
      DefaultGateway '192.168.2.1' \
      Dns '192.168.2.8','192.168.2.1'
# Get updated Spec Object
$Spec = Get-OSCustomizationSpec -Name 'Win2012R2'
# Get Template to deploy from
$Template = Get-Template -Name 'WS2012R2'
# Get VMHost to deploy new VM on
$VMHost = Get-VMHost -Name 'vSphere1'
# Deploy VM
New-VM -Name 'WEB001' \
  -VMHost $VMHost \
  -Template $Template \
  -OSCustomizationSpec $Spec \
  Start-VM
```

The workflow is somewhat backward, but it makes sense once the underlying mechanism is explained. First, the customization specification was modified to use the desired IP address. Here is where it gets a little crazy: the update is applied to the actual customization specification—this isn an an object in memory. Once the new modified customization object is retrieved from vCenter Server with the template and VMHost object, a simple call of the New-VM cmdlet will deploy the new virtual machine.

Notice in Listing 7.10 that the New-VM object is piped into Start-VM. This is strongly advised because customization information isn't in the guest yet—and not until VM is powered on for the first time. Once the new virtual machine is powered for the first time, vCenter waits for VMware Tools to report in. After the Tools report for the first time, vCenter Servers copies an OS customization script to the guest VM and then calls a series of finalization scripts that perform the guest customization.

Although completely functional, both of the previous examples had one critical flaw: they modified the customization specification stored on vCenter Server. This behavior is especially troublesome as it will permanently modify the source specification. To work around this, using nonresident OS customization specifications. The process looks identical to the process in Listing 7.10 with one exception: before making any modifications, the customization specification is cloned to a nonpersistent specification. This step enables the modification of the specification without affecting the copy stored on vCenter Server. The code contained in Listing 7.11 deploys another Windows Server performing the same customization as before but this time leaving the master copy on vCenter Server unaffected.

## LISTING 7.11 Cloning a customization to a nonpersistent specification

```powershell
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
-Template $Template 
-OSCustomizationSpec $Spec |
Start-VM
```

> WARNING When you use a nonpersistent customization specification, it is stored in the memory of that PowerCLI session. Other PowerCLI sessions have no knowledge of access to the cloned customization specification. However, within the session where the customization is created, the nonpersistent specification is managed as if it were a persistent specification—meaning you cannot have two specs with the same name.

![](img/62596f5acc979040608a4e5111beb7d6_284_0.png)
