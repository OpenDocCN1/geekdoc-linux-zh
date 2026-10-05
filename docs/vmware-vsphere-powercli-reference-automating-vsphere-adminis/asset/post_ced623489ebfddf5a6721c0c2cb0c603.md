
# CHAPTER 3 : AUTOMATING NETWORKING

```powershell
try {
    # --- Deal with certificate issues
    # Note: this will cause the cert handling behavior for the
    # current PowerShell session to trust all certs whether they are
    # valid,
    # --- self-signed, invalid, etc
    Add-Type @"
    using System.Net;
    using System.Security.Cryptography.X509Cert;
    public class TrustAllCertsPolicy : ICertificatePolicy {
        public bool CheckValidationResult(
            ServicePoint srvPoint, X509Certificate certificate,
            WebRequest request, int certificateProblem) {
            return true;
        }
    }
@"
```

[System.Net.ServicePointManager]::CertificatePolicy =
New-Object TrustAllCertsPolicy
```

```powershell
# -- Create REST Headers
$Auth = "admin" + ':' + $NSXPassword
$Encoded = [System.Text.Encoding]::UTF8.GetBytes($Auth)
$EncodedPassword = [System.Convert]::ToBase64String($Encoded)
$Headers = @{"Authorization":"Basic $($EncodedPassword)"}
$ClusterID = Get-Cluster $cluster | Get-View -Property Name
```

```powershell
# -- Send request and process results
```

```powershell
$uri = "https://$NSXIP/api/2.0/nwfabric/config"
$body = "<nwFabricFeatureConfig><resourceConfig>"
$body += "<resourceID=$($ClusterID.MoRef.Value)</resourceId>"
$body += "</resourceConfig></nwFabricFeatureConfig>"
```

```powershell
$PreHosts = Invoke-RestMethod -Post -Uri $uri \
Headers $Headers -ContentType "application/xml" -body $body
```

```powershell
Write-host "Host Preparation initiated"
}
catch [Exception] {
    throw "Error occurred while trying to prepare hosts"
}
```

# Install and Configure VXLAN

Now that your hosts have been prepared, the only thing left to do in preparation for creating your logical networks and logical switches is to install and configure VXLAN on these hosts. VXLAN enables the creation of a Layer 2 network on top of Layer 3; see Listing 3.31.

- LISTING 3.31 Installing and configuring VXLAN {

```powershell
function Install-VXLAN {
<<
.SYNOPSIS
Install VXLAN on Cluster
.DESCRIPTION
Install VXLAN on Cluster
.PARAMETER NSXIP
NSX IP Address
.PARAMETER NSXPassword
The NSX Admin password given during deploy
.PARAMETER Cluster
Name of the target cluster
.PARAMETER DVS
Name of Distributed Switch
.EXAMPLE
Install-VXLAN -NSXIP 10.144.99.22 -NSXPassword Vmwarel! -Cluster "Main-CL" -vDS-Main
#
Param (
    [parameter (Mandatory=$true)][[ValidateNotNullOrEmpty()]]
    [String]$NSXIP,

    [parameter(Mandatory=$true)][[ValidateNotNullOrEmpty()]
    [String]$NSXPassword,

    [parameter(Mandatory=$true)][[ValidateNotNullOrEmpty()]
    [String]$Cluster,

    [parameter(Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [String]$DVS
)

try {
    # Deal with certificate issues
    # Note: this will cause the cert handling behavior for the
    # current
    # PowerShell session to trust all certs whether they are
    # valid,
    # self-signed, invalid, or etc
    Add-Type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
        ServicePoint srvPoint, X509Certificate certificate,
        WebRequest request, int certificateProblem) {
        return true;
    }
}
@"
[System.Net.ServicePoint]::CertificatePolicy = `
New-Object TrustAllCertsPolicy

# Create REST Headers
$Auth = "admin" + ':' + $NSXPassword
$Encoded = [System.Text.Encoding]::UTF8.GetBytes($Auth)
$EncodedPassword = [System.Convert]::ToBase64String($Encoded)

$Headers = @{"Authorization":"Basic $($EncodedPassword)"};
$CLID = Get-Cluster cluster | Get-View -Property Name
$NetID = Get-DVSwitch $DVS | Get-View -Property Name

# -- Send REST call and process results
$uri = "https://NSXIP/api/2.0/nwfabric/configure"
$body = "nwFabricFeatureConfig<featureId>"
$body += "<com.vmware.vsield.nsxmgr.xlan>"
$body += "<resourceConfig resourceId=$($CLID.MoRef.Value)">
$body += "</resourceId>
$body += "<configSpec class="clusterMappingSpec">
$body += "<switch><objectId>$($NetID.MoRef.Value)</objectId>
$body += "<vlanId>0</vlanId></switch>
$body += "<vmknicCount>$$vmknicCount</vmknicCount>
$body += "</resourceConfig></resourceConfig>
$body += "<resourceConfigId=$($NetID.MoRef.value)</resourceId>
$body += "<configSpec class="vdcContext">
$body += "<switch><objectId>$($NetID.MoRef.value)</objectId>
$body += "<switch><mtu>1600</mtu><teaming></switch>
$body += "<FAILOVER_ORDER</teaming></configSpec>
$body += "</resourceConfig></nwFabricFeatureConfig">

$VXLAN = Invoke-RestMethod -Method Post -Uri $uri
-Headers $Headers -ContentType "application/xml" -body $body

}
catch [Exception] {
    throw "Error occurred while trying to install VXLAN"
}
```

# Further Configuration and Administration of NSX

You have now some examples of REST calls using PowerShell to configure NSX. Once VXLAN is configured on all the hosts in the cluster, you are ready to finalize the logical network settings, creating logical networks, and benefit from all of the capabilities and functionality of NSX. To continue REST calls to configure NSX, you may refer to VMware's NSX API Guide. The guide for NSX 6.2, for example.
