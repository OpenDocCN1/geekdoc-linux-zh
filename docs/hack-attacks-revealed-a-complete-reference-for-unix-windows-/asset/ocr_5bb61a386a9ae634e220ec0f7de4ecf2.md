```
set hello=c:\letter
```

# Share

Share installs file sharing and locking.

**Syntax:**

```
share  [/:space] [/L:locks]
```

**Comments**

You can see the share command only when networking is active. If you want to install shared files, you can include the share command in your *autoexec.bat* file.

The share command accepts the following switches:

+   * /I:space  Allocates file space (in bytes) for the DOS storage area used to record file-sharing information. The default value is 2048. Note that each open file requires enough space for the length of the full filename, plus 11 bytes, since an average pathname is 20 bytes in length.
+   * /L:locks  Allocates the number of locks you want to allow. The default value is 20.

**Example**

The following example loads file sharing, and uses the default values for the /f and /L switches:

```
share
```

# Sort

Sort reads input, sorts the data, then writes the sorted data to your screen, to a file, or to another device.

**Syntax**

```
[source]  |  sort  [ /r ] [ /+ n ]
```

or

```
sort  [ /r ] [ /+ n ]  source
```

Where source is a filename or command.

**Comment**

The sort command is a filter program that lets you alphabetize a file according to the character in a certain column. The sort program uses the collating sequence table, based on the country code and code page settings.

The pipe (|) and less-than (<) redirection symbols direct data through the sort utility from source. For example, you may use the dir command or a filename as a source. You may use the more command or a filename as a destination.