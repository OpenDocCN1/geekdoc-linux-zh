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