**Task 6:**

Finally, clean up:

```
cd ~
rm -r lab46
```

**Notes:**

To open a file descriptor for reading only, you could use `exec 3< file`, or for writing only, `exec 3> file`.