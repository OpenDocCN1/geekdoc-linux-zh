producing the package. The data in this example is White Socks Software, Inc.. Therefore, RPM will store White Socks Software, Inc. as the vendor of the package.

Note also that spacing between the tag, the colon, and the data is unimportant. Given this, and the case insensitivity of the tag, each of the following lines is equivalent to the previous example:

VendOr : White Socks Software, Inc. 

vendor:White Socks Software, Inc. 

VENDOR : White Socks Software, Inc.

The bottom line is that you can make tag lines as neat or as ugly as you like—RPM won't mind either way. Note, however, that the tag's data might need to be formatted in a particular fashion. If there are any such restrictions, we'll mention them. The following sections group together tags of similar functions for easier reference, starting with the tags used to create the package name.

# 13.2.1. Package Naming Tags

The following tags are used by RPM to produce the package's final name. Since the name is always in this format:

```
<name>-<version>-<release>
```

it's only natural that the three tags are known as name, version, and release.

# 13.2.1.1. The name Tag

The name tag is used to define the name of the software being packaged. In most (if not all) cases, the name used for a package should be identical in spelling and case to the software being packaged. The name cannot contain any whitespace: If it does, RPM will only use the first part of the name (up to the first space). Therefore, if the name of the software being packaged is cdplayer, the name tag should be something like this:

```
Name: cdplayer
```

# 13.2.1.2. The version Tag

The version tag defines the version of the software being packaged. The version specified should be as close as possible to the format of the original software's version. In most cases, there should be no problem specifying the version just as the software's original developer did. However, there is a restriction: There can be no dashes in the version. If you forget, RPM will remind you:

```
# rpm -ba cdplayer-1.0.spec
Package: cdplayer
Illegal '-' char in version: 1.0-a
```