data is still out on the disk. Someone may access that data, either inadvertently or deliberately. To avoid this, set the secure deletion attribute on the file. When the file is deleted, all data blocks will be set to 0 and written to disk. ${ }^{8}$ For example, we can set this attribute on the file really_private:

```
```
$ chattr -v +s really_private
chattr 1.12, 9-Jul-98 for EXT2 FS 0.5b, 95/08/09
Flags of really_private set as s-----
$
```
```

The -v flag of chattr is for verbose output, essentially saving the step of executing lsattr to confirm the setting. Notice that you need not be root to set the secure delete attribute. The only attributes requiring root privilege are the immutable (i) and append-only (a) attributes.

The a attribute is useful for log or similar files to which data is appended but not overwritten. When the a attribute is set, the only way to modify the file is by appending data to it. Once this bit is set, even root cannot remove the file. You can set the append-only attribute, for example, on /var/log/secure:

```
```
# chattr -V +a /var/log/secure
chattr 1.12, 9-Jul-98 for EXT2 FS 0.5b, 95/08/09
Flags of /var/log/secure set as ---a---
```

```

Let's verify that this file cannot be removed:

```
```
# rm /var/log/secure
rm: /var/log/secure: Operation not permitted
```

```

You may also set multiple flags using the = operator instead of the + operator:

```
```
# chattr -V =Aa /var/log/secure
chattr 1.12, 9-Jul-98 for EXT2 FS 0.5b, 95/08/09
Flags of /var/log/secure set as ----a-A
```

```

Here we are also setting the A attribute (no atime—see Table 4.4 on page 75), which suppresses access timestamp updating.

At some point you may need to unset an attribute. For example, to unset the a attribute on /var/log/secure:

```
```
# chattr -V -a /var/log/secure
chattr 1.12, 9-Jul-98 for EXT2 FS 0.5b, 95/08/09
Flags of /var/log/secure set as -------A
```

```

8. This does not guarantee complete erasure of the data. There are techniques to reconstruct the data on media even after the blocks are overwritten numerous times. See Chapter 15 for a more secure file deletion solution.