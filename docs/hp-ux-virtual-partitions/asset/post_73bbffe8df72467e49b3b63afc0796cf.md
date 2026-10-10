
## Appendix A
### Virtual Partitions Online Manual Pages

The commands for working with Virtual Partitions appear in every chapter in this book. Many examples are provided in the chapters. In addition, the Quick Reference Tear Out card has on it summaries and examples of all of the commands. There is, however, nothing like the command detail that appears in the man pages for a command. The man pages for Virtual Partitions commands are well written and thorough. This appendix consists of the manual pages for Virtual Partitions commands only. The following is a list of the commands:

- **vparboot** - Boots (starts) a virtual partition.
- **vparcreate** - Creates a new virtual partition.
- **vparmodify** - Modifies an existing virtual partition.
- **vparremove** - Removes (deletes) an existing virtual partition.
- **vparreset** - Sends a TOC or hard reset to a virtual partition.
- **vparresources** - Provides description of Virtual Partitions and their resources.
- **vparstatus** - Displays virtual partition and available resources information.
- **vpartition** - Displays information about the vPars Command Line Interface.
- **vparutil** - Works with SCSI information of disks in vPar.

## vparboot

vparboot - Boots (starts) a virtual partition.

**vparboot (1M)**

### NAME
vparboot - boot a virtual partition

### SYNOPSIS
```
vparboot -p vp_name [-b kernel_path] [-o boot_opts] [-B boot_addr]
vparboot -p vp_name -i ignite_kernel
```

### DESCRIPTION
The vparboot command causes the virtual partition monitor to boot the specified virtual partition. The monitor must be running. The virtual partition must exist in the monitor configuration and be in the Down state. For example, not running. For this reason, it is not possible to boot the current partition using this command. The partition in which the command is executing is called the current partition.

Only a superuser can execute the vparboot command.

### Options
'vparboot' recognizes the following command line options and arguments:

- **-p vp_name**  
  Specifies the unique name of the virtual partition which is to be booted. The virtual partition must exist in the monitor's database, must be in the Down state, and must have a configured boot device. Required.

- **-b kernel_path**  
  Specifies the absolute path to a bootable kernel for the virtual partition. For example, if a non-partitioned system start string at the ISL prompt is:
  `ISL> hpx -is /stand/vmunix`
  
  the kernel-path is the `/stand/vmunix` portion of this string.

  If this option is omitted, the value is taken from any `-b kernel_path` specified during virtual partition creation or its most recent modification, or `/stand/vmunix` if `-b kernel_path` has never been specified.

- **-o boot_opts**  
  Specifies the command-line options applied when the virtual partition is booted. For example, if a non-partitioned system start string at the ISL prompt is:
  `ISL> hpxx -15 /stand/vmunix`
  
  the boot_opts string in this case will be `-15`.
  
  Note that if any whitespace is included in the string, the string must be quoted.

  Refer to the virtual partitions administration guide and the chapter titled “Monitor and Shell Commands” for a full list of supported boot option strings.

  If the `-o` option is omitted, the value is taken from any `-o boot_opts` specified during virtual partition creation or its most recent modification, or the empty string if `-o boot_opts` has never been specified.

- **-B boot_addr**  
  Specifies the device from which the virtual partition kernel image is read. It must be one of the following three forms:

  - `bct[0] | pri(mary)` (case-insensitive). This is the default if the -B option is omitted. vparboot attempts to boot vp_name from the device previously configured with the BOOT attribute. It is an error if no device has been so configured.
  - `alt[ernate][boot]` (case-insensitive). vparboot attempts to boot vp_name from the device previously configured with the ALTBOOT attribute. It is an error if no device has been so configured.
  - **Boot From Hardware Path:** Any other string is assumed to be the hardware path (for example, 10/0) to the desired boot device. vparboot does not check any part of such a specification. If it is not a proper path, the path does not exist, the virtual partition does not own the device at that path, or there is no bootable device at that path, the command either fails with an error, or the boot attempt fails with no error indication.

