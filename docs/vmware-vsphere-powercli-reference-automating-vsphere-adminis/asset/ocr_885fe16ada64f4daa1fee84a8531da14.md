Let's take an example where the static baseline created earlier in the chapter for hosts contains a patch (ESXi550-20140401-BG) that causes issues in your organization. You now need to update your baseline to exclude this patch.

First, retrieve a new set of patches to manage the issue. Then, update the static baseline to remove this patch from the list of patches to be deployed, applying the updated set of patches to the baseline (Listing 14.6).

# LISTING 14.6 Updating patches in a baseline

```
$UpdatedPatches = Get-Patch -TargetType -Vendor VMware* \
-Product 'embeddedESX 5.0.0' -After 2014.01.01 \
Where-Object {$.IdByVendor -ne 'ESXi550-20140401-BG'} \
Get-PatchBaseline -Name 'ESXi' -Current (Static)' | \
Set-PatchBaseline -IncludePatch $UpdatedPatches
```

The number of patches now present in this baseline is seven, one less than the previous:

> ((Get-PatchBaseline \
-Name 'ESXi' - Current (Static)').CurrentPatches).count

Other properties or search criteria used to create baselines can also be modified using the Set-PatchBaseline cmdlet.

# Attaching and Detaching Baselines

You have learned how to automate the creation of baselines, but they are not much until they are attached to a host or VM. To be able to scan a host or VM to discover what patches are required and subsequently deploy them, you must have one or more baselines attached. You can attach a baseline directly to a host or VM or allow it to be inherited from a parent object such as a cluster or datacenter.

The Attach-Baseline cmdlet is used to connect a baseline with a vCenter object. Although it is possible to attach a baseline directly to all hosts in a cluster, it is easier to attach the baseline at the cluster level and let the hosts inherit it. This means that any new hosts in the cluster will automatically inherit the correct baseline line.

To attach a baseline at a cluster level, simply return the cluster object and attach the baseline to that object (Listing 14.7).

![](bbox=[0.913, 0.355, 0.978, 0.532])