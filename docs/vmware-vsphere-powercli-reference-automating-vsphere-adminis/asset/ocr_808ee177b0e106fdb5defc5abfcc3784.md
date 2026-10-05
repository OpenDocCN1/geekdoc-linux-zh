# SET UP THE NETWORK

```
$Auth = "admin" + ':' + $NSXPassword
$Encoded = [System.Text.Encoding]::UTF8.GetBytes($Auth)
$EncodedPassword = [System.Convert]::ToBase64($Encoded)
$Headers = @{"Authorization="Basic ($EncodedPassword)"};
```

# -- Send REST call and process results

```
$uri = "https://NSXIP/api/2.0/services/vcconfig"
$body = "<vcinfo<ipaddress>$vcIP</ipaddress>"
$body += "<username>$vcuser</username><password>"
$body += "<vcpass/password>certificateThumbprint"
$body += "<thumb>/certificateThumbprint>"
$body += "<assignRoleToUser>$assignRoleToUser>"
$body += "</vcinfo>"
```

```
$ConnectVC = Invoke-RestMethod -Method Post -Uri $uri `
-Headers $Headers -ContentType "application/xml" -body $body

$QueryVC = Invoke-RestMethod -Method Get -Uri $uri `
-Headers $Headers -ContentType "application/xml"
if ($QueryVC) { Write-host "NSX Manager Connected" }
```

```
catch [Exception]{

throw "Unable to connect NSX with vCenter"
}
```

# Adding an IP Pool for NSX Controllers

The NSX controller is the mechanism that stores information on and controls the logical networks created in NSX. A deep dive into NSX technology and its functions is outside the scope of this book—just know that NSX controllers must exist in order for NSX to work. Before you can deploy an NSX controller, you must add an IP pool for the NSX controllers, Virtual Extensions Lanes (VXLANs), and VXLAN Tunnel Endpoints (VTEPs) to pull from. These IP pools are not the same as IP pools found within vCenter Server. Listing 3.28 is a function that creates an NSX IP pool.