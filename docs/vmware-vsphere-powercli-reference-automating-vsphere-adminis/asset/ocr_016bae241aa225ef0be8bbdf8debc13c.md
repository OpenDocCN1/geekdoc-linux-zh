DN of the Organization Unit to create the User in
.PARAMETER ADUsername

Username to connect to Active Directory with
.PARAMETER ADPassword

Password to connect to Active Directory with
.INPUTS

String
.OUTPUTS

None.
.EXAMPLE

```
/.New-ActiveDirectoryUser.ps1 -FirstName 'Joe'
-Surname 'Bloggs' -OU 'Users,OU=HQ,DC=sunnydale,DC=local'
-ADUsername 'sunnydale\vcosvc' -ADPassword P@sswordrd1'
#
```

```
[CmdletBinding() ]
```

```
Param
([parameter (Mandatory=$true)]n[ValidateNotNullOrEmpty()]
[String] $FirstName,
```

```
[parameter (Mandatory=$true)]n[ValidateNotNullOrEmpty()]
[String] $Surn,
```

```
[parameter (Mandatory=$true)]n[ValidateNotNullOrEmpty()]
[String] $OU,
```

```
[parameter (Mandatory=$true)]n[ValidateNotNullOrEmpty()]
[String] $ADUsername,
```

```
[parameter (Mandatory=$true)]n[ValidateNotNullOrEmpty()]
[String] $ADPassword
)
```