# IMPORT VCENTER SERVER INVENTORY ITEMS 431

```
{ Write-Host "$_ on $($row.Host) added Successfully" `
-ForegroundColor Green else { Write-Host "It Appears `
that $($) on $($row.Host) was not added successfully to `
($($).Switch" -ForegroundColor Red }
```

# Tags

Tags and tag categories can be imported into vCenter Server at any time. However, you will want to make sure all of your virtual objects are populated in vCenter before you try to re-create the tag relationships; otherwise you will receive errors. The tags will not be able to find their associated objects. Listing 12.11 contains a function that will help you import the tags and tag categories that you exported earlier in this chapter.

![](bbox=[0.903, 0.343, 0.952, 0.433])

# LISTING 12.11 Importing tags and tag categories

```
function Import-Tag {
#
.SYNOPSIS
Import Tags and Tag Categories
.DESCRIPTION
This function exports Tags and Tag Categories from vCenter
.NOTES
Source: Automating vSphere Administration
.PARAMETER Path
Mandatory parameter used by the function to determine
the source of the Tags file.
.EXAMPLE
Import-Tag -Path C:\Temp\TagData.xml
#
[CmdletBinding()]
Param (
[Parameter(Mandatory = $True, Position = 1)]
[string]$Path
```

# PART III