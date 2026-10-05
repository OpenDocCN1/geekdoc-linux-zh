automate the same tasks performed in the GUI in the earlier sections "Create a Repository" and "Create a Project Structure."

> NOTE Just like the WMI Explorer tool, the WMI-based functions should also be run on the VisualSVN Server.

# LISTING 24.1 New-VisualSVNRepository

```
function New-VisualSVNRepository (
<#n.SYNOPSIS
Create a new Repository in VisualSVN
.DESCRIPTION
Create a new Repository in VisualSVN
.PARAMETER Name
Repository Name
.PARAMETER Project
Project Name
.PARAMETER CreateFolders
Create the standard folder structure: branches, tags, trunk
.INPUTS
System.String.
.OUTPUTS
None.
.EXAMPLE
New-VisualSVNRepository -Name Repository01 -Project Project01
-CreateFolders
#>
[CmdletBinding()]
Param (
[parameter (Mandatory=$true)]
[ValidateNotNullOrEmpty()]
[String]$Name,
[parameter (Mandatory=$false)]
[ValidateNotNullOrEmpty()]
[String]$Project,
```