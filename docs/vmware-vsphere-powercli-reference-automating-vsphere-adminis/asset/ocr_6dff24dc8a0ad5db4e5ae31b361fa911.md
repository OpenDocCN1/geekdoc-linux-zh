# 162  CHAPTER 4 • AUTOMATING STORAGE

```
while ((($Task.State -ne 'Success') -and \
($Task.State -ne 'Error'))
{
```

```
Write-Verbose "Wating for VSAN Maintenance Mode \
task to complete ($($Task.PercentComplete)% done)"
Start-Sleep -Seconds $PollSeconds
```

```

$Task = Get-Task -Id $MaintenanceModeTask
```

```

}
if ($Task.State -eq 'Success') {
```

```
Write-Verbose "VSAN Maintenance Mode task for ESXiHost \
succeeded! The timespan for the operation: \
''(New-TimeSpan -Start $Task.StartTime -End $Task.FinishTime)'
```

```
Get-VMHost $ESXiHost | Select-Object Name,ConnectionState
```

```

if ($Task.State -eq 'Error') {
```

```
Write-Warning "VSAN Maintenance Mode \
task for $ESXiHost failed"
```

```

}
}
catch [Exception] {
```

```
$ErrorText = "VSAN Maintenance Mode task for \
$ESXiHost failed"
throw
```

```

}
catch [Exception] {
```

```
if ($ErrorText) {
throw "Unable to set VMHost $($ESXiHost) to VSAN \
Maintenance Mode. Error is: $($ErrorText)""
```