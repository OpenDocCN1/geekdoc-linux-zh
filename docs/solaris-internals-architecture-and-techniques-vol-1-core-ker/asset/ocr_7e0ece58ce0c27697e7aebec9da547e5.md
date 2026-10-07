# File System Framework

dnlc_lookup
find nc's by
hash lookup

freelist rotor

DNLC entries are taken from the first entry with a reference count=1, starting from the end of the chain

![](bbox=[0.265, 0.098, 0.765, 0.452])

nc_hash[]

vnode
dir. vnode
char*
name

struct ncache

Figure 13.7 Solaris 2.4 DNLC

The Solaris 7 DNLC was enhanced to use the kernel memory allocator to allocate a variable length string for the name; this change removed the 31-character limit. In the Solaris 7 DNLC structure, shown below, note that the name field has changed from a static structure to a pointer.

# 13.5.5.3 DNLC Support Functions

Table 13-14 lists the DNLC support functions.

Table 13-14 Solaris 7 DNLC Functions from sys/dnlc.h

| Function | Description |
|---|---|
| dnlc_lookup() | Locates an ncache entry that matches the supplied name and directory vnode pointer. Returns a pointer to the vnode for that entry or returns NULL |
| dnlc_update() | Enters a new ncache entry into the DNLC for the given name and directory vnode pointer. If an entry already exists for the name and directory pointer but the vnode is different, the entry is overwritten. Otherwise, the function returns with no action. |
| dnlc_enter() | Enters a new ncache entry into the DNLC for the given name and directory vnode pointer. If an entry already exists for the name and directory pointer, the function returns with no action. |