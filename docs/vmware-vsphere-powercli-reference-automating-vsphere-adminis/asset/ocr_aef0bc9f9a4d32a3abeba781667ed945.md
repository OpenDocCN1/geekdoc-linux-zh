```
# -- Convert Credential Object to Username and Password

$Username = $Credential.Username
$Password = $Credential.GetNetworkCredential().

# -- Deal with certificate issues
# Note: this code will disable certificate checking
# -- for this PowerShell session
if (-not ("TrustAllCertsPolicy" -as [type])) {
```

```
# -- Deal with certificate issues
# Note: this code will disable certificate checking
# -- for this PowerShell session
if (-not ("TrustAllCertsPolicy" -as [type])) {
```

```
Add-Type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    ServicePoint srvPoint, X509Certificate certificate, WebRequest request, int certificateProblem) {
        return true;
    }
}\@
```

```
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

```
# -- Create REST Headers
$Auth = $Username + ':' + $Password
$Encoded = [System.Text.Encoding]::UTF8.GetBytes($Auth)
$EncodedPassword = [System.Convert]::ToBase64String($Encoded)
$Headers = @("Authorization="Basic \($EncodedPassword)");
```

```
if ($PSBoundParameters.ContainsKey('ParameterType')) {
```

```
$ParameterType = $ParameterType.ToLower()
$Body = @"
```