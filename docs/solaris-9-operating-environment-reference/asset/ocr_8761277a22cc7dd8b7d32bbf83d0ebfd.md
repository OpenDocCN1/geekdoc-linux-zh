# 700

# /usr/bin/ln

-n If the link is an existing file, do not overwrite the contents of the file. The -f option overrides this option. This behavior is the default for /usr/xpg4/bin/ln and is silently ignored.

# Operands

source-file

A path name of a file to be linked. This file can be either a regular or special file. If you specify the -s option, source-filecan also be a directory. 

target

The path name of the new directory entry to be created or of an existing directory in which the new directory entries are to be created.

# Usage

largefile(5) for the description of the behavior of ln when encountering files greater than equal to 2 Gbytes (2**31 bytes).

# Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of ln: LC_TYPE, LC_MESSAGES, and NLPATH.

# Exit Status

0 All the specified files were linked successfully.

>0 An error occurred.

# Attributes

attributes(5) for descriptions of the following attributes:

# /usr/bin/ln

Attribute Type Attribute Value

Availability CSI SUNWosu Enabled

# /usr/xpg4/bin/ln

Attribute Type Attribute Value

Availability CSI SUNWxcu4 Enabled

# See Also

chmod(1), ls(1), stat(2), attributes(5), environ(5), largefile(5), XPG4(5)