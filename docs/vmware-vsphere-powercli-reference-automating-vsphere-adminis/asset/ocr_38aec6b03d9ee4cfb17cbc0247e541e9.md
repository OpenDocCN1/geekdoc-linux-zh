# CHAPTER 22 * SITE RECOVERY MANAGER

}

}

```
if ($plan.GetInfo().State -eq $expectedState) {
    Write-Host "Starting operation..." -NoNewline
    $plan.Start($mode);

    # wait for the operation to finish/fail
    $start = Get-Date
    while ((New-TimeSpan $start).TotalMinutes -le $WaitMinutes) {
        if ($plan.GetInfo().State -ne "Running") {
            break
        }

        Write-Host "." -NoNewline
        Start-Sleep -Seconds 5
    }

Write-Host "DONE!"
```

# get result

$planHistory = $srmApi.Recovery.GetHistory($plan.MoRef)

$planHistory.GetRecoveryResult(1) [0]

} else {

Write-Warning "SRM plan is not in expected state."

}

}

When used to test a plan, followed by cleanup, the output will look like the following:

```
# begin plan test
Invoke-SrmPlanAction -RecoveryPlan $planName -Test
Executing test................................DONE!
```