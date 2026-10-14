The access_mode_options uses the +, -, and = operators to add, remove, or assign permissions to a given group. Combinations separated by commas are allowed. The following example grants the owner of test full access while removing all access from the group owner and the world.

```
`Athena: /home/admin/demo # chmod u=rwx,go-rwx test`
```

# NOTE

If you specify more than one mode option, as is in the preceding example, ensure there are no spaces before or after the comma. For example, if you used chmod u=rwx, go-rwx test, chmod considers what comes after the space (go-rwx test) as filenames and results in a “No such file or directory” error when trying to access go-rwx.

If a file’s owner currently has the rw permission, for example, chmod u=rx will overwrite the current access rights with the new ones, while chmod u+rx will add the execute permission (because the read permission already has been granted).

When you use chmod with numeric arguments, the values for each granted access right have to be counted together per group. Thus, you get a three-digit number, which is the symbolic value for the settings chmod has to make. For example, for rw- permission, the corresponding numeric value (see Table 6.2) is (4=4) + (w=2) = 6. Therefore, the numeric value for rw-rw-rw- is 666. Table 6.4 lists the most commonly used numeric permission combinations to protect files and directories.

# NOTE

There is actually a fourth digit, which precedes the first three and sets special access modes, namely the sticky bits and the SUID/SGID bits. These settings are further discussed in the “Special File Permissions” section later in this chapter. To simplify discussion here, you can consider that leading digit to be zero and can omit it when specifying values for chmod.

# TABLE 6.4

Common chmod Settings

| COMMAND | TEXTUAL VALUE | MEANING |
|---|---|---|
| chmod 400 file | r-- --- --- | To protect a private file from being accidentally deleted or modified by the owner. |