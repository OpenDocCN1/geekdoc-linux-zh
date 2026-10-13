The cups options = raw directive means that print jobs are already processed by a service with print processors, such as the CUPS service.

```
load printers = yes
cups options = raw
printcap name = /etc/printcap
```

Alternatively, it's possible to configure a different print server. The following option obtains information from printers configured on older Linux systems:

```
printcap name = lpstat
```

# Filesystem Options

The following section supports the configuration of extended attributes, associated with the Access Control List (ACL) settings for a Microsoft file. With the right options, such attributes can be stored. The comments within the Samba configuration file refer to the Microsoft Disk Operating System (DOS), as shorthand for how permissions and related ACL bits are specified for such shared files. The following would be the default for all shared directories, starting with the following comment:

```
#----------------- Filesystem Options -----------------
```

First, the map archive directive can control whether the DOS file archive attribute is mapped to the local Linux executable bit, if supported by the create mask directive.

```
; map archive = no
```

The map hidden directive can control whether DOS hidden files are mapped to the local Linux executable bit, if supported by the create mask directive.

```
; map hidden = no
```

The map read only directive, also known as map readonly in Samba documentation, as shown is useful for shared mounted media such as DVDs:

```
; map read only = no
```

The map system directive, if set to yes, supports the use of the Linux execute bit for DOS system files:

```
; map system = no
```

Finally, the store dos attributes directive, if active, attempts to store previously configured ACLs of DOS files:

```
;     store dos attributes = yes
```