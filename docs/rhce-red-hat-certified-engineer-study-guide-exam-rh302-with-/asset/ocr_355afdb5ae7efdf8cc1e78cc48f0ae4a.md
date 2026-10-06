# Unix Command Facilities

specifying the partition (for example, /dev/hdb2) that you want to check. To specify that the check should include a test for bad blocks and errors should be repaired automatically, add the -c and -p options (respectively) in the following command:

```
e2fsck -f -c -p /dev/hdb2
```

This section surveys important Unix command facilities, including stream redirection, regular expressions, and shell scripts. Several books have been written on Unix command facilities, so it's not possible to cover every detail here. This section focuses on the most useful aspects of these facilities. If you're unfamiliar with the material in this section, you should consult the reference given at the end of this chapter.

# Using Stream Redirection

Every Unix process has the following three standard streams:

+   - Standard Input Command input
- Standard Output Command output
- Standard Error Error messages

Table 3.8 summarizes stream redirection operators, which let you redirect these input and output streams. For example, the command

```
ls -l > filelist
```

sends the output of the ls command to the file filelist.

# TABLE 3.8 Important Redirection Operators

| Operator | Meaning |
|---|---|
| < file | Take standard input from file. |
| > file | Write standard output to file. |
| >> file | Append standard output to file. |