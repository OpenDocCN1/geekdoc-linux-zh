

# 从 POWERSHELL 773 调用 VRO 工作流

vRO ItemHref

.PARAMETER ParameterName
为工作流提供单个参数

.PARAMETER ParameterValue
提供单个参数的值

.PARAMETER ParameterType
提供单个参数的类型

.PARAMETER ParameterXML
通过 XML 提供工作流参数

.PARAMETER NoParameters
当使用 ItemHref 且未提供任何参数时需要

.PARAMETER Credential
PS Credential 对象

示例

```
$Credential = Get-Credential
Invoke-vROWorkflow -Server vRO01 -ID c0278910-9ae2-46c5-bb45-2292fe88e3ab -Credential $Credential
```

示例

```
$Credential = Get-Credential
Invoke-vROWorkflow -ItemHref
https://vRO01.sunnydale.local:8281/api/workflows/c0278910-9ae2-46c5-bb45-2292fe88e3ab/ -NoParameters -Credential $Credential
```

示例

```
Invoke-vROWorkflow -Server vRO01 -ID c0278910-9ae2-46c5-bb45-2292fe88e3ab -ParameterName 'Apple' -ParameterType 'String' -Credential $Credential
```

示例

```
$ParameterXML =
'<execution-context xmlns="http://www.vmware.com/vco">
<parameters>
  <parameter type="string" name="text" scope="local">
  <string>Apple</string>
  </parameter>
```

![](img/62596f5acc979040608a4e5111beb7d6_804_0.png)

# 第 21 章 • VREALIZE ORCHESTRATOR

```
<parameter type="number" name="a" scope="local">
<number>7</number>
</parameter>
</parameters>
```

```
<execution-context>
Invoke-vROWorkflow -Server vRO01 -ID $ParameterXML $ParameterXML -Credential $Credential
.EXAMPLE
Get-vROWorkflow -Name 'Test-Workflow' -Server vRO01.sunnaily.local -Credential $Credential | Select Server,ID | Invoke-vROWorkflow -ParameterName a -ParameterValue 'Nature' -ParameterType String -Credential $Credential
.EXAMPLE
Get-vROWorkflow -Name 'Test-Workflow' -Server vRO01.sunnaily.local -Credential $Credential | Select ItemHref | Invoke-vROWorkflow -ParameterName a -ParameterValue 'Junior' -ParameterType String -Credential $Credential
```

```cs
#
[CmdletBinding(DefaultSetName="A")]
[OutputType([('System.Management.Automation.PSObject')]
```

```cs
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

# 从 POWERSHELL 调用 VRO 工作流

```
[parameter (Mandatory=$true, ValueFromPipelinePropertyName=$true, 
ParameterSetName="C")
[parameter (ValueFromPipelinePropertyName=$true, ParameterSetName="D")
[parameter (ParameterSetName="E")]
ValidateNotNullOrEmpty())
[String] $ItemHref,
```

```
[parameter (Mandatory=$false, ParameterSetName="A")
[parameter (ParameterSetName="C")
ValidateNotNullOrEmpty())
[String] $ParameterName,
```

```
[parameter (Mandatory=$false, ParameterSetName="A")
[parameter (ParameterSetName="C")
[String] $ParameterValue,
```

```
[parameter (Mandatory=$false, ParameterSetName="A")
[parameter (ParameterSetName="C")
ValidateNotNullOrEmpty())
[String] $ParameterType,
```

```
[parameter (Mandatory=$false, ParameterSetName="B")
[parameter (ParameterSetName="D")
ValidateNotNullOrEmpty())
[String] $ParameterXML,
```

```
[parameter (Mandatory=$false, ParameterSetName="E")
ValidateNotNullOrEmpty())
[Switch] $NoParameters,
```

```cs
[parameter (Mandatory=$true)
ValidateNotNullOrEmpty())
[PSCredential] $Credential
}
```

```cs
# -- 将凭据对象转换为用户名和密码

$Username = $Credential.Username
$Password = $Credential.GetNetworkCredential().Password

# -- 处理证书问题
# 注意：此代码将禁用证书检查
# -- 对于此 PowerShell 会话
if (-not ("TrustAllCertsPolicy" -as [type])) {
```

```cs
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

```cs
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

```cs
# -- 创建 REST Header
$Auth = $Username + ':' + $Password
$Encoded = [System.Text.Encoding]::UTF8.GetBytes($Auth)
$EncodedPassword = [System.Convert]::ToBase64String($Encoded)
$Headers = @("Authorization="Basic $($EncodedPassword)");
```

```cs
if ($PSBoundParameters.ContainsKey('ParameterType')) {

$ParameterType = $ParameterType.ToLower()
$Body = @"
<execution-context xmlns="http://www.vmware.com/vco">
  <parameters>
    <parameter type="$(ParameterType)" name="$(ParameterName)" scope="local">
      <$(ParameterType)>$(ParameterValue)</$(ParameterType)>
    </parameter>
  </parameters>
</execution-context>
"@
}

if ($PSBoundParameters.ContainsKey('ParameterXML')) {
  $Body = $ParameterXML
} else {
  $Body = @"
<execution-context xmlns="http://www.vmware.com/vco">
  <parameters>
    <parameter type="string" name="$(ParameterName)" scope="local">
      <string>$(ParameterValue)</string>
    </parameter>
  </parameters>
</execution-context>
"@
}

if ($PSBoundParameters.ContainsKey('ItemHref')) {
  $URL = $ItemHref
} else {
  $URL = "https://$Server/$(ID)"
}

$InvokeRequest = Invoke-WebRequest -Method Post -Uri $URL -Headers $Headers -ContentType "application/xml" -Body $Body

$Object = @{
    StatusCode = $InvokeRequest.StatusCode
    StatusDescription = $InvokeRequest.StatusDescription
    Execution = $InvokeRequest.Headers.Location
}
return $Object
```

# 第 21 章 • VREALIZE ORCHESTRATOR

# 查询工作流状态

工作流调用后，可能需要一些时间完成。列表 21.20 中的 Get-vROState 函数通过提交执行状态（来自列表 21.19 的输出）加上 state 单词来获取以下 URL。该 URL 可作为 Get-vROState 函数的 ExecutionState 参数的值。

```
https://vro01:281/vco/api/workflows/c0278910-9ae2-46c5-bb45-2292fe88e3ab/executions/402880244ae8e2a6014b0961089a234/state
```

- **21.20** Get-vROState

```powershell
function Get-vROState {
#SYNOPSIS
 获取工作流状态
.DESCRIPTION
 获取工作流状态
.PARAMETER ExecutionStateRef
 工作流执行引用
.PARAMETER Credential
 PS Credential 对象
.EXAMPLE
 $Credential = Get-Credential
 Get-vROState -ExecutionStateRef \
https://vRO001:8281/vco/api/workflows/\
656b2c35-3607-4ab9-7-9102c139108/executions/\
402880244ae8e2a6014b045ea90213 -Credential $Credential
}
```

输出如下：

```
StatusCode : 202
StatusDescription : Accepted
Execution : https://vro01.sunnydale.local:8281/vco/api/workflows/c0278910-9ae2-46c5-bb45-2292fe88e3ab/executions/402880244ae8e2a6014b0961089a234/
```

