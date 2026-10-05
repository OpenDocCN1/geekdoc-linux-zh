334 CHAPTER 10 • USING VAPPS

```
$OvfConfig.Common.guestinfo.cis.appliance.ssh.enabled.Value = "True"
```

```
# create a hash table with all the configuration
$Splat = @{
  'Name' = 'VCSA'
  'VMHost' = (Get-VMHost ESX1)
  'Source' = $Path

  'OvfConfig' = $OvfConfig
  'DiskStorageFormat' = 'Thin'
}
```

#Import the vApp using Splat to inject parameters
Import-VApp @Splat

Virtual appliances can simplify the deployment of a new VM. vApps bring simplicity at a scale that was previously only available to the largest hosting providers.

# Create Your Own vApps

vApps are a resource pool at their base, so when creating a new vApp, resource guarantees are where it all starts. There are three ways to create a new vApp in your environment.

+   - Create a new vApp.
- Clone an existing vApp.
- Import a vApp from an OVF/OVA.

Listing 10.3 creates a new vApp that conforms to the following specification:

+   - Name: App01
- Location: Cluster Prod1
- Reserve 4 GHz CPU
- Reserve 6 GB of RAM