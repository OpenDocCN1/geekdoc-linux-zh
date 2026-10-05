Get-VDSwitch myVDSwitch0, myVDSwitch1 |
Assert-HardeningGuideVNetworkHealthChk -Remediate:$true

Disable any enabled health check setting on vDSitches, as the hardening
gu recommends

.Outputs
If remediating, the VMware.VimAutomation.Vds.Impl.V1.VmwareVDSwitchImpl
object for each VDSwitch updated. If just reporting, the
Selected.Vmware.Vim.VmwareVDSwitchV1MinutHealthCheckConfig and
Selected.Vmware.Vim.VmwareDVSteamingHealthCheckConfig object for each
VDSwitch involved

```
#
[CmdletBinding(SupportsShouldProcess=$true)]
```

Param(

+   ## Virtual distributed switch to assess/remediate. If none specified, will
# only report
# act on all VDSitches in the VIServer to which current session is
# connected
[parameter(ValueFromPipeline=$true)] [PSObject[]]$VDSwitch,
## Switch: Remediate the entity? Default is $false, which causes changes to

```
[switch]$Remediate = $false
)
```

```
begin
## the desired value for the HealthCheckConfig properties
$DesiredConfigValue = $false
}
```

```
process
$ArrVDSwitchOfInterest = if ($PsBoundParameters.ContainsKey("*VDSwitch")) {
if ($VDSwitch.GetType().Name -eq "VmwareVDSwitchImpl") {$VDSwitch}
else {Get-VDSwitch -Name $VDSwitch}
} else {Get-VDSwitch}
```

![](bbox=[0.913, 0.345, 0.936, 0.435])

PART III