+   4. `~/..mtoolsrc`

+   5. `$MTOOLSRC' (file pointed by the MTOOLSRC environmental variable)

Options described in the later files override those described in the earlier files. Drives defined in earlier files persist if they are not overriden in the later files. For instance, drives A and B may be defined in `'/usr/local/etc/mtools.conf'` and drives C and D may be defined in `'/..mtoolsrc'`. However, if `'/..mtoolsrc'` also defines drive A, this new description would override the description of drive A in `'/usr/local/etc/mtools.conf'` instead of adding to it. If you want to add a new description to a drive already described in an earlier file, you need to use either the `+drive` or `drive+` keyword.

# BACKWARDS COMPATIBILITY WITH OLD CONFIGURATION FILE SYNTAX

The syntax described herein is new for version mtools-3.0. The old line-oriented syntax is still supported. Each line beginning with a single letter is considered to be a drive description using the old syntax. Old style and new style drive sections may be mixed within the same configuration file, in order to make upgrading easier. Support for the old syntax will be phased out eventually, and in order to discourage its use, I purposely omit its description here.

# COMMAND LIST

This section describes the available mtools commands, and the command line parameters that each of them accepts. Options that are common to all mtools commands are not described here, see 'arguments' for a description of those.

# MATTRIB

Mattrib is used to change MS-DOS file attribute flags. It has the following syntax:

```
mattrib [-a][+a] [-h][+h] [-r][+r] [-s][+s] msdosfile_
            [ msdosfiles ... ]
```