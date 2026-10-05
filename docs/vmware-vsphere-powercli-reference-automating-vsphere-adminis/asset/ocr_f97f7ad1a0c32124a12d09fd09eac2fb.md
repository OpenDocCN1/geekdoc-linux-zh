# LISTING 19.5 Bulk import of vApp networks from CSV

```
function Add-CivAppNetwork {
#
.SYNOPSIS
Bulk-import vAppNetworks from CSV
.DESCRIPTION
This function will allow you to bulk-import vAppNetworks from CSV
.NOTES
Headers Used in CSV: vApp, ParentOrgNetwork, NetType, Name, Description,
DNSSSuffix, Gateway, Netmask, PrimaryDNS, SecondaryDNS, StaticIPPool
Source: Automating vSphere Administration
ARAMETER CSV
Parameter used by the function to locate the import file
.EXAMPLE
  Add-CivAppNetwork -CSV c:\temp\vAppNetworks.csv
}

param(
    [Mandatory=$True,NotNullOrEmpty()]
    [String]$CSV
)

process{
    $Source = Import-Csv -Path "$CSV"
    foreach ($line in $Source) {
        $shashParamForCivAppNetwork = @{
            vApp = $line.vApp
            Routed = $true
            Name = $line.Name
            Description = $line.Description
            DnsSSuffix = $line.DnsSSuffix
            Gateway = $line.Gateway
            Netmask = $line.Netmask
            PrimaryDNS = $line.PrimaryDNS
            SecondaryDNS = $line.SecondaryDNS
            StaticIPPool = $line.StaticIPPool
        }
    }
}
```