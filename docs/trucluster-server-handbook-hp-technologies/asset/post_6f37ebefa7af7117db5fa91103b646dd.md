
## 7.4.5 How Can I See All the Information for a Specific Component?

```
# hwmgr -get attribute -id 46

46:
name = COMPAQ AlphaServer DS10 466 MHz
category = platform
memory_size_MB = 256
registration_time = Tue Mar 20 12:39:23 2001
user_name = (null) (settable)
location = (null) (settable)
software_module = (null)
state = available
state_previous = unknown
state_change_time = none
event_count = 0
last_event_time = none
```

## 7.4.6 How Can I See Only a Few Attributes for Some Components?

You can see as little as one attribute by specifying that particular attribute with the "-a attribute" option.

```
# hwmgr -get attribute -a dev_base_name -id 59

59:
dev_base_name = dsk7
```

Here is an example showing several attributes, including searching for an attribute NOT containing a certain value.

```
# hwmgr get -a name -a dev_base_name -a power_mgmt_capable!=1

2:
name = CPU0
power_mgmt_capable = 0

30:
name = FDI-fdio-unit-0
dev_base_name = Floppy0
power_mgmt_capable = 0

45:
name = SCSI-WWID:0710002c::"COMPAQ   CRD-8402B" :d05b000:00000100000*
dev_base_name = cdrom0
power_mgmt_capable = 0
```

Here is a similar example where we are searching for an attribute that contains a particular value. We are also limiting our search to the "disk" category.

```
# hwmgr -get -a -a dev_base_name -a cluster_disables=1 -cat disk
45:
dev_base_name = cdrom0
cluster_disables = 1
```

Note that some of the conditional parsing does not work as expected. For example, the component at HWID 40 has "COMPAQ" listed as the manufacturer.

```
# hwmgr -get -a -a manufacturer -id 40
40:
manufacturer = COMPAQ
```

Yet, when we specifically state "manufacturer!=COMPAQ", we get the opposite of what we would expect.

```
# hwmgr -get -a -a manufacturer!=COMPAQ
40:
manufacturer = COMPAQ
...
```

If we look for "manufacturer=COMPAQ", we do not see any output.

```
# hwmgr -get -a -a manufacturer=COMPAQ
<no output>
```

We considered that it might be a string parsing problem, but:

```
# hwmgr -get -a -a dev_base_name -a state=available -cat disk
30:
dev_base_name = floppy0
state = available
40:
dev_base_name = dsk0
state = available
...
```

This appears to be a bug, and we have notified COMPAQ's Customer Support Center.

### 7.4.7 How Can I Set the “settable” Attributes for a Component?

Some components have user settable attributes like a name (`user_name`) or physical location (`phys_location`). In large configuration, the ability to give a device a name that is meaningful to you, such as “my boot disk” or its location, can be very useful. First, let’s find the “settable” attributes for a particular device.

```
# hwmgr --get attr -id 46 | grep "(settable)"

user_name = (null) (settable)
location = (null) (settable)
```

What device is this?

```
# hwmgr --get attr -id 46 -a name

46:
  name = COMPAQ AlphaServer DS10 466 MHz
```

It’s the system. Well, let’s set the “user_name” to the system’s hostname. Note that the “user_name” attribute is currently limited to fifteen characters. For example:

```
# hostname | wc -c

17
```

Notice that the fully qualified hostname of this system is sixteen characters (“wc -c” returns an extra character, probably the newline character). So let’s try to set the attribute with more than fifteen characters.

```
# hwmgr --set attr -a user_name=$(hostname) -id 46
hwmgr: 46: Attribute "user_name" value is too large.
```

Now let’s set the “user_name” attribute by using only the base hostname.

```
# hwmgr --get attr -a user_name=$(hostname -s) -id 46

46:
  user_name = sheridan (settable)
```

Verify that the change has taken place.

```
# hwmgr -get attr -id 46 -a name -a user_name
46:
name = COMPAQ AlphaServer DS10 466 MHz
user_name = sheridan (settable)
```

## 7.4.8 How Can I Find a Device?

If you happen to have a large cabinet with a bunch of disks in it, wouldn’t it be nice to be able to find the device you are looking for quickly? Well, it can be. Try this:

```
# hwmgr -flash light -dsc dsk3
```

Although this only works on SCSI disks, most disks are currently still SCSI, so for the immediate future, this is a useful command. By the way, if the flashing is too slow or fast due to other disk activity in the cabinet, try the "-nopause" option.

## 7.4.9 How Can I Find a Device with Inconsistent Data?

You can use the "hwmgr show component" command with the "-inconsistencies" command to locate software inconsistencies in the hardware component database files. An "inconsistency" is a possible internal error in the dec_hwc_cdb and dec_hwc_ldb files.

```
# hwmgr show comp -i
HWID: HOSTNAME FLAGS SERVICE COMPONENT NAME
--------------------------------------------
106: molari rcd-i iomap SCSI-WWID:0c000008:0000-0e11-0018-9f1f
```

You can obtain additional information by adding the "-full" option.

## 7.5 The Device Special File Manager (dsfmgr)

### 7.5.1 The dsfmgr(8) Command

The dsfmgr command is used to manage device special files using the new naming convention defined in Tru64 UNIX version 5.0. The following database files are used by dsfmgr:
