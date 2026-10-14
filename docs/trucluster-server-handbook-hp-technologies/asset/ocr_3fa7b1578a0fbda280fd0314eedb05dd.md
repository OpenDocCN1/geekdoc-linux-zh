# 23.4.12 Updating a Registered Resource

Any time that modifications are made to a resource profile, CAA must be notified. Registered profiles are stored in the caa.reg database in /var/cluster/caa/registry and not read from the profile directory.

If the profile is for an application resource, the profile can be updated using the caa_register command with the "-u" option.

```
# caa_register -u myApplicationResource
```

# NOTE:

Prior to V5.1B, if the resource is a non-application resource, then the resource must be unregistered and then registered. Since non-application resources are only used as a dependency for an application resource, this presents a bit of an inconvenience in that the application resource must also be unregistered and then registered.

For example, say we have a network resource (nicUP) that is a REQUIRED_RESOURCE for an application resource (memberUP). When we attempt to unregister the profile we receive an error.

```
# caa_unregister nicUP
Can't unregister 'nicUP' because it is required by other resources.
Could not unregister resource nicUP.
```

So we must unregister every resource that depends on nicUP.

+   1. Find the resources that require the nicUP resource.

```
# grep nicUP *.cap | grep -v nicUP.cap
memberUP.cap:REQUIRED_RESOURCES=nicUP
```

+   2. If the resource is running, stop it.

```
# caa_stat -a memberUP -r && caa_stop memberUP
Attempting to stop 'memberUP' on member 'molari'
Stop of 'memberUP' on member 'molari' succeeded.
```

Note that we used the "-r" option with the "-a" option to the caa_stat command to see if the resource was running.

+   3. If the resource is registered, unregister it.

```
# caa_stat -a memberUP -g && caa_unregister memberUP
```

Note that we used the "-g" option with the "-a" option to the caa_stat command to see if the resource was registered.