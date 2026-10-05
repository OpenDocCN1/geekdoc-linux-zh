# VFLASH CACHE 179

```
ParameterName="EnableVfrc"
```

```
]
```

```
[ValidateSet("strong", "weak")]
```

```
[string]$CCacheType
```

```
,
```

```
parameter(
```

```
Mandatory=$false,
```

```
ParameterName="EnableVfrc"
```

```
]
```

```
[ValidateSet(4,8,16,32,64,128,256,512,1024)]
```

```
[Int]$BlocksizeKB
```

```
,
```

```
parameter(
```

```
Mandatory=$false,
```

```
ParameterName="EnableVfrc"
```

```
]
```

```
[ValidateRange(4, 409600)]
```

```
[Int]$ReservationMB
```

```
}
```

```
process {
```

```
# get the owning VM's view
```

```
$parentVm = Get-Vm -Id $disk.Parentid
```

```
if ($parentVm.Version -ne "v10") {
```

```
Write-Warning "VM must be version 10"
```

```
} else {
```

```
$parentVm = $parentVm | Get-View -Property Name
```

```
# set the default values for the vFRC
```

```
$VflashConfig = New-Object
```

```
VMware.Vim.VirtualDiskVFlashCacheConfigInfo
```

```
# If we are disabling, set the reservation to 0
```

```
if ($Disable) {
```

![](bbox=[0.903, 0.118, 0.966, 0.262])