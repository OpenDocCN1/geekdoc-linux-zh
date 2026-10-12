```
#System keyboard
keyboard us

#System mouse
mouse generics/2

#System timezone
timezone --utc America/New_York

#Root password
rootpw --iscrypted $1$/n3yjdV$AWoBZgRqq/1Ax9hX1JSM1
...
```

![](bbox=[0.16, 0.34, 0.84, 0.71])

**FIGURE 2.2 Fedora's kickstart configuration tool, ksconfig, can be used to quickly and easily create installation profiles for use in automated installations.**

Note that not all the output of a sample ks.cfg is shown. However, you can see that this file will feed kickstart directions for an install, including an encrypted root password to be installed on the target system.

The next step is to copy your new ks.cfg to a boot disk created using one of the boot floppy images (found under the images directory on the first Fedora CD/DVD). You can