Use the lsattr command to list the attributes of files in a directory. By default, most files have no attributes set. You can use the chattr command to change the attributes of one or more files. To use this command, determine the code letter for the attributes you want to add or remove from a file. Use a plus sign (+) or minus sign (-), respectively, to add or remove those attributes. To assign the entire set of attributes for a file, use an equals sign. (The use of (+), (-), and (=) for chattr is very similar to their use as part of the chmod command.) You can add the -R option to make your action recursive to the contents of all subdirectories in the named directory if you are setting attributes for multiple files. The possible attribute values are listed in Table 10-2. Note carefully which are supported and which are not yet supported.

# Table 10-2 File Attributes in Linux

| File attribute code letter | Description |
|---|---|
| A | Do not update the atime field of a file's inode when the file is accessed; this reduces the disk activity on laptops |
| a | The file can only be appended to—no part of the file can be overwritten; only root can set this attribute on a file |
| c | The file is automatically compressed by the kernel before being written to disk (this attribute is not yet supported and has no effect) |
| D | Used for directories; write changes to files in this directory immediately instead of waiting for the disk cache to fill up; this reduces the efficiency of disk operations but also reduces the chance that a change is not written to disk in case of a system failure |
| d | Skip this file when using certain commands to back up the system |
| E | Indicates that a compression error has occurred. This attribute cannot be changed with chattr, but is displayed by lsattr. It is used by developers working on kernel compression features. |
| I | Indicates that a directory has been indexed in a particular way (using hashed trees); this attribute may not be set or reset using chattr, but is displayed by lsattr |
| i | The file is immutable. It cannot be modified, deleted, appended to, or renamed. No link can be created to this file. Only root can set or clear this attribute. |
| j | Use journaling for the file. If you are using ext3, all files use journaling by default, so this attribute is not needed. Only root can set or clear this attribute. |
| s | Safe delete this file; when the file is deleted, its contents are all written as zeros, rather than simply marking its space as free |
| S | Write changes to this file immediately to disk; the equivalent for a file of the D attribute on a directory |
| T | A special purpose directory attribute used by the Orlov block allocator algorithm |