- **-I ignite_kernel**  
  Specifies a path to a cold-install kernel such as `/opt/ignite/boot/WINSTALL`. This form of the command is used to cold-install an instance of HP-UX on a virtual partition. Most often, this is done on a newly-created virtual partition, one that has a completely unwritten disk. However, it can be used to cold-install HP-UX over an existing instance.

  ignite_kernel can reside either on the current virtual partition (the one on which vpboot is run) or on any other networked system or virtual partition accessible from that partition. The syntax for ignite_kernel is:
  `[Server name or IP addr,]cold-install_kernel`

  If cold-install_kernel begins with a slash, “/”, you are specifying an absolute path and vpboot looks for it at that location. If cold-install_kernel does not begin with “/”, the default path `/opt/ignite/boot/` is prepended to cold-install_kernel.

  If the Server name or IP address is not specified, vpboot loads the cold-install kernel from the filespace of the current virtual partition. Otherwise the command loads it from the filespace of the specified server. The comma is a required part of the server name syntax.

### RETURN VALUE
The vpboot command exits with one of the following values:
- 0 Successful completion.
- 1 One or more error conditions occurred.

### EXAMPLES

Boot the virtual partition called Oslo
```
vpboot -p Oslo
```

Boot the virtual partition Bergen specifying an alternate kernel
```
vpboot -p Bergen -b /stand/vmunix_debug
```

Cold-install the virtual partition Trondheim from a file on a remote server
```
vpboot -p Trondheim -i mysys.myserver.mysdomain.com:/mypath/mysinst
```

Cold-install the virtual partition Sandefjord from a file at the default path /opt/ignite/boot on the current virtual partition
```
vpboot -p Sandefjord -I MINSTALL
```

### ERRORS
vpboot displays error messages on stderr for any of the following conditions:
- VP_name does not exist in the monitor.
- VP_name is in some state other than Down, and so cannot be booted. Use the vpareset(1M) command instead.
- An error occurs while trying to access an Ignite server or cold-install file.
- You have specified the BOOT or ALTBOOT device, but the corresponding device has not been configured in vp_name.

NOTE: If the boot device has not been configured properly the vpboot command will complete without errors, but the virtual partition will not boot. Two possible reasons for this could be:
- The BOOT or ALTBOOT attribute was assigned to a device other than a disc or tape.
- The file at the default or configured kernel path does not exist or is not a bootable image.

### AUTHOR
vpboot was developed by the Hewlett-Packard Company.

### SEE ALSO
vpcreate(1M), vpmodify(1M), vpremove(1M), vpreset(1M), vpstatus(1M), vpreources(5), vpartition(5).

## vparcreate

vparcreate - Creates a new virtual partition.

**vparcreate[1M]**

### NAME
vparcreate - create a virtual partition

### SYNOPSIS
```
vparcreate -p vp_name [-B boot_attr] [-D db_file] [-S static_ctrl]
        [-b kernel_path] [-O boot_opts] [-a rsrc]...
```

### DESCRIPTION
The **vparcreate** command creates a new virtual partition (vPar) using the specified hardware resources. **vp_name** is a symbolic name for the virtual partition and must be used in all references to it. If the *-D* option is specified, the **virtual partition is created in db_file**. Otherwise it is created in the virtual partition monitor database. In either case, a virtual partition named **vp_name** must not already exist in the database. Any error terminates the command without creating a virtual partition.

Only a superuser can execute the **vparcreate** command.

### Options
No option except *-a* (add resource) may be specified more than once. Resources allocated with the *-a* option must be available, that is, not already allocated to a virtual partition, not exceeding the overall limits of the resources. Resources assigned with multiple *-a* options must not conflict. Violation of any condition is a command error.

The **vparcreate** command recognizes the following command line options and arguments:

| Option | Description |
| :--- | :--- |
| -p vp_name | Specifies the symbolic name of the virtual partition. The name can consist of alpha-numeric characters A-Z, a-z, 0-9, the underscore character (_), and the period (.). The maximum length of the name is 259 characters. Required. |
| -B boot_attr | Specifies the autboot attribute of the virtual partition. **boot_attr** can have the following (case-insensitive) values: |
| &nbsp;&nbsp;&nbsp;&nbsp;auto | sets the autoboot attribute. |
| &nbsp;&nbsp;&nbsp;&nbsp;manual | clears the autoboot attribute. |
| | If the autoboot attribute is set to **auto**, the virtual partition is rebooted after a successful **vparreset** command or when the virtual partition monitor is first loaded, if appropriate monitor options have been specified. |
