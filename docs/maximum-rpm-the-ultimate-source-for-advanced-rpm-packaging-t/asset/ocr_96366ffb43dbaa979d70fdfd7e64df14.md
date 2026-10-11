What does all this stuff mean? Let’s go through it, item by item:

+   ■ /usr/sbin/adduser is simple: It’s the name of the file being dumped.
+   ■ 4442 is the size of the file, in bytes.
+   ■ How about 841083888? It’s the time the file was last modified, in seconds past the UNIX zero date of January 1, 1970.
+   ■ ca5fa53dc74952aa5b5e3a5fa5d8904b is the MD5 checksum of the file’s contents, all 128 bits of it.
+   ■ If you guessed 0100755 was the file’s mode, you were right.
+   ■ The first root represents the file’s owner.
+   ■ The second root is the file’s group.
+   ■ We’ll take the next part (0 0) in one chunk. The first 0 shows whether the file is a config file. If 0, as in this case, the file is not a config file. The next 0 shows whether the file is documentation. Again, since there is a 0 here, this file isn’t documentation either.
+   ■ The final 0 represents the file’s major and minor numbers. These are set only for device special files. Otherwise, it will be 0.
+   ■ If the file were a symlink, the spot taken by X would contain a path pointing to the linked file.

Normally, the --dump option is used by people who want to extract the file-related information from RPM and process it somehow.

# 5.2.2.10. --scripts: Show Scripts Associated with a Package

If you add --scripts (that’s two dashes) to a query, you get to see a little bit more of RPM’s underlying magic:

```
# rpm -q --scripts XFree86
preinstall script:
(none)

postinstall script:
/sbin/ldconfig
/sbin/pamconfig --add --service=xdm --password=none --sesslist=none

preuninstall script:
(none)

postuninstall script:
/sbin/ldconfig
if [ "$1" = 0 ]; then
/sbin/pamconfig --remove --service=xdm --password=none --sesslist=none
fi
```