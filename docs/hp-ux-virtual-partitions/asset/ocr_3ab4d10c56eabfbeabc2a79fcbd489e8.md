# Defaults

Default values chosen by hpx to complete a command are obtained through a sequence of steps. First, any components of the command specified explicitly are used. If the command is not complete, hpx attempts to construct defaults from information maintained by pdc (see pdc(8M)). If sufficient information to complete the command is unavailable, the autoexecute file is searched. If the search fails, any remaining unresolved components of the command are satisfied by hard-coded defaults.

There is no hard-coded default choice for a manager; if none can be chosen, hpx reports an error.

When the hardware path to the boot device is not specified, hpx defaults to information maintained by pdc. The hardware path element has no hard-coded default.

If the minor number element is not supplied, hpx takes its default from the autoexecute file. Failing that, the hard-coded default of 0 is used.

For the boot command, a devicefile specification without a file name indicates that the boot device does not contain an HP-UX file system. hpx interprets this as a NULL (instead of missing) file name and does not search for a default. If the entire devicefile specification is missing, hpx searches for a default; either the autoexecute file contents or the hard-coded default is chosen.

There are two possible hard-coded default devicefile specifications. One hard-coded default devicefile specification is /vmunix. The other hard-coded default devicefile specification is /stand/vmunix.

If you have a LVM system where the boot volume and the root volume are on different logical volumes, the kernel would be /vmunix. This is because the boot volume will be mounted under /stand when the system is up.

For all other configurations, the kernel would be /stand/vmunix.

The search order for the hard-coded defaults is /stand/vmunix and then /vmunix.

# boot Operation

The boot operation loads an object file from an HP-UX file system or raw device as specified by the optional devicefile. It then transfers control to the loaded image.

Any missing components in a specified devicefile are supplied with a default. For example, a devicefile of vmunix.new would actually yield:

```
disc(8.0.0.0)/vmunix.new
```

and a devicefile of (8.0.1)/stand/vmunix, for booting from the disk at HP-IB address 1, would yield

```
disc(8.0.1.0)/stand/vmunix
```

Regardless of how incomplete the specified devicefile may be, boot announces the complete devicefile specification used to find the object file. Along with this information, boot gives the sizes of the TEXT, DATA, and BSS segments and the entry offset of the loaded image, before transferring control to it.

The boot operation accepts several options. Note that boot options must be specified positionally as shown in the syntax statement in the