```
select[[drive1:] [drive2:] [path]  [yyy] [xx]
```

Where *drive1* is the source drive, and *drive2* is the target drive.

# **Comments**

The *select* command lets you install DOS on a new disk along with country-specific information (such as date and time formats and collating sequence) for a selected country. The *select* command does the following:

+   - Formats the target disk.
+   - Creates both the *config.sys* and *autoexec.bat* files on a new disk.
+   - Copies the contents of the source disk, track by track, to the target disk.

The source drive may be either drive A or B. The default source drive is A, and the default target drive is B. You can use the following options with the *select* command:

+   * **yyy**	Specifies the country code.
+   * **xx**	Specifies the keyboard code for the keyboard layout used (see the *keyb* command).

# **Example**

Suppose you want to create a new DOS disk that included the country-specific information and keyboard layout for Germany. With your source disk in drive B and your target disk in drive A, type:

```
select b: a: 049 gr
```

# **Set**

This command sets one string of characters in the environment equal to another string for later use in programs.

# **Syntax**

```
set [string = [string]]
```

# **Comments**

You should use the *set* command only if you want to set values for programs you have written. When DOS recognizes a *set* command, it inserts the given string and its equivalent into a part of memory reserved for the environment. If the string already exists in the environment, it is replaced with the new setting.

If you specify just the first string, *set* removes any previous setting of that string from the environment. Or, if you use the *set* command without options, DOS displays the current environment settings.

# **Example**

The following command sets the string “hello” to c:\letter until you change it with another *set* command: