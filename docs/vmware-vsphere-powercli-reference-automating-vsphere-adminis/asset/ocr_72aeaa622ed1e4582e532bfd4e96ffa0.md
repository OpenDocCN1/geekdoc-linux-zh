# CHAPTER 4 • AUTOMATING STORAGE

Where {$_.Name -eq 'Disk group' \
(0200000006000c29ca92f335c2481dc6ca83577a56692724756)} \
New-VsanDiskGroup-VSANDiskGroup-VSANDiskGroup-CanonicalName \
naa.6000293bb4ca806b04e8169e61420

Conversely, in Listing 4.27 we remove a disk from an existing disk group. Note that this time we can recover the canonical name using the Get-VsanDisk cmdlet. Also Note that we need to identify the correct disk group to remove the disk from its (not particularly named)

# LISTING 4.27 Removing a disk from an existing VSAN disk group

```
$VSANDiskGroup = Get-VsanDiskGroup -VMHost vsanesxi01* | \
Where {$_.Name -eq 'Disk group' \
(0200000006000c29ca92f335c2481dc6ca83577a56692724756)} \
$VSANDiskGroup | Get-VsanDiskGroup | Format-Table CanonicalName \
$VSANDiskGroup | Get-VsanDisk -CanonicalName \
naa.60002937b02be32b670035b8a435d74e66 \
Remove-VsanDisk -Confirm:$false
```

In 4.28 we create a new VSAN disk group containing one SSD and one HDD. As usual, we will need the canonical name of both.

# LISTING 4.28 Creating a VSAN disk group

```
Get-VMHost vsanesxi01* | Get-ScsiLun -LuneType \
Format-Table CanonicalName \
$VSANDiskGroup = New-VsanDiskGroup -VMHost vsanesxi01* \
-SsdCanonicalName naa.6000296622408072f5516467bfdfd16330 \
-DataDiskCanonicalName naa.600029c21f3e7a3428ef55c4bfe4081
```

![](bbox=[0.243, 0.676, 0.293, 0.715])

> NOTE The minimum requirement for a VSAN disk group is one SSD and one HDD.

In 4.29, we remove a VSAN disk group, which will also remove disks within the group.

# LISTING 4.29 Removing a VSAN disk group

```
Get-VsanDiskGroup -VMHost vsanesxi01* | \
Where {$_.Name -eq 'Disk group' \
(0200000006000c296622408072f516467bfdfd1630566927247561)} \
Remove-VsanDiskGroup -Confirm:$false
```