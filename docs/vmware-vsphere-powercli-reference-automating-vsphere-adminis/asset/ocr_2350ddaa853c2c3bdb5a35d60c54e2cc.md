# INFORMATION SOURCES

531

available event.

.PARAMETER Finish

The end of the time range in which to look for events.
If not specified, the function will use the current time
as the end of the time range.

.PARAMETER EventChainId

The function will only return events that have this specific
EventChainId.

.PARAMETER User

If specified will only return events for tasks triggered by
this user. If not specified the function will return events
independent of the user who started the task.

.EXAMPLE

Get-VIEventSDK -Entity (Get-Cluster -Name "MyCluster")

```
.EXAMPLE
Get-VM myVM | Get-VIEventSDK -EventChainId $task.

Param(
[Mandatory=$true,ValueFromPipeline = $true)
$Entity,
[switch]$EntityChildren = $false,
[DateTime]$Start,
[DateTime]$finish,
[Int]$EventChainId,
[String]$User
)
```

![](bbox=[0.903, 0.433, 0.922, 0.555])

PART IV

```
Begin{
$Si = Get-View ServiceInstance
$eventMgr = Get-View $si.Content.EventManager
$eventNumber = 100
}
```

```
Process{
$Entity | ForEach-Object -Process {
$eventFilter = New-Object VMware.Vim.EventFilterSpec

if($Entity){
```