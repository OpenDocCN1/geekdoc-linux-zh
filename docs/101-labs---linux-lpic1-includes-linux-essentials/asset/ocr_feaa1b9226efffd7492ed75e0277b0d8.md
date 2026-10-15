
# Task 6

The default permissions for a newly created file can be adjusted with `umask`. This serves to "mask out," at a bit level, permissions that a new file should not have. Run the following:

```bash
u=$(umask)
umask 0777
mkdir bar
ls -ld bar
umask $u
```

The `bar` directory should have no permissions set—you've masked them all out with `umask`.

Finally, clean up with:

```bash
sudo rm -r foo bar
```

# Notes

Another special bit specific to directories is called the sticky bit, which is covered in Lab 25. This bit, set on a world-writable directory, ensures that users can only remove or modify files that they themselves own. This is most useful on `/tmp`.
