```
[String]$NSXIP,
```

```
[parameter(Mandatory=$true)]n[ValidateNotNullOrEmpty()]
[String]$NSXPassword,
```

```
[parameter(Mandatory=$true)]n[ValidateNotNullOrEmpty()]
[String]$Cluster,
```

```
[parameter(Mandatory=$true)]
[ValidateNotNullOrEmpty()]
[String]$DVS
)
```

```
try {
    # Deal with certificate issues
    # Note: this will cause the cert handling behavior for the
current
    # PowerShell session to trust all certs whether they are
valid,
    # self-signed, invalid, or etc
    Add-Type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
ublic class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
        ServicePointPoint, X509Certificate certificate,
        WebRequest request, int certificateProblem) {
        return true;
    }
}
```

```
@"
[System.Net.ServicePoint]::CertificatePolicy = `
New-Object TrustAllCertsPolicy
```

```
# Create REST Headers
$Auth = "admin" + ':' + $NSXPassword
$Encoded = [System.Text.Encoding]::UTF8.GetBytes($Auth)
$EncodedPassword = [System.Convert]::ToBase64String($EncodedPassword)
```