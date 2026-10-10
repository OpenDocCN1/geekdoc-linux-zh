Sh Backspace

# Example

The following command sets a two-line prompt that displays the current date and time:

```
prompt time = $t$_date = $d
```

# Recover

This command recovers a file or disk that contains bad sectors.

# Syntax

```
recover [drive:][path]filename
```

or

```
recover [drive:]
```

# Comments:

If the chkdsk command shows that a sector on your disk is bad, you can use the recover command to recover the entire disk or just the file containing the bad sector. The recover command causes DOS to read the file, sector by sector, and to skip the bad sectors.

# Examples

To recover a disk in drive A, type:

```
recover a:
```

Suppose you have a file named sales.jan that has a few bad sectors. To recover this file, type:

```
recover sales.jan
```

# Ren (Rename)

Rename changes the name of a file.

# Syntax

```
rename [drive:][path]filename1 filename2
ren [drive:][path]filename1 filename2
```

Where: filename1 is the old name, and filename2 is the new name.

# Examples

The following command changes the extension of all filenames ending in .txt to .doc:

```
ren *.txt *.doc
```