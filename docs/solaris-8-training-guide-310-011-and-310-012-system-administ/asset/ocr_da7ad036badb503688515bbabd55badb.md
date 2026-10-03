# The Forth Monitor

The Forth Monitor, the default mode in OpenBoot, is an interactive command interpreter that gives you access to an extensive set of functions for hardware and software diagnosis. These functions are available to anyone who has access to the system console.

The Forth Monitor prompt is ok. When you enter the Forth Monitor mode, the following line is displayed:

```
Type help for more information ok
```

On older SPARCstations, if you want to leave the Forth Monitor mode and get into the Restricted Monitor mode, type the following:

```
ok old-mode
```

Old mode is not available on UltraSparc systems.

# GETTING HELP IN OPENBOOT

You can obtain help at any time on the various Forth commands supported in OpenBoot by using the help command. The syntax for using help from the ok prompt is any of the choices listed in Table 2.2.

NOTE When the system is halted, the PROM monitor prompt is displayed. The type of prompt depends on your system type. Older Sun systems, such as the Sun4/nnn series, use the greater-than sign (>) as the PROM prompt. Newer Sun systems use ok as the PROM prompt but support the > prompt. To switch from the > prompt to the ok prompt on newer Sun systems, type n at the > prompt.

# TABLE 2.2

# OpenBoot Help

| Command | Description |
|---|---|
| help | Displays instructions about using the help system, and lists the available help categories. |
| help <category> | Shows help for all commands in the category. Use only the first word of the category description. |
| help <command> | Shows help for the individual command. |

Because of the large number of commands, help is available only for commands that are used frequently.