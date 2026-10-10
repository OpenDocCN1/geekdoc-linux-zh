This command joins a disk drive to a specific path.

# Syntax

```
```
join [drive: drivepath]
join drive: /d
```
```

# Comments

With the join command, you don't need to give physical drives separate drive letters. Instead, you can refer to all the directories on a specific drive with one path. If the path existed before you gave the join command, you can use it while the join is in effect. But note, you cannot join a drive if it is being used by another process.

If the path does not exist, DOS tries to make a directory with that path. After you give the join command, the first drive name becomes invalid; and if you try to use it, DOS displays the “invalid drive” error message.

# Examples

You can join a drive only with a root-level directory, such as:

```
```join d: c:\sales```
```

To reverse join, type:

```
```join drive: /d```
```

# Keyb

Keyb loads a keyboard program.

**Syntax:**

```
```
keyb [xx[, yyy,[drive: [path]filename]]]
```
```

Where:

+   - xx is a two-letter country code.
+   - yyy is the code page that defines the character set.
+   - filename is the name of the keyboard definition file.

# Comments

Here, xx is one of the following two-letter codes:

us      United States (default)

fr      France

gr      Germany

it      Italy