# **Comments**

The copy command accepts the following switches:

+   /v        Causes DOS to verify that the sectors written on the target disk are recorded properly.

+   /a        Lets you copy ASCII files. This switch applies to the filename preceding it and to all remaining filenames in the command, until copy encounters another /a or /b switch.

+   /b        Lets you copy binary files. This switch applies to the filename preceding it and to all remaining filenames in the command, until copy encounters another /a or /b switch. This switch tells the command processor to read the number of bytes specified by the file size in the directory.

# **Examples**

To copy a file called *letter.doc* from your working drive directory to a directory on drive C called *docs*, type:

```
```
copy letter.doc c:\docs
```
```

You can also combine several files into one by:

```
```
copy *.doc combine.doc
```
```

This takes all the files with an extension .doc and combines them into one file named *combine.doc*.

# *Ctty*

Ctty lets you change the device from which you issue commands.

# **Syntax**

```
```
ctty device
```
```

Where *device* specifies the device from which you are giving commands to DOS.

# **Comments**

Ctty is useful if you want to change the device on which you are working. The letters tty represent your terminal—that is, your computer screen and keyboard.

# **Examples**

The following command moves all command I/O from the current device (the console) to an AUX port, such as another terminal:

```
```
ctty aux
```
```

The next command moves I/O back to the console screen and keyboard:

```
```
ctty con
```
```