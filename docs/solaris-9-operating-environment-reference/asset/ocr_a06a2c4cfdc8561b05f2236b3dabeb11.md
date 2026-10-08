# 688

# llc2_config

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWll1c |

# See Also

llc2_config(1), llc2(4), attributes(5), llc2(7D)

# ## New llc2_config — Configure LLC2 Interface Parameters

# Synopsis

```
/usr/lib/llc2/llc2_config [-P | -U -d -q -i ppa] -r ppa
```

# Description

Use the llc2_config command, new in the Solaris 8 Operating Environment, to start and stop the LLC2 subsystem and to configure LLC2 interface parameters.

# Options

+   -d Turn on debug mode to print extra debugging information.
-i ppa Initialize the corresponding interface using the file /etc/llc2/default/llc2.ppa.
-P Read in all /etc/llc2/default/llc2 configuration files, devices defined in the files, and set up the streams needed for LLC2 to use those devices. Before you use this command, llc2_config -q shows nothing.
-q Query the LLC2 subsystem. Information similar to that shown in the following example is printed for all PPAs (Physical Point of Attachment) available under the LLC2 module.

```
PPA State ID Maddr Type MaxSD MinSD Mode
0 0000 00208a217e ethernet 1500 0
```

The fields are described below:

+   PPA The relative logical position of the interface.
State The state of the interface.\dup The interface is initialized and operational.
down The interface was discovered by the LLC2 driver, has passed its boot diagnostics, and is awaiting initialization.