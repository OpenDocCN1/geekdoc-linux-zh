
# 第 21 章 • VREALIZE ORCHESTRATOR

# 从 POWERSHELL 调用 VRO 工作流

```powershell
$Credential = Get-Credential
```

```powershell
Invoke-vROWorkflow -Server vRO01 -ID c0278910-9ae2-46c5-bb45-2292fe88e3ab -Credential $Credential
```

示例

```powershell
$Credential = Get-Credential
Invoke-vROWorkflow -ItemHref https://vRO01.sunnydale.local:8281/api/workflows/c0278910-9ae2-46c5-bb45-2292fe88e3ab/ -NoParameters -Credential $Credential
```

示例

```powershell
Invoke-vROWorkflow -Server vRO01 -ID c0278910-9ae2-46c5-bb45-2292fe88e3ab -ParameterName 'Apple' -ParameterType 'String' -Credential $Credential
```

示例

```xml
$ParameterXML =
'<execution-context xmlns="http://www.vmware.com/vco">
<parameters>
  <parameter type="string" name="text" scope="local">
  <string>Apple</string>
  </parameter>
```

![](img/62596f5acc979040608a4e5111beb7d6_804_0.png)

```xml
<parameter type="number" name="a" scope="local">
<number>7</number>
</parameter>
</parameters>
```

```powershell
<execution-context>
Invoke-vROWorkflow -Server vRO01 -ID $ParameterXML $ParameterXML -Credential $Credential
```

.EXAMPLE

```powershell
Get-vROWorkflow -Name 'Test-Workflow' -Server vRO01.sunnaily.local -Credential $Credential | Select Server,ID | Invoke-vROWorkflow -ParameterName a -ParameterValue 'Nature' -ParameterType String -Credential $Credential
```

.EXAMPLE

```powershell
Get-vROWorkflow -Name 'Test-Workflow' -Server vRO01.sunnaily.local -Credential $Credential | Select ItemHref | Invoke-vROWorkflow -ParameterName a -ParameterValue 'Junior' -ParameterType String -Credential $Credential
```

```powershell
#
[CmdletBinding(DefaultSetName="A")]
[OutputType([('System.Management.Automation.PSObject')]

Param
(
[parameter(Mandatory=$true, ValueFromPipeline=$true,
ValueFromPipelinePropertyName=$true, ParameterSetName="A")]
[parameter(ParameterSetName="B")]
[ValidateNotNullOrEmpty()]
[String]$Server,
[parameter(Mandatory=$true, ValueFromPipelinePropertyName=$true,
ParameterSetName="A")]
[parameter(ParameterSetName="B")]
[ValidateNotNullOrEmpty()]
[String]$ID,
```

```powershell
[parameter (Mandatory=$true, ValueFromPipelinePropertyName=$true, 
ParameterSetName="C")
[parameter (ValueFromPipelinePropertyName=$true, ParameterSetName="D")
[parameter (ParameterSetName="E")]
ValidateNotNullOrEmpty())
[String] $ItemHref,
```

```powershell
[parameter (Mandatory=$false, ParameterSetName="A")
[parameter (ParameterSetName="C")
ValidateNotNullOrEmpty())
[String] $ParameterName,
```

```powershell
[parameter (Mandatory=$false, ParameterSetName="A")
[parameter (ParameterSetName="C")
[String] $ParameterValue,
```

```powershell
[parameter (Mandatory=$false, ParameterSetName="A")
[parameter (ParameterSetName="C")
ValidateNotNullOrEmpty())
[String] $ParameterType,
```

```powershell
[parameter (Mandatory=$false, ParameterSetName="B")
[parameter (ParameterSetName="D")
ValidateNotNullOrEmpty())
[String] $ParameterXML,
```

```powershell
[parameter (Mandatory=$false, ParameterSetName="E")
ValidateNotNullOrEmpty())
[Switch] $NoParameters,
```

```powershell
[parameter (Mandatory=$true)
ValidateNotNullOrEmpty())
[PSCredential] $Credential
}
```

```powershell
# -- 将凭据对象转换为用户名和密码
$Username = $Credential.Username
$Password = $Credential.GetNetworkCredential().Password
# -- 处理证书问题
# 注意：此代码将禁用证书检查
# -- 对于此 PowerShell 会话
if (-not ("TrustAllCertsPolicy" -as [type])) {
```

```powershell
Add-Type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckCertificatePoint(ServicePoint srvPoint, X509Certificate certificate, WebRequest request, int certificateProblem) {
        return true;
    }
}
"@
```

```powershell
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

```powershell
# -- 创建 REST Header
$Auth = $Username + ':' + $Password
$Encoded = [System.Text.Encoding]::UTF8.GetBytes($Auth)
$EncodedPassword = [System.Convert]::ToBase64String($Encoded)
$Headers = @("Authorization="Basic $($EncodedPassword)");
```

```powershell
if ($PSBoundParameters.ContainsKey('ParameterType')) {
```
