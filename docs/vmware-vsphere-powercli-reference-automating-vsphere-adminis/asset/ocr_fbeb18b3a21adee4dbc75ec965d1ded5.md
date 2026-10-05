# CHAPTER 19 * VCLOUD DIRECTOR

```
$PvDCProperties["MemoryAllocatedGB"] = $PvDC.
MemoryAllocatedGB
$PvDCProperties["MemoryAllocatedPcnt"] = $if ($PvDC.
MemoryTotalGB -
gt 0) {($PvDC.MemoryAllocatedGB / $PvDC.MemoryTotalGB) *
100}
}
```

```
#CPU
if ($CPU) -or ($All)) {
$PvDCProperties["CPUUsedGhz"] = $PvDC.CpuUsedGhz
$PvDCProperties["CpuOverheadGhz"] = $PvDC.CpuOverheadGhz
$PvDCProperties["CpuTotalGhz"] = $PvDC.CpuTotalGhz
$PvDCProperties["CpuAllocatedGhz"] = $PvDC.CpuAllocatedGhz
$PvDCProperties["CpuAllocatedPcnt"] = ($PvDC.
CpuAllocatedGhz / 
$PvDC.CpuTotalGhz) * 100
}
```

```
$PvDC = New-Object -TypeName PSObject $PvDCProperties
```

```
}
#Set -NoClobber to not overwrite existing files
$PvDCs | Export-Csv "Path" -NoTypeInformation -NoClobber
```

```
#Verify if the file was created
if(!(Test-Path $Path)) {Write-Warning "It appears that the CSV
file was not created. Please try again.\} else {
{Write-Verbose "File Saved Successfully to '$Path'}
}
```

# Organization vDCs

Within your organization, you can split up the resource allocation and configurations using org vDCs. Org vDCs are partitioned from the resources of a provider vDC.