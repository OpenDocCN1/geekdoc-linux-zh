
## fdisk

The `fdisk` command displays a series of menus to help you partition your hard disk for DOS. With `fdisk`, you can:

- Create a primary DOS partition.
- Create an extended DOS partition.
- Change the active partition.
- Delete a DOS partition.
- Display partition data.
- Select the next fixed disk drive for partitioning on a system with multiple fixed disks.

## Find

`Find` searches for a specific string of text in a file or files.

### Syntax

```
find [/v] [/c] [/n] "string" [[drive:] [pathname] ... ]
```

Where “string” is a group of characters for which you want to seek.

### Comments

String must be enclosed in quotation marks. Uppercase characters in `string` will not match lowercase characters you may be searching for.

The `find` command accepts the following switches:

- `/v` Displays all lines not containing the specified string.
- `/c` Displays only the number of lines that contain a match in each of the files.
- `/n` Precedes each line with its relative line number in the file.

### Example

The following displays all lines from the file `pencil.ad` that contains the string “Pencil Sharpener”:

```
find "Pencil Sharpener" pencil.ad
```

## Format

This command formats the disk in the specified drive to accept files.

### Syntax

```
format drive:[/1][/4][/8][/n:xx][/t:yy] [/v][/s]
format drive:[/1][/b][/n:xx][/t:yy]
```

### Comments

You must use `format` on all “new” disks before DOS can use them. Note that formatting destroys any previously existing data on a disk.

The `format` command accepts the following switches:

- **/1** Formats a single side of the floppy disk.
- **/4** Formats four sectors per track.
- **/8** Formats eight sectors per track.
- **/b** Formats the disk, leaving ample space to copy an operating system.
- **/s** Copies the operating system files to the newly formatted disk.
- **/t:yy** Specifies the number of tracks on the disk. This switch formats 3-1/2 inch floppy disk to the number of tracks specified. For 720 KB disks and 1.44 MB disks, this value is 80 (/t:80).
- **/n:xx** Specifies the number of sectors per track. This switch formats a 3-1/2 inch disk to the number of sectors specified. For 720 KB disks, this value is 9 (/n:9).
- **/v** Causes `format` to prompt you for a volume label for the disk you are formatting. A volume label identifies the disk and can be up to 11 characters in length.

### Example

To format a floppy disk in drive A, and copy the operating system to it, type:

```
format a: /s
```

## Graftabl

`Graftabl` enables an extended character set to be displayed when using display adapters in graphics mode.

### Syntax

```
graftabl [xxx]
graftabl /status
```

Where `xxx` is a code page identification number.

### Comments

Valid code pages (`xxx`) include:

- 437 United States (default)
- 850 Multilingual
- 860 Portuguese
- 863 French-Canadian
- 865 Nordic

If you type the `graftabl` command followed by the `/status` switch, DOS displays the active character set.

### Example

To load a table of graphics characters into memory, type:

```
graftabl
```

## Graphics

`Graphics` lets you print a graphics display screen on a printer when you are using a color or graphics monitor adapter.

### Syntax

```
graphics [printer] [/b] [/p=port] [/r] [/lcd]
```

Where `printer` is one of the following:

- **color1** Prints on an IBM Personal Computer Color Printer with black ribbon.
- **color4** Prints on an IBM Personal Computer Color Printer with red, green, blue, and black (RGB) ribbon.
- **color8** Prints on an IBM Personal Computer ColorPrinter with cyan, magenta, yellow, and black (CMY) ribbon.
- **compact** Prints on an IBM Personal Computer Compact printer.
- **graphics** Prints on an IBM Personal Graphics Printer or IBM Pro printer.

### Comments

If you do not specify the printer option, `graphics` defaults to the graphics printer type.

The `graphics` command accepts the following switches:

- **/b** Prints the background in color. This option is valid for `color4` and `color8` printers.
- **/p=port** Sets the parallel printer port to which `graphics` sends its output when you press the Shift-Print Screen key combination. The port may be set to 1, 2, or 3. The default is 1.
- **/r** Prints black and white.
- **/lcd** Prints from the LCD (liquid crystal display) on the IBM PC portable computer.

### Example

To print a graphics screen on your printer, type:

```
graphics
```

## Join

This command joins a disk drive to a specific path.

### Syntax

```
join [drive: drivepath]
join drive: /d
```

### Comments

With the `join` command, you don't need to give physical drives separate drive letters. Instead, you can refer to all the directories on a specific drive with one path. If the path existed before you gave the `join` command, you can use it while the join is in effect. But note, you cannot join a drive if it is being used by another process.

