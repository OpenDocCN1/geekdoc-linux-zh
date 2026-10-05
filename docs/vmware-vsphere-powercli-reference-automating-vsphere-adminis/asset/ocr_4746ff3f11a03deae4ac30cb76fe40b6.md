# Better Error Handling after Asynchronous Tasks

The ability of your scripts to intercept errors and produce meaningful error messages will improve their user friendliness. The following code snippet, which you can insert immediately after a wait loop, will check a call to an asynchronous method completed successfully. If the call to the method failed, the script displays an error message and then exits.

```
if($task.Info.State -eq "error") {
  $task.UpdateViewData("Info.Error")
  $task.Info.Error.Fault.faultMessage | % {
    $_Message
  }
  exit
}
```

# Finding Service Managers with Get-View Shortcuts

As mentioned earlier, the Get-View cmdlet has shortcuts for several of the service managers that you would normally access via the ServiceInstance object. But how can you find out which shortcuts are recognized by Get-View? The following short function returns a list of the shortcuts you can use with Get-View:

```
function Get-GVShortcut {
  Write-Verbose -Verbose "Shortcuts supported by Get-View"
  $si = Get-View ServiceInstance
  $si.content | Get-Member -MemberType Property | Foreach-Object {
    if($_.Name -match "Manager") {
      $t = Get-View $_.Name -ErrorAction SilentlyContinue
      if($t -ne $null) {
        Write-Output $_.Name
      }
    }
  }
}
```