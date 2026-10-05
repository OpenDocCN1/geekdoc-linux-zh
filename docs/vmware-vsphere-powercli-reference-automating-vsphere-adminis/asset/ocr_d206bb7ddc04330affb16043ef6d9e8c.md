# UNDERSTAND SOME BASIC CONCEPTS

[System.Reflection.Assembly] :: LoadWithPartialName($SMO) |
Out-Null

$SMOSrv = 'Microsoft.SqlServer.Management.Smo.Server'
sqlSrv = New-Object ($SMOSrv) $sqlServer

```
$sqlSrv.JobServer.Jobs |
Where-Object {$_.Category -eq 'Stats Rollup'} | Foreach-Object {
  $Object = [ordered]@{
    Name = $_.Name
    Description = $_.Description
    LastRun = $_.LastRunDate
    NextRun = $_.NextRun
    LastRunResult = $_.LastRunOutcome
    'Schedule (s)' = $_.Schedules | Foreach-Object {$.Name}
  }
  New-Object PSObject -Property $Object
}
```

> **NOTE** The get-AggregationJob function assumes that your Windows account has the necessary requirements to open and query the vCenter Server database and that the SQL Management Studio is installed on the machine where you execute the function, or at least the SQL Management Objects assemblies, which can be installed separately if the full Studio install is not desired.

The function produces an output listing similar to this:

```
Get-AggregationJob -SqlServer vcenter6
```

+   Name : Past Day stats rollupVC6DB
Description : This job is to roll up 5 min stats and should run every 30 mins
LastRun : 6/21/2015 1:30:00 AM
NextRun : 6/21/2015 2:00:00 AM
LastRunResult : Succeeded
Schedule(s) : 30 min schedule