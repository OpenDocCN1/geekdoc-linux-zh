# CHAPTER 3

. EXAMPLE

Get-Datacenter Prod01 | Get-DistributedSwitchCandidate
-DistributedSwitch vDS01 -Recurse

```
#>
[CmdletBinding()]
Param(
    [Parameter(Mandatory=$true,
    ValueFromNotNullOrEmpty())
    [Vmware.VimAutomation.Sdk.Types.V1.VIOObject]
    $VIOject,

    [Parameter(Mandatory=$true,
    ValueFromPipeline=$true,
    ValueFromPipelinePropertyName=$true)]n    [ValidateNotNullOrEmpty()]
    [String]
    $DistributedSwitch,

    [Parameter()]
    [ValidateNotNullOrEmpty()]
    [Switch]
    $Recurse
)
begin{
    $dvSwitchManager =
    Get-View (Get-View ServiceInstance).content.dvSwitchManager
}
process{
    $vds = Get-View -ViewType "VmwareDistributedVirtualSwitch" \
    -Filter ('Name'=$DistributedSwitch')
    if (-$vds) {
        Write-Warning "$Name not found!"
        continue;
    }
    if ($Recurse) {$r = $True}else{$r = $False}
$Moref = $VIOject | Get-View |
```