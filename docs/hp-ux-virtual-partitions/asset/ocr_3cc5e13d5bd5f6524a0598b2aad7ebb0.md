```
ea\_aa01487
OB\_AMFE\_aa01630
cmd\_res8215
tmp\_cfg\_file
cmd\_res8708
excl\_ude\_temp
arch\_incl\_ude\_l
3570 blocks
# 
```

Now that we have written to the tape and viewed its table of contents, we'll restore the contents of /var/tmp. In the following example we use several options to `cpio`. including `i` for input mode, `c` for ASCII header format, `v` for verbose, `B` for block output, `d` for directories, `u` for unconditional write over existing files, and `m` to restore the original modification times:

```
# cpio -icvBdu m < /dev/rmt/0m
.
envd\_action2
envd\_action5
swagent\_log
ntp
OB\_AMHB\_AA01020
aaaa01558
aaaa01426
aaaa01112
OB\_AMHB\_AA01540
aaaa01299
.
.
.
.
.
ea\_aa01487
OB\_AMFE\_aa01630
cmd\_res8215
tmp\_cfg\_file
cmd\_res8708
excl\_ude\_temp
arch\_incl\_ude\_l
3570 blocks
# 
```