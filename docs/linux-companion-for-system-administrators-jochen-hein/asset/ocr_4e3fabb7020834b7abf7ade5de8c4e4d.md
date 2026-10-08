# 4.13 Keyboard mapping

Under Linux, keyboard mapping can be adapted to personal requirements in a very flexible way. This applies both for working at the console and working under X. This section only deals with console keyboard mapping; information on remapping keys under X can be found in Section 6.3.3.

Keyboard mapping for the Linux console is carried out by means of the loadkeys program. If a file name is specified as a parameter (for example, loadkeys de-latin1.map), the file is read and the keyboard mapping is modified accordingly. However, the loadkeys program can also read its input from the standard input. This is useful if the keyboard mapping is stored in compressed form (for example, on a boot or emergency floppy disk). Then, it could look like:

```
zcat /etc/keytables/de-latin1.map.gz | loadkeys
```

The kbd-0.95.tar.gz package, can be obtained anywhere an up-to-date Linux kernel is available, includes a series of keyboard tables. These keyboard tables are installed in the directory /usr/lib/kbd/keytables.

+   - de-latin1-nodeadekeys.map: In contrast to the keyboard mapping de-latin1.map, here the accent keys are not defined as dead-keys. Thus, these keys do not act as modifiers, as under de-latin1.map, but output the corresponding character directly.

The keyboard mapping is initially loaded at start-up by means of the loadkeys program. Users can, however, use the loadkeys programs to remap the keyboard according to their requirements. This can also have the effect of putting the keyboard into an unusable state. The file de-latin1.map can serve as an example of how to modify the keyboard mapping.

| Additional Information and Sources |
|---| Man pages: loadkeys(1), dumpkeys(1), keytables(5), showkey(1), and several others |
| server: ftp.funet.fi |
| ftp path: /pub/Linux/PEOPLE/Linus/ |
| Package: kbd-0.95.tar.gz |
| Size: about 398 Kbytes |