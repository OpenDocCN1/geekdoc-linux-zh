not established for the volume group, it is not activated. However, belive it or not, you can force it to vary online with the -f switch to the varyong command.

```
```
# varyong <VGname> # Vary a volume group online
# varyong -f <VGname> # Force vary on a volume group
```
```

You can take a volume group offline using the varyofvg command or via SMIT. Note that all access to logical volumes in the volume group must be terminated. Any fileystems located in the volume group must be unmounted, and any paging space must not be active.

```
```
# varyofvg <VGname>
# smit varyofvg
```
```

To remove or replace physical volumes in a volume group for maintenance purposes, use SMIT or the chpv command.

```
```
# reducevg <VGname> <PVname> # Remove the disk from VG
# rmdev -dl hdisk<x> # Remove the hdisk definition
```
```

Replace the disk...

```
```
# cfgrw -v # Let the system discover the disk
# lsv # Find the newly found disk and write down the hdisk #
# chdev -l hdisk<x> -a pv=yes # Create a PVID for the new hdisk
# extendvg <VGname> <hdisk<x>> # Add the new disk into the volume group
```
```

> NOTE When you remove all of the physical volumes from a volume group, the volume group is deleted from the system (reducevg command).

An entire volume group may be moved as a unit from one system to another. When the volume group is exported, all references to it are removed from the ODM. When the volume group is imported on the new system, all device table, special file, and /etc/fileystem entries are added automatically to the ODM. You can export and import a volume group on the same system to resynchronize the VGDA and ODM information.

```
```
# exportvg <VGname>
# importvg <VGname> <PVname>
```
```

# Root Volume Group—rootvg

A special VG called rootvg is used by AIX for the operating system’s root fileystems and the default paging areas. It’s a good idea to use separate volume groups for user and local application fileystems. This way, you can export and import these volume groups between systems while the system is active.