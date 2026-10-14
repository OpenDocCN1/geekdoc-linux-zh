```
# cfsmgr -a server=molari /fafrak
```

You can add the "-x" switch to relocate the underlying disk storage to keep it served locally as well. This is only useful if the devices are not Direct-Access I/O (DAIO) capable. See chapter 15 for more information on DAIO devices.

Let's verify that the relocation was successful using the cfsmgr command.

```
# cfsmgr /fafrak

Domain or filesystem name = /fafrak
Server Name = molari
Server Status : OK
```

# NOTE:

Since there is a CFS server per AdvFS domain, relocating a file system that is a fileset of a multi-fileset domain will cause all filesets in the domain to be relocated. For example, if you recall from examples earlier in this chapter, the tcrhb domain contains two filesets: fafrak and lola. If the tcrhb#lola fileset had been mounted at the time we had done the relocation of the /fafrak file system, then the /lola file system would also have been relocated.

```
# mount tcrhb#lola /lola
```

```
# cfs | grep -E "^CFS|^-|tcrhb*"
CFS Server    Mount Point    File System    FS Type
------------  -------------- --------------- --------
molari        /fafrak         tcrhb#fafrak    AdvFS
molari        /lola           tcrhb#lola      AdvFS
```

```
# cfsmgr -a server=sheridan /fafrak
```

```
# cfs | grep -E "^CFS|^-|tcrhb*"
CFS Server    Mount Point    File System    FS Type
------------  -------------- --------------- --------
sheridan       /fafrak         tcrhb#fafrak    AdvFS
sheridan       /lola           tcrhb#lola      AdvFS
```