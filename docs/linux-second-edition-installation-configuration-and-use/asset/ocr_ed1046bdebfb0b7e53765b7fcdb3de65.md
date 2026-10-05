Many useful hints for the adaptation of Linux to foreign languages are contained in the different HOWTO files (for example Chinese, Cyrillic, Danish, Esperanto, Finnish, French, German, Hebrew, Italian, Portuguese, Slovenian, Spanish, and Thai). General information on the HOWTO documents can be found from page 77 onward.

Significantly greater problems need to be solved in Asian countries where characters are coded in two bytes and special forms of input are required. Lack of personal experience, however, I will not discuss these peculiarities.

Thus, there is no central file in which you simply tell the system that you want to use the ISO Latin-1 character set. One program needs a system variable to be set, the third program is persuaded to cooperate via a configuration file, and so on. The same can be said for the support of function keys on the keyboard. Therefore within this section you will find several subsections that describe the configuration of various programs.

A central point for keyboard management is the Loadkeys program. This program loads a table which controls the mapping between keyboard codes and characters. If you are configuring your system for a German keyboard, the setting should be /de-latin1.map. A variation on this is /de-latin1-nodekeys.map. The only difference is that the special characters ',', '.', and '&' can be entered immediately (without a subsequent space). With the following command, you can try any keyboard table you like. (Compressed tables are automatically decompressed).

```
root# loadkeys /usr/lib/kbd/keymaps/1386/type/name.map
```

If you want your keyboard to be loaded automatically at start-up, you must store the setting permanently. Unfortunately, the configuration file has in nearly every distribution (a problem that will arise over and again in the course of this chapter).

In RedHat, the name of the keyboard table must be entered into the file /etc/sysconfig/keyboard:

```
#etc/sysconfig/keyboard (RedHat)
# line split only for reasons of space
KEYBOARD=
"/usr/lib/kbd/keymaps/i386/qw/de-latin1-nodekeys.map.gz"
```

In SuSE, the corresponding file is /etc/rc.config. The specified file is searched for in the subdirectories of /usr/lib/kbd/keymaps.

```
#etc/rc.config (SuSE)
KEYBOARD=de-latin1-nd.map.gz
```

In Debian, the keyboard table is taken from /etc/kbd/default.map. If you wish to modify the keyboard table, you need to copy the required table to that location.

At the moment, loadkeys only applies to the console. Information on keyboard configuration for the X Window System can be found on page 242.