# ## Shell Compatibilities

The Solaris 8 operating system employs several shells for use as command interpreters. As discussed earlier, the three primary shells are the Bourne shell (sh), which is used most often by system administrators; the Korn shell (ksh), which is used heavily by developers and advanced users; and the C shell (csh), which is favored by the typical user. There are three freeware shells shipped with Solaris 8: the Bourne Again Shell (bash), the Z Shell (zsh), and the TC Shell (tcsh).

> **NOTE** Only the three primary shells will be described in this section. There may be a brief reference to other shells when necessary.

Certain features are common to the three primary shells. The administrator defines the default shell for the user, but you can change the shell from the command line. The main reasons to change a shell are that one may have more capabilities than another and you may be more familiar with the commands and language in one. Table 17.4 describes some features found in all three of the primary shells.

**TABLE 17.4: COMMON FEATURES OF PRIMARY SHELLS**

| Feature | Bourne | Korn | C |
| :--- | :---: | :---: | :---: |
| Aliases | No | Yes | Yes |
| Command-line editing | No | Yes | Yes |
| History list | No | Yes | Yes |
| Ignore Ctrl+D | No | Yes | Yes |
| Separate from .profile | No | No | Yes |
| Job control or (jsh) | Yes | Yes | Yes |
| Logout file | No | Yes | Yes |
| Overwrite protection | No | Yes | Yes |
| Bourne syntax compatible | Yes | Yes | No |