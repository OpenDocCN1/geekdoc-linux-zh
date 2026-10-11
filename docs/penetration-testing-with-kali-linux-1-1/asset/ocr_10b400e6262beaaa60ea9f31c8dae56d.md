> While Microsoft has not documented a list of searchable SPN's there are extensive lists available online.<sup>637</sup>

For example, let’s update our PowerShell enumeration script to filter the `serviceprincipalname` property for the string `*http*`, indicating the presence of a registered web server.

```
$domainObj = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()

$PDC = $($domainObj.PdcRoleOwner).Name

$SearchString = "LDAP://"
$SearchString += $PDC + "/"

$DistinguishedName = "DC=$($domainObj.Name.Replace('.', ', ' ), DC=')'"
$SearchString += $DistinguishedName

$Searcher = New-Object System.DirectoryServices.DirectorySearcher ( [ADSI]$SearchString)
$objDomain = New-Object System.DirectoryServices.DirectoryEntry

$Searcher.SearchRoot = $objDomain

$Searcher.filter="serviceprincipalName=*http*"

$Result = $Searcher.FindAll()

Foreach($obj in $Result)
{
    Foreach($prop in $obj.Properties)
    {
        $prop
    }
}
```

*Listing 686 - PowerShell script to detect registered service principal names*

This search returns a number of results, and although they could be further filtered, we can easily spot relevant information:

| Name | Value |
| ----- | ----- |
| givenname | {iis_service} |
| samaccountname | {iis_service} |
| cn | {iis_service} |
| pwdlastset | {131623309820953450} |
| whencreated | {05/02/2018 19.03.02} |
| badpwdcount | {0} |
| displayname | {iis_service} |

<sup>637</sup> (Sean Metcalf, 2017), http://adsecurity.org/?page_id=183