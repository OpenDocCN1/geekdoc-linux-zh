
# COMMANDS

Interactive commands for more are based on vi(1). Some commands may be preceded by a decimal number, called k in the descriptions below. In the following descriptions, ^X means Ctrl-X.

- h or ?
  Help: display a summary of these commands. If you forget all the other commands, remember this one.
- SPACE
  Display next k lines of text. Defaults to current screen size.
- z
  Display next k lines of text. Defaults to current screen size. Argument becomes new default.
- RETURN
  Display next k lines of text. Defaults to 1. Argument becomes new default.
- d or ^D
  Scroll k lines. Default is current scroll size, initially 11. Argument becomes new default.
- q or Q or INTERRUPT
  Exit.
- s
  Skip forward k lines of text. Defaults to 1.
- F
  Skip forward k screenfuls of text. Defaults to 1.
- B or ^B
  Skip backwards k screenfuls of text. Defaults to 1.
- '
  Go to place where previous search started.
- =
  Display current line number.
- /pattern
  Search for kth occurrence of regular expression. Defaults to 1.
- N
  Search for kth occurrence of last re. Defaults to 1.
- !<cmd> or :!<cmd>
  Execute <cmd> in a subshell
- V
  Start up /usr/bin/vi at current line
- ^L
  Redraw screen
- :n
  Go to *kth* next file. Defaults to 1.
- :p
  Go to *kth* previous file. Defaults to 1.
- :f
  Display current file name and line number
- .
  Repeat previous command

# ENVIRONMENT

**more** utilizes the following environment variables, if they exist:

- MORE
  This variable may be set with favored options to **more**.
- SHELL
  Current shell in use (normally set by the shell at login time).
- TERM
  Specifies terminal type, used by more to get the terminal characteristics necessary to manipulate the screen.

# SEE ALSO

vi(1) less(1)

# AUTHORS

Eric Shienbrood, UC Berkeley.
Modified by Geoff Peck, UCB to add underlining, single spacing.
Modified by John Fodero, UCB to add -c and MORE environment variable.

# HISTORY

The **more** command appeared in 3.0BSD. This man page documents **more** version 5.19 (Berkeley 6/29/88), which is currently in use in the Linux community. Documentation was produced using several other versions of the man page, and extensive inspection of the source code.

# MTOOLS.1(3)

# NAME

**mtools** Utilities to access DOS disks in Unix.

# INTRODUCTION

Mtools is a public domain collection of tools to allow Unix systems to manipulate MS-DOS files: read, write, and move around files on an MS-DOS filesystem (typically a floppy disk). Where reasonable, each program attempts to emulate the MS-DOS equivalent command. However, unnecessary restrictions and oddities of DOS are not emulated. For instance, it is possible to move subdirectories from one subdirectory to another.

# COMMON FEATURES OF ALL MTOOLS COMMANDS

## OPTIONS AND FILENAMES

MS-DOS filenames are composed of a drive letter followed by a colon, a subdirectory, and a filename. Only the filename part is mandatory, the drive letter and the subdirectory are optional. Filenames without a drive letter refer to Unix files. Subdirectory names can use either the / or ` separator. The use of the ` separator or wildcards requires the names to be enclosed in quotes to protect them from the shell. However, wildcards in Unix filenames should not be enclosed in quotes, because here we *want* the shell to expand them. The regular expression “pattern matching” routines follow the Unix-style rules. For example, * matches all MS-DOS files in lieu of * . The archive, hidden, read-only and system attribute bits are ignored during pattern matching.

All options use the - (minus) as their first character, not / as you'd expect in MS-DOS.

Most mtools commands allow multiple filename parameters, which doesn't follow MS-DOS conventions, but which is more user-friendly.

Most mtools commands allow options that instruct them how to handle file name clashes. See section name clashes, for more details on these. All commands accept the -V flags which print the version, and most accept the -v flag, which switches on verbose mode. In verbose mode, these commands print out the name of the MS-DOS files upon which they act, unless stated otherwise. See section “Commands,” for a description of the options which are specific to each command.

## DRIVE LETTERS

The meaning of the drive letters depends on the target architectures. However, on most target architectures, drive A is the first floppy drive, drive B is the second floppy drive (if available), drive J is a Jaz drive (if available), and drive Z is a Zip drive (if available). On those systems where the device name is derived from the SCSI id, the Jaz drive is assumed to be at SCSI target 4, and the Zip at SCSI target 5 (factory default settings). On Linux, both drives are assumed to be the second drive on the SCSI bus (/dev/sdb). The default settings can be changed using a configuration file (see section on Configuration).

**CURRENT WORKING DIRECTORY**
The mcd command (mcd) is used to establish the device and the current working directory (relative to the MS-DOS filesystem), otherwise the default is assumed to be A:\ . However, unlike MS-DOS, there is only one working directory for all drives, and not one per drive.

**VFAT-STYLE LONG FILE NAMES**
This version of mtools supports VFAT style long filenames. If a Unix filename is too long to fit in a short DOS name, it is stored as a VFAT long name, and a companion short name is generated. This short name is what you see when you examine the disk with a pre-7 version of DOS. The following table shows some examples of short names:

| Long name | MS-DOS name | Reason for the change |
| --- | --- | --- |
| thisisatest | THISIS~1 | Filename too long |
| alain.knaff | ALAIN~1.KNA | Extension too long |
| prn.txt | PRN~1.TXT | PRN is a device name |
| .abc | ABC~1 | Null filename |
| hot+cold | HOT_CO~1 | Illegal character |

As you see, the following transformations happen to derive a short name:

- Illegal characters are replaced by underscores. The illegal characters are ;:+[ ] ' </\?>.
- Extra dots, which cannot be interpreted as a main name/extension separator are removed
- A `~n` number is generated,
- The name is shortened so as to fit in the 8+3 limitation

The initial Unix-style file name (whether long or short) is also called the primary name, and the derived short name is also called the secondary name.

## 716 Appendix A

Example:

```
mcopy /etc/motd a:RealllylongNAME
```

Mtools creates a VFAT entry for Realllylongname, and uses REALLYLO as a short name. Realllylongname is the primary name, and REALLYLO is the secondary name.

```
mcopy /etc/motd a:motd
```

Motd fits into the DOS filename limits. Mtools doesn't need to derive another name. Motd is the primary name, and there is no secondary name. In a nutshell: The primary name is the long name, if one exists, or the short name if there is no long name.

Although VFAT is much more flexible than FAT, there are still names that are not acceptable, even in VFAT. There are still some illegal characters left (*\^</?:|) , and device names are still reserved.

| Unix name | Long name | Reason for the change |
|---|---|---|
| prn | prn-1 | PRN is a device name. |
| ab:c | ab_c-1 | Illegal character. |

As you see, the following transformations happen if a long name is illegal:

- Illegal characters are replaces by underscores.
- A -n number is generated.

## NAME CLASHES

When writing a file to disk, its long name (primary name) or short name may collide with an already existing file or directory. This may happen for all commands which create new directory entries, such as mcopy, mmd, mren, mmv, mwrit e, and mread. When a name clash happens, mtools asks you what it should do. It offers several choices:

- overwrite
  Overwrites the existing file. It is not possible to overwrite a directory with a file.
- rename
  Renames the newly created file. Mtools prompts for the new filename
- autorename
  Renames the newly created file. Mtools chooses a name by itself, without prompting.
- skip
  Gives up on this file, and moves on to the next (if any).

To choose one of these actions, type its first letter at the prompt. If you use a lowercase letter, the action only applies for this file only, if you use
