```
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
-NoProfile
-NonInteractive -Command C:\Scripts\Test-ReturnCodeLocal.ps1 -a
3;
exit $LASTEXITCODE
[2015-01-14 15:34:18.224] [I] Return code: 0
```

# Use Case

In this section, we will look at a use case for PowerShell as well as the alternative method for vRO (and explain how to go implementing).

# Active Directory User Accounts

Working on virtualization automation projects regularly requires interaction with Microsoft Active Directory (AD). Whether it's manipulating AD with vCenter permissions, creating AD computer accounts for newly deployed VMs, or creating AD user accounts for new employees within an organization, it's a common integration point. vRO ships with an Active Directory plug-in that will meet many of your requirements. However, as of writing, there are a few restrictions with the plug-in. vRO PowerShell integration may be required to fill in some gaps. Specifically, these restrictions with the AD:

+   * To be able to carry out some AD tasks, as creating an AD Enabled User account, the connection between vRO and AD must use SSL.
* Only a single AD domain is supported.
* Only a single domain controller within the domain is supported. If the domain controller is unavailable for any reason, any workflows it will fail.

![](bbox=[0.236, 0.715, 0.283, 0.755])

> Version 2 of the AD plug-in is expected to remove the restrictions on the AD domain and single domain controller. However, this example is primarily here to illustrate how PowerShell can be used to fill a potential gap in any plug-in.

The Microsoft Active Directory PowerShell module is not affected by any of those restrictions. Consequently, it can be used in combination with the vRO PowerShell alternative method to meet scenarios affected by the restrictions, without needing