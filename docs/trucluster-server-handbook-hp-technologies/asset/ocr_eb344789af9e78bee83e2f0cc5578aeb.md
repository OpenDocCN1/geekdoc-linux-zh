# 23.4.19.1 How Can I Determine If a Resource is Registered?

There are a couple of ways to determine whether or not a resource is registered. You can use the caa_stat command followed by the resource name. If the resource is not registered you will receive an error.

```
# caa_stat aNonRegisteredResource
Could not find resource aNonRegisteredResource.
```

However, if you're writing a script, it would be much easier to be able to check the return status of the caa_stat command by using the "-g" switch with the "-a resource" switch.

```
# caa_stat -g -a memberUP ; echo $?
0
```

If the resource is registered, a zero is returned.

```
# caa_stat -g -a aNonRegisteredResource ; echo $?
1
```

If the resource is not registered, a value of "1" is returned.

# 23.4.19.2 How Can I Determine If a Resource is Running?

You can use the caa_stat command followed by the resource name. If the resource's STATE is ONLINE, it's running.

You can use the caa_stat command with the "-r -a resource" switches to check the return status. This is particularly useful if you're writing a script.

```
# caa_stat -r -a memberUP ; echo $?
0
```

If the resource is running, a zero is returned. Conversely, if the resource is not running, a "1" is returned.

```
# caa_stop memberUP
Attempting to stop 'memberUP' on member 'alph12'
Stop of 'memberUP' on member 'alph12' succeeded.
```

```
# caa_stat -r -a memberUP ; echo $?
1
```