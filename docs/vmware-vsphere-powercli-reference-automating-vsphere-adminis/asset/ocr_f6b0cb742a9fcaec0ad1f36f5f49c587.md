# Adding a Target

```
Set-VMHostSnmp -TargetHost $sendTrapsHere \
-TargetCommunity $sendCommunity \
-AddTarget `\
-HostSnmp (Get-VMHostSnmp)
```

Advanced Options To optimize your infrastructure, you will eventually have to set an option or two—task easily performed via the Set-AdvancedSetting cmdlet. To enable vMotion, you run the following:

```
Get-AdvancedSetting -Entity (Get-VMHost vSphere02) \
-Name Migrate.Enabled | \
Set-AdvancedSetting -Value 1
```

You could configure a set of options all at once using a hash table to loop through the settings and apply the Set-AdvancedSetting cmdlet. For instance, to vSphere to NFS on a NetApp FS system, you run the:

```
@{
'NFS.MaxVolumes' = 256
'Net.TcpHeapMax' = 512
'Net.TcpHeapSize' = 32
'NFS.HeartbeatFrequency' = 12
'NFS.HeartbeatTimeout' = 5
'NFS.HeartbeatMaxFailures' = 10
'NFS.MaxQueueDepth' = 64
}.GetEnumerator() | ForEach-Object {
Get-AdvancedSetting -Entity (Get-VMHost vSphere02) \
-Name $_.Name \
Set-AdvancedSetting -Value $_.Value
}
```

Using the cmdlets we have highlighted, and the automation workflow in the chapter, you can create a zero-touch installation for any environment. Now that you have both a zero-touch vSphere installation via Kickstart and a fully automated host configuration script, it's time to glue these together and deliver on the promise of a fully automated host provisioning life cycle. To accomplish this, we adapted a technique originally documented by Lance Berc. The general workflow looks like this:

+   1. Kickstart your vSphere host, configuring at a minimum management network.