# LISTING 21.11 vRO JavaScript code for New-DRRule Set Alignments task

```
var arguments = "-Name " + drsRuleName + "-Cluster " + cluster +
+ "-VM "n  + vms + "-vCenter " + vCenter + "-Username " + username +
  + "-Password " + password;

if (keepTogether) {
  arguments += " --KeepTogether"
}
```

Within the workflow schema, the previously created Invoke-ExternalPSScriptReturnCode workflow (Figure 26).

# FIGURE 21.26 Adding the Invoke-ExternalPSScriptReturnCode workflow

![](bbox=[0.273, 0.396, 0.903, 0.584])

In In tab of the Invoke-ExternalPSScriptReturnCode workflow, create the following- (Figure 21.27):

powershellHost Type: PowerShell:PowerShellHost, as workflow attribute. Set the value to be the PowerShellHost created as part of the PowerShell plug-in setup.

scriptPath Type: String, as workflow attribute. Set the value to c:\Scripts\New-ClusterDRSRule.ps1.

and select the following existing attribute (Figure 21.27):

arguments Type: String