```
```text
. . .tar/bin/tar -c -f %s:T_REG:T_DIR:O_TAR:TAR
```
```

The following sections describe the fields in a conversion entry.

# Types

You must use the types field of the ftpconversions file to tell the server what types of files the conversion rules apply to. Separate the file type entries with the (:) character, and give each type a value of T_REG, T_ASCII, and T_DIR.

T_REG signifies a regular file, T_ASCII an ASCII file, and T_DIR a directory. A typical entry is T_REG | T_ASCII, which signifies a regular ASCII file.

# Options

The options field informs the server what action is being done to the file. Similar to the types file, options are separated by the (:) character. Here are the valid ranges you can assign to items in the options field:

+   - O_COMPRESS to compress the file
+   - O_UNCOMPRESS to uncompress the file
+   - O_TAR to tar the file

An example of this field is O_COMPRESS | O_TAR, where files are both compressed and Tared.

# Description

The description field allows an administrator to quickly understand what the rule is doing. This field does not have any syntax restriction, although it is usually a one-word entry—such as TAR, TAR+COMPRESS, or UNCOMPRESS—which is enough to get the concept across.

# An Example of Conversions in Action

Crafting complex conversion entries is a task perhaps best left to the Linux/Unix expert, but the sample ftpconversions file included with wu-ftpd provides more than enough examples for the average administrator. Building your own simple conversion entry is not really too difficult, so let’s examine and decode an example:

```
```text
:Z:  :  :/bin/compress -d -c %s:T_REG:T_ASCII:O_UNCOMPRESS:UNCOMPRESS
```
```

In this example, the strip prefix (field 1) is null because it is not yet implemented, so this rule does not apply to strip prefixes. The second field of this rule contains the .Z postfix; therefore it deals with files that have been compressed with the compress utility. The rule does not address the add-on prefix or postfix, so fields 3 and 4 are null. Field 5, the external command field, tells the server to run the compress utility to decompress all files that have the .Z extension, as the -d parameter signifies. The -c option tells compress to write the output of the compress utility to the standard out, which is the server in this case. The %s is the name of the file against which the rule was applied. Field 6 specifies that this file is a regular file in ASCII format. Field 7, the options field, tells the server that this command uncompresses the file. Finally, the last field is a comment that gives the admin-