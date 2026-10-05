# CHAPTER 21

.DESCRIPTION

Get vRO Workflows

.PARAMETER All

Retrieve all workflows

.PARAMETER Category

Retrieve workflow by category

.PARAMETER Name

Retrieve workflow by name

.PARAMETER Wildcard

Perform a wildcard search when using the Name parameter

.PARAMETER Server

vRO Server to connect to

.PARAMETER Credential

PS Credential Object

.EXAMPLE

```
$Credential = Get-Credential
```

```
Get-vROWorkflow -All -Server vRO01 -Credential $Credential
```

.EXAMPLE

```
Get-vROWorkflow -Category -Name 'New-DRSRule' -Server vRO01 
-Credential $Credential
```

.EXAMPLE

```
Get-vROWorkflow -Name 'New' -Wildcard -Server vRO01 
-Credential

```

```
$Credential
```

```
#
[CmdletBinding(DefaultParameterName="All")
[OutputType('System.Management.Automation.PSObject')]]
```

```
Param
(
```

```
[parameter(Mandatory=$false, ParameterSet="All",
Position=0)]
```

```
[Switch]$All,
```

```
[parameter(Mandatory=$false, ParameterSet="Category",`
```