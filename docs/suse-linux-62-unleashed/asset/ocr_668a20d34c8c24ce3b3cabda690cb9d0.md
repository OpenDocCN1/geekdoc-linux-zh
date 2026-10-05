# Software Management
CHAPTER 19

Note (in Figure 19.3) that in the fun series, a list of packages is displayed. The left column displays a pair of brackets ([]) that shows the status of the package. The value inside the pair be

+   [ ] The package is not installed.
[I] The package is installed.
[D] The package is installed and will be removed.
[R] The package is installed and will be updated.
[X] The package will be installed.

Toggle a software package's status by pressing the spacebar, Enter key, or plus (+) or minus (-) keys. Press F2 to get a description of the software package (much like the rpm command's -qi or -qpi options). A dialog box displaying a description will appear, as shown in Figure 19.4.

When you've finished selecting software for removal or installation, press F10 to.

![](bbox=[0.068, 0.423, 0.233, 0.603])

```
Terminal - zsh
File Help Search: fun
Packages tuxuins Series: *
Author: Jan van Meer, Jan van Wij, Jr.
Copyright: 1998, Jan van Wij, Jr.
Package: 1.0 /usr/tuxuins.rpm (217.5 K)
Size: Installed 1.4 M (compressed)
Source: sphew dev-rubios a x +libpng-gre a
Installed: Fri Sep 10 04:32:17 1998
Version: 0.5.2-4
With rolling eyes
A penguin dually to springuin. Very cute with its rolling eyes
following the house curves.
A tumultuous mixture of sticky, springuin and keys.
Continue _
```

![](bbox=[0.883, 0.613, 0.933, 0.765])

You'll be at the main Yaast dialog box (shown in Figure 19.1). Select the Start Installation and press Enter. If you're removing software, Yaast will ask for confirmation, as shown in Figure 19.5.

When removing or overwriting one or more software packages, yast will also ask for permission to choose the location of a compressed tar archive as a backup of the software to be removed. If you choose to remove the software, you'll see the dialog box shown in Figure 19.6.

If you don't want to use the default /var/adm/backup directory, type in a different location, select Yes and press Enter. To avoid the backup step, use the Tab key to select No and press Enter. To cancel, press the Esc or use the Tab key to select Abort and press Enter.