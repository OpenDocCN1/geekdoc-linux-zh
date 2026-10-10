is the type of the image to be booted the next time the system is power cycled or reset.

+   0 Boot the Evaluation Board Debug Monitor,
+   1 Boot the Windows NT ARC firmware.

In order to tell the boot code to boot the MILO firmware from flash then you need a boot option that means boot the N'th image. For this, you need to 128 plus N, so if MILO is the third image, you would use the command:

```
MILO> bootopt 131
```

Note: Be very careful with this command. A good rule is never to set bootopt to 0 (the Evaluation Board Debug Monitor), but instead use the system's jumpers to achieve the same thing.

# ## D.7 Running the Flash Management Utility

The run command is used to run the flash management utility. Before you start you will need a device available to MILO that contains the updateflash program. This (like vminilux) can be gzip\'d. You need to run the flash management utility program from the MILO using the (run) command:

```
MILO> run fd0:fm.u.gz
```

Once it has loaded and initialised, the flash management utility will tell you some information about the flash device and give you a command prompt. Again the help command is most useful.

```
Linux MILO Flash Management Utility V1.0

Flash device is an Intel 28f008SA
16 segments, each of 0x10000 (65536) bytes
Scanning Flash blocks for usage
Block 12 contains the environment variables
FMU>
```

Note that on systems where environment variables may be stored and where there is more than one flash block (for example, the AlphaPC64) the flash