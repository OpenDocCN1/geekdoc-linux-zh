v4.33                               A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

The problem is that the offset we have is the keyword's offset in the disk image, not in the file system (which is what the volume data block is associated with). So we have to calculate the offset to the file AND the offset to the partition that contains it. The offset to the partition is simply a matter of multiplying the sector offset by the size of the sector for our system:

```
barry@forensic1:~/aleb$  echo "10260+512" | bc
5253120
```

![](bbox=[0.159, 0.342, 0.859, 0.545])

The difference between the two is the volume offset of the keyword hit, instead of the physical disk (or image) offset.

```
barry@forensic1:~/aleb$ echo "10561603-5253120" | bc
5308483
```

![](bbox=[0.159, 0.686, 0.859, 0.891])

229