If the path does not exist, DOS tries to make a directory with that path. After you give the `join` command, the first drive name becomes invalid; and if you try to use it, DOS displays the “invalid drive” error message.

### Examples

You can join a drive only with a root-level directory, such as:

```
join d: c:\sales
```

To reverse join, type:

```
join drive: /d
```

## Keyb

`Keyb` loads a keyboard program.

### Syntax

```
keyb [xx[, yyy,[drive: [path]filename]]]
```

Where:

- xx is a two-letter country code.
- yyy is the code page that defines the character set.
- filename is the name of the keyboard definition file.

### Comments

Here, `xx` is one of the following two-letter codes:

- us United States (default)
- fr France
- gr Germany
- it Italy
- sp Spain
- uk United Kingdom
- po Portugal
- sg Swiss-German
- sf Swiss-French
- df Denmark
- be Belgium
- nl Netherlands
- no Norway
- la Latin America
- sv Sweden
- su Finland

### Note

You can include the appropriate `keyb` command in your `autoexec.bat` file so that you won’t have to type it each time you start DOS.

### Example

To use a German keyboard, type:

```
keyb gr
```

## Label

`Label` creates, changes, or deletes the volume label on a disk.

### Syntax

```
label [drive:][label]
```

Where `label` is the new volume label, up to 11 characters.

### Comments

A volume label is a name you can specify for a disk. DOS displays the volume label of a disk as a part of its directory listing, to show you which disk you are using.

### Notes

You can use the DOS `dir` or `vol` command to determine whether the disk already has a volume label. `Label` doesn't work on drives involved with `subst` or `join` commands.

Do not use any of the following characters in a volume label:

? / \ . , ; : + = [ ] ( ) & ^

### Example

To label a disk in drive A that contains a report for Sales, type:

```
label a:reportSales
```

## Mkdir (MD)

`Mkdir` (`MD`) makes a new directory.

### Syntax

```
mkdir [drive:]path
md [drive:]path
```

### Comment

The `mkdir` command lets you create a multilevel directory structure.

### Example

If you want to create a directory to keep all your papers, type:

```
md \papers
```

## Mode

`Mode` sets operation modes for devices.

### Syntax

Parallel printer mode:

```
mode LPTn[:] [chars] [, [lines] [, p]]
```

Asynchronous communications mode:

```
mode COMn[:] baud [, parity [, databits [, stopbits [, p]]]]
```

Redirecting parallel printer output:

```
mode LPTn[:] = COMn[:]
```

Display modes:

```
mode display
mode [display], shift[[,t]]
```

Device code page modes:

```
mode device codepage prepare =[[,yyy]][drive:][path]filename]
mode device codepage select = yyy
mode device codepage refresh
mode device codepage [/status]
```

### Comments

The `mode` command prepares DOS for communications with devices such as parallel and serial printers, modems, and consoles. It also prepares parallel printers and consoles for code page switching. You can also use the `mode` command to redirect output.

### Parallel Printer Modes

For parallel modes, you can use `PRN` and `LPT1` interchangeably. You can use the following options with the `mode` command to set parameters for a parallel printer:

- n Specifies the printer number: 1, 2 or 3.
- chars Specifies characters per line: 80 or 132.
- lines Specifies vertical spacing, lines per inch: 6 or 8.
- p Specifies that `mode` tries continuously to send output to the printer if a time-out error occurs. This option causes part of the `mode` program to remain resident in memory.

The default settings are `LPT1`, 80 characters per line, and 6 lines per inch.

You can break out of a time-out loop by pressing Control-Break.

### Asynchronous (Serial) Communication Modes

You can use the following options with the `mode` command to set the following parameters for serial ports:

- m Specifies the asynchronous communications (`COM`) port number: 1, 2, 3, or 4.
- baud Specifies the first two digits of the transmission rate: 110, 150, 300, 600, 1200, 2400, 4800, 9600, or 19,200.
- parity Specifies the parity: N (none), O (odd), or E (even). The default is E.
- databits Specifies the number of data bits: 7 or 8. The default is 7.
- stopbits Specifies the number of stop bits: 1 or 2. If the baud is 110, the default is 2; otherwise, the default is 1.
- p Specifies that `mode` is using the `COM` port for a serial printer and continuously retrying if time-out errors occur. This option causes part of the `mode` program to remain resident in memory. The default settings are `COM1`, even parity, and 7 data bits.

### Display Modes
