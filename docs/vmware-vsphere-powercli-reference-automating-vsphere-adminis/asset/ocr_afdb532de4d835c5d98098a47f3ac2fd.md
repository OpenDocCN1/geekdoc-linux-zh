# USE CUSTOMIZATION SPECIFICATIONS

247

# LISTING 7.5 Copy specification to create a custom IIS specification

```
Get-OSCustomizationSpec -Name 'Win2012R2' |
  New-OSCustomizationSpec -Name 'Win2012R2_IIS' |
  Set-OSCustomizationSpec -AutoLogonCount 1 |
  -GuiRunOnce 'cmd /C PowerShell.exe -Command "Add-WindowsFeature \
  Web-Server -IncludeAllSubFeature -IncludeManagementTools \
  -Restart"'
```

> NOTE The GuiRunOnce component within a customization specification has caused much confusion over the years. Remember, when it comes to a Windows machine, Sysprep is doing all the work—VMware is merely automating Sysprep. Therefore, the RunOnce component from Sysprep is not using any integration to automate the process. If you are having issues using the RunOnce component, see Sysprep's documentation at https://microsoft.com/en-us/library/cc76604928v-vs.1029.aspx. PowerShellCLI is just the facilitator in this transaction.

![](bbox=[0.893, 0.233, 0.966, 0.363])

# Using Customization Specifications

There are two ways to use an OS customization specification:

+   - Apply it to an existing powered-off VM.

+   - Attach to a template deployment.

Now, let's stick to using a powered-off machine. Although it's not well known, it is possible to use the Set-VM cmdlet to apply customization specifications to any guest, as long as that meets the minimum requirements described earlier.

The Set-VM cmdlet -OSCustomizationSpec parameter was intended to apply a customization specification to a cloned VM. However, there is nothing preventing it from being used on demand. Listing 7.6 uses a customization specification to change both the network adapter settings and the domain membership of an existing VM.

# LISTING 7.6 Employing customization specifications on demand

```
# Save the credential object with permission to join the domain.
$DomainCredentials = Get-Credential glnsize@vSphere.local
```