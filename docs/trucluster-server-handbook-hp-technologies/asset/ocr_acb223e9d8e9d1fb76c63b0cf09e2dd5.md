3. You can now use the attribute.

For example, we will create a new application resource using the new attributes.

```
```shell
# caa_profile -create aliasAPP -t application -B /code/caa/aliasAPP \
> -o arcaa_alias,aaq=192.168.1.71
```
```

We can verify that the resource was created by printing the resource profile using the caa_profile command. Note the output has been trimmed.

```
```shell
# caa_profile -print aliasAPP | grep -E "NAME|ALIAS"
NAME=aliasAPP
USR_ALIAS_IP=192.168.1.71
USR_ALIAS_NAME=caa_alias
```
```

# 23.5.3.3.2  *Using a User-Defined Attribute in an Action Script*

User-defined attributes can be accessed within an application resource’s action script by adding an underscore prefix to the attribute name.

For example, we added two print statements to the action script of the aliasAPP resource we created in the previous section.

```
```shell
# grep print aliasAPP.scr

print "_USR_ALIAS_NAME = ${_USR_ALIAS_NAME}"
print "_USR_ALIAS_IP = ${_USR_ALIAS_IP}"
```
```

We still have the __CAA_UI_FMT environment variable set from section 23.5.2, so all we need to do is register and start the resource (of course, we had to modify the action script and test it too).

```
```shell
# caa_register aliasAPP
```
```

```
```text
# caa_start aliasAPP
Attempting to start 'aliasAPP' on member 'sheridan'
Start of aliasAPP on member 'sheridan' succeeded.
_USR_ALIAS_NAME = "caa_alias"
_USR_ALIAS_IP = "192.168.1.71"
```
```

As you see by the output, our user-defined attributes are accessible from the action script.

# 23.5.3.3.3  *Modifying a User-Defined Attribute Value Temporarily*

You can temporarily modify a user-defined attribute using the caa_start, caa_stop, and caa_relocate commands.