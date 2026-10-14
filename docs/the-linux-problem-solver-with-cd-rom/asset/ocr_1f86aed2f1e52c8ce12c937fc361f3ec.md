The first argument is the printer's primary name, the second a description, the third a list of aliases, and the fourth its physical location. This information makes up the first field of a printcap entry.

Because you can attach printers locally to different machines, printcaps vary across the network. For example, if the host mikado had an inkjet attached to its parallel port, its /etc/printcap would contain the spool directory and filter information required to send files to that printer. Any machine on the network other than mikado would need a printcap with an entry saying this printer is on mikado. That's what the fourth argument in the printer-list.m4 file is about—it's the machine that this printer is attached to. If the fourth argument matches the definition of this_host, you get output tailored for a local printer; otherwise it is a remote printer entry.

To add a new printcap variation, as in the local printer on the host mikado above, you'd make a new file called mikado.m4:

```
define(this_host,mikado)dnl
include(common.m4)dnl
include(lprng-printcap.m4)dnl
include(printer-list.m4)dnl
```

After that, the command

```
$ m4 mikado.m4 > mikado
```

would create a new printcap just for mikado. However, the Makefile offers a way to make everything at once; take a look at the description below.

# Macro Definitions

The printer list is a set of macro invocations. For an LPRng printcap, the macro definitions are in lprng-printcap.m4 and they look like generalized printcap definitions. Each kind of printer (or printer configuration) has a different macro definition, and most are very similar (compare HPPSD with HP4SI). Adding a new kind of printer is typically only a matter of copying a similar definition, then modifying it to suit your needs.

Note, however, that when you add new types of printers, you may also need to do some work in other files. This system of printcap generation is flexible enough to accommodate other kinds of files that require information about your printers. These include printcaps for the original lpd (not LPRng) (done here in lpd-printcap.m4), Netatalk (netatalk-source.m4) and SAMBA (samba-source.m4) configuration files for allowing AppleTalk and SMB access, a script that creates appropriate spool directories (mkdirs.m4), and anything else you can write a macro list for.

If you add a new printer type and use these additional files (samba-source.m4, for example) to generate other files, you'll need to add that type of printer to them. Fortunately, you probably have the hard work behind you