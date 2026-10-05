```
$incompatible = $false
```

```
$nodeMaxEvcMode.GetEnumerator() | Foreach-Object {
$currentManufacturer = ($_.Value.split "-") [0]
if ($lastManufacturer -eq "") {
$lastManufacturer = $currentManufacturer
}
```

```
if ($lastManufacturer -ne $currentManufacturer) {
Write-Warning "Hosts have Intel and AMD CPUs"
incompatible = $true
}
```

```
# check to see if they are all the same
[Array]$evcGroups = $nodeMaxEvcMode.GetEnumerator() |
Group-Object -Property Value
```

```
if ($evcGroups.Count -eq 1) {
# they're the same, print out the first one
$obj = " | Select-Object MaxEvcMode
$obj.MaxEvcMode = $evcGroups[0].Name
$obj}
```

```
elseif ($incompatible -eq $false) {
# they're not the same, let's figure out the least
# common denominator
```

```
# collect all available EVC modes
$evcModes = @{
'intel' = @();
'amd' = @();
}
```

```
$serviceInstance = Get-View ServiceInstance
```

```
$serviceInstance.Capability.SupportedEVCMode | Foreach-Object {
$procManufacturer = ($_.key -split "-") [0]
```