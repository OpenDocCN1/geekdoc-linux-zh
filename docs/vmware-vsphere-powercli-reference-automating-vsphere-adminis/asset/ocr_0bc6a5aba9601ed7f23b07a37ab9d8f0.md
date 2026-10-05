```
$false, $VMKernel
```

Write-Verbose "Successfully set iSCSI Binding for $ESXXiHost"

```
$ISCIBindingOutput = $ESXCLI.isci.networkportal.list() | \
Where-Object { $_.Adapter -eq $ISCIHBA.Device -and \
$_.vmknic -eq $VMKernel}
}
catch [Exception] {
```

```
$ErrorText = "Unable to set SCSI Binding for $ESXiHost"
throw
}
# --- Rescan HBA and VMFS if requested
try {
```

```
if ($PSBoundParameters.ContainsKey('Rescan')) {

Write-Verbose "Rescanning HBAs and VMFS for $ESXiHost" $ESXiHost | \
Get-VMHostStorage -RescanAllHba -RescanVmfs \nn-ErrorAction Stop | Out-Null
}
catch [Exception] {
```

```
$ErrorText = "Unable to rescan HBA and VMFS for $ESXiHost"
throw
}

# --- Output the Successful Result
Write-Output $ISCIBindingOutput
}
catch [Exception] {
```