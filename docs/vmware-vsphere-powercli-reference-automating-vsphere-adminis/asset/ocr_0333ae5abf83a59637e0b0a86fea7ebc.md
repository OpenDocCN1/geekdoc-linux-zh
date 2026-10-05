```
Write-host "Host Preparation initiated"
}
catch [Exception] {
```

```
throw "Error occurred while trying to prepare hosts"
}
```

# Install and Configure VXLAN

Now that your hosts have been prepared, the only thing left to do in preparation for creating your logical networks and logical switches is to install and configure VXLAN on these hosts. VXLAN enables the creation of a Layer 2 network on top of Layer 3; see Listing 3.31.

+   LISTING 3.31 Installing and configuring VXLAN {

```
function Install-VXLAN {
<<
.SYNOPSIS
Install VXLAN on Cluster
.DESCRIPTION
Install VXLAN on Cluster
.PARAMETER NSXP
NSX IP Address
.PARAMETER NSXPassword
The NSX Admin password given during deploy
.PARAMETER Cluster
Name of the target cluster
.PARAMETER DVS
Name of Distributed Switch
.EXAMPLE
Install-VXLAN -NSXIP 10.144.99.22 -NSXPassword Vmwarel! -Cluster "Main-CL" -vDS-Main"
#
Param (
[parameter (Mandatory=$true)]n[ValidateNotNullOrEmpty()]]
```