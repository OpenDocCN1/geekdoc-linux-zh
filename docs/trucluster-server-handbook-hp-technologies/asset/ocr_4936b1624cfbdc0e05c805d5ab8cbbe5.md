# NOTE:

You cannot delete a profile that is associated with a registered resource. You'll receive the following error:

```
Can not delete profile for resource nicUP as it is currently registered.
```

See section 23.4.13 for more information on unregistering a resource.

# CAUTION:

Prior to V5.1B, using caa_profile with the "-delete" option to remove an application resource's profile will also delete the resource's action script! Note, "sysman" will do the same thing.

```
# caa_profile -delete memberUP
```

```
# ls /var/cluster/caa/script/memberUP.scr
ls: /var/cluster/caa/script/memberUP.scr not found
```

For more information on the caa_profile command, see the caa_profile(8) reference page.

# 23.4.11 Registering a Resource

Once you have created and edited a resource profile, the resource must be registered with CAA before it can be managed or monitored.

# NOTE:

Before registering a resource with CAA you should always do the following:

+   - Validate the profile (see section 23.4.7).
+   - If it is an Application Resource, see the "scripting tips" in section 23.5.1.
+   - If it is a non-application resource make sure that it is configured.

You can register a profile using the caa_register command.

```
# caa_register myResource
```

For more information on registering resources, see the caa_register(8) reference page.