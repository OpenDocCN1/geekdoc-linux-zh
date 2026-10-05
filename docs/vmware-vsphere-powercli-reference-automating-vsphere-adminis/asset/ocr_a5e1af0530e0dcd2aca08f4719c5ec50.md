```
[switch]$Storage,

# Set All in different ParameterName to not be used with Resources
[Parameter(ParameterSetName = 'All')]
[switch]$All = $true
)
```

```
process {

# Create empty array
$PVDCs = @()
foreach ($pVDC in (Get-ProviderVdc)) {

# Default pVDC information
$pVDCProperties = @{
    Name = $pVDC.Name
    Description = $pVDC.Description
    Enabled = $pVDC.Enabled
    Status = $pVDC.Status
}
```

```
#Storage
if (($Storage) -or ($All)) {
    $pVDCProperties["StorageUsedGB"] = $pVDC.StorageUsedGB
    $hshPropertiesForNewObject["StorageOverheadGB"] = $pVDC.StorageOverhead
    $pVDCProperties["StorageTotalGB"] = $pVDC.StorageTotalGB
    $pVDCProperties["StorageUsedPct"] = $(if ($pVDC.StorageTotalGB -gt 0) {($pVDC.StorageUsedGB / $pVDC.StorageTotalGB) * 100})
```

```
#Memory
if (($Memory) -or ($All)) {
    $pVDCProperties["MemoryUsedGB"] = $pVDC.MemoryUsedGB
    $pVDCProperties["MemoryOverheadGB"] = $pVDC.MemoryOverheadGB
    $pVDCProperties["MemoryTotalGB"] = $pVDC.MemoryTotalGB
```