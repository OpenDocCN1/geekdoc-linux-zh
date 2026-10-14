If you want to relocate the application resource to a specific member, you can use the “-c” option (output not shown).

```
```text
# caa_relocate -c sheridan memberUP
```
```

You can modify user-defined resource attributes when relocating a resource.

```
```text
# caa_relocate USR_ATLAS_IP=192.168.0.74 atlasAPP
```
```

See section 23.5.3.3 for more information on user-defined resource attributes.

If an application resource’s PLACEMENT is set to “restricted” and there are no other HOSTING_MEMBERs available, you will see the following error:

```
```text
# caa_relocate memberUP
molari : Resource memberUP (application) cannot run on molari
Resource memberUP has placement error.
```
```

The resource will continue running on the member where it is currently placed.

A final note regarding relocation: you can use “-s” option to relocate all the resources currently running on that member to another member.

```
```text
# caa_relocate -s molari
Attempting to stop 'memberUP' on member 'molari'
Stop of 'memberUP' on member 'molari' succeeded.
Attempting to start 'memberUP' on member 'sheridan'
Start of 'NICUP' on member 'sheridan' succeeded.
Attempting to start 'memberUP' on member 'sheridan'
Start of 'memberUP' on member 'sheridan' succeeded.
Attempting to stop 'cluster_lockd' on member 'molari'
Stop of 'cluster_lockd' on member 'molari' succeeded.
Attempting to start 'cluster_lockd' on member 'sheridan'
Start of 'cluster_lockd' on member 'sheridan' succeeded.
```
```

**Note**, resources with a PLACEMENT of “restricted” will not relocate unless another member in the HOSTING_MEMBER attribute is available. Also, a resource’s REQUIRED_RESOURCES must be available on the target member in order for the relocation to succeed.

For more information regarding resource relocation, see the caa_relocate(8) reference page.

# 23.4.17 Load-Balancing Resources

Placement of an application resource, based on the load of a particular cluster member, can be accomplished using one of methods shown in Table 23-12.