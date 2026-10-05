# FIGURE 24.53 Reset to Commit

![](bbox=[0.238, 0.128, 0.874, 0.431])

Click OK to confirm the reset (Figure 24.54).

# FIGURE 24.54 Click OK in warning.

![](bbox=[0.415, 0.523, 0.715, 0.646])

You can verify that the `Test-Function01.ps1` file has reverted to the content you chose with a `Write-Host` line:

```
Get-Content C:\GitHub\Test01\Test-Function01.ps1
```

```
function Test-Function01 {
    Write-Host "This is test 01"
}
```

This locally made change needs to be committed to the repository to make it the definitive version (for now) for everyone else. Navigate to the File Status tab, see the view back to Pending Files ➤ Sorted By File Status, and verify that the `Test-Function01.ps1` file is in the Unstaged Files area (Figure 24.55).