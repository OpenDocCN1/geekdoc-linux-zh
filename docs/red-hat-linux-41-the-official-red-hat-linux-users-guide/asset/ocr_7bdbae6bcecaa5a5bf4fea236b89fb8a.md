```
FMU> program
Image is:
Firmware Id: 7 (Milo/Linux)
Image size is 217896 bytes (4 blocks)
Executing at 0x200000
Found existing image at block 8
Overwrite existing image? (N/y)? y
Do you really want to do this (y/N)? y
Deleting blocks ready to program: 8 9 10 11
Programming image into flash
Scanning Flash blocks for usage
FMU>
```

Wait until it has completed before powering off your system.

Note: I cannot emphasise just how careful you must be here not to overwrite an existing flash image that you might need or render your system useless. A very good rule is never to overwrite the Debug Monitor.

# E.7.4 The “environment” command

This selects a flash block to contain Milo’s environment variables.

# E.7.5 The “bootopt” command

This is just the same as Milo’s “bootopt” command, see (Section E.6.4 The “bootopt” command).

# E.7.6 The “quit” command

This is really pretty meaningless. The only way back to Milo (or anything else) once the flash management utility has run is to reboot the system.

# E.8 Restrictions

Unfortunately this is not a perfect world and there, as always, some restrictions that you should be aware of.