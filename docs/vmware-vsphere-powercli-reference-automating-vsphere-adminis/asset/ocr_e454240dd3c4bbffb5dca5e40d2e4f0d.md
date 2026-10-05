# EXPLORING THE SRM CMDLETS

# 807

```
[int]$WaitMinutes = 5

process {
  if ($global:DefaultSrmServers.length -lt 1) {
    throw "Not connected to SRM server"
  }

  $srmApi = $global:DefaultSrmServers[0].ExtensionData

  # get the recovery plan from the API
$plan = $srmApi.Recovery.ListPlans() | Where-Object {
    $_.GetInfo().Name -eq $RecoveryPlan
  }

$expectedState = ""
$mode = 0
witch ($true) {
  $Test {
    $expectedState = "Protecting"
    $mode = 1
  }

  $Cleanup {
    $expectedState = "NeedsCleanup"
    $mode = 2
  }

  $Failover {
    $expectedState = "Protecting"
    $mode = 0
  }
}

$Reprotect {
  $expectedState = "FailedOver"
  $mode = 3
}
```