# CONFIGURE ACTIVE DIRECTORY INTEGRATION

New-Datastore -Name prod01_03 
-Nfs 
-NfsHost 192.168.1.3 
-Path /vol/prod01_03

```
# get the profile for the cluster
$VMHostProfile = $cluster | Get-VMHostProfile
```

```
# update the profile from the reference host
$profileSpec = New-Object VMware.Vim.HostProfileBasedConfigSpec
$profileSpec.host = =
(Get-View -Id $VMHostProfile.ReferenceHostId -Property Name).MoreRef
$profileSpec.useHostProfileEngine = $true
```

```
$VMHostProfile.ExtensionData.UpdateHostProfile($profileSpec )
```

```
# test compliance for all hosts
$cluster | Get-VMHost | Test-VMHostProfileCompliance
```

If you are fortunate to have the licensing, enjoy host profiles! They are a fan-astic tool that truly simplifies the management of any size environment.

# Configure Active Directory Integration

Active Directory (AD) integration has been refined over the last versions of PowerCLI and has been simplified down to just two commands: Get-VMHostAuthentication (Listing 5.24) and Set-VMHostAuthentication (Listing 5.25). Using AD to authenticate users for vSphere Hypervisor is a simple, easy-to-maintain, and efficient method of ensuring that only authorized users are able to connect to the hosts using the CLI or vSphere Client. Using this method provides a quick and easy way to ensure that when administrators join or leave your team, their can quickly be updated from a single point.

LISTING 5.24 Getting the current host authentication settings

```
Get-VMHost $hostname | Get-VMHostAuthentication
```

| Domain | DomainMembershipStatus | TrustedDomains |
| --- | --- | --- |
| ____ | ---- | ---- |