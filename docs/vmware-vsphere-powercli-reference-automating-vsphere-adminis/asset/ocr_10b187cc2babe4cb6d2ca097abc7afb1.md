# CREATE AN AUTOMATED INSTALLATION

# Networking
$json.vcsa.networking.mode="static"
$json.vcsa.networking.ip="10.144.99.19"
$json.vcsa.networking.prefix="24"
$json.vcsa.networking.gateway="10.144.99.1"
$json.vcsa.networking.dns.servers="10.144.99.55"
$json.vcsa.networking.system.name="10.144.99.19"
$json | ConvertTo-Json | Set-Content -Path "$updatedconfig"
Invoke-Expression "$installer $updatedconfig"

**Figure 1.1** Sample VCSA import process

![](bbox=[0.298, 0.477, 0.77, 0.818])

```
vCSA installer finished deploying "VCSA6", an embedded node:
System Name: VCSA6.LOCAL
Login as: administrator@vsphere.local
PS C:\Windows\System32 _>
```