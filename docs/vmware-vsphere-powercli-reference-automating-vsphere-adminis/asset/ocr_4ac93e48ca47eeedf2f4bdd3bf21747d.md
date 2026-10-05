# CALLING VO WORKFLOWS FROM POWERSHELL

.PARAMETER Credential
PS Credential Object
EXAMPLE

```
$Credential = Get-Credential
Get-vWorkflowExecutionResult -ExecutionRef https://vRO01:8281/vco/
api/workflows/565b2c35-3607-4ab9-ace7-9102c139108/executions/
40288024ae8e2a641b045ea9290213 -Credential $Credential

#>
[CmdletBinding(OutputType={'System.Management.Automation.PSObject'}))
```

Param

```
(\parameter (Mandatory=$true, ValueFromPipeline=$true,
ValueFromPipelinebyPropertyName=$true)
[ValidateNullOrEmpty()] (Alias("Execution"))
[String]$ExecutionRef,

[parameter (Mandatory=$true)
[ValidateNullOrEmpty()]
[PSCredential]$Credential
)
```

begin {

```
# --- Convert Credential Object to Username and Password

$Username = $Credential.UserName
$Password = $Credential.GetNetworkCredential().Password

# Deal with certificate issues
# -- Note: this code will disable certificate session
# for this PowerShell session
if (-not ("TrustAllCertsPolicy" -as [type])){
```

Add-Type "@"