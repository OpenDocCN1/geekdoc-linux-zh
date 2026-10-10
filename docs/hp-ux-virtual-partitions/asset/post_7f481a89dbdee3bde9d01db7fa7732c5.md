
![](img/eff8b9287a5f38c5adf538f24aacf29e_550_0.png)

Figure 9-22 Creating a New Volume

The maximum size that we could have made this volume is the total size of the unused disk of which rootdg is comprised, which is 17781760 bytes. We have selected about 1 GByte without RAID 5 because another disk would have been required. The default name of vol01 is used. In addition, selecting Add File System... from the bottom of Figure 9-22 brought up the window in Figure 9-23:

![](img/eff8b9287a5f38c5adf538f24aacf29e_551_0.png)

Figure 9-23 Specifying File System Information of a New Volume

In Figure 9-23 we selected a name of /dataspace as the mount point and have selected vxfs as the file-system type. After clicking OK, a new volume is created, as shown in Figure 9-24:

![](img/eff8b9287a5f38c5adf538f24aacf29e_552_0.png)

Figure 9-24 vol01

Figure 9-24 shows vol01 with a mount point of /dataspace. We can use the `vxprint` command with some useful options to see volume information. This includes information on the volume we just created. The following `vxprint` shows some useful options in the following listing:

```bash
$ vxprint -ASteg
Disk group: rootdg

dg  rootdg  default default 0 969390349.1025.13
md  disk01-01  vol01-01  disk01 0 1000000 0 c2t2d0 ENA
$
```

This output shows that our roughly 1 GByte area on `c2t2d0` is in place. We issued this `vxprint` with the `-q` option to eliminate the header information shown in the earlier example.

This simple example demonstrates the ease with which volumes can be added using VxVM. In the next section, we’ll add two disks to the system and perform some additional setup.

### HP VERITAS Volume Manager Mirroring and Striping

Now that we’ve covered the basics of VxVM, let’s take the next step and add two additional disks to our system and use mirroring and striping.

To begin with, let’s again use the `vxdisk` command to see the two new disks we’ve added to the system:

```bash
# vxdisk list

DEVICE    TYPE    DISK      GROUP     STATUS
c2t0d0    simple  -       -         online invalid
c2t2d0    simple  -       -         LVM
c2t2d0g   simple  -       -         online invalid
c2t2d0    simple  disk01  rootdg    online
```

At this point, the disks are listed, but they have not been configured in any way. These disks were physically added to the system, and no additional commands were issued prior to the `vxdisk`.

Let’s now go to the graphical interface and configure these disks. Figure 9-25 shows a total of four disks, including our two new unconfigured disks:

![](img/eff8b9287a5f38c5adf538f24aacf29e_554_0.png)

Figure 9-25 Two New Disks in vmsa

Figure 9-25 shows that disks `c1t0d0` and `c2t0d0` are installed and *Not Initialized*. Let’s now add these disks to a new disk group, called *test*, using the graphical interface as shown in Figure 9-26 for the first of the two disks:

![](img/eff8b9287a5f38c5adf538f24aacf29e_555_0.png)

Figure 9-26 Adding New Disk to Group test

We add both disks to *test* graphically using the *Add Disk(s)* window. This results in the screen shown in Figure 9-27, in which both new disks, *test01* and *test02*, are part of *test*.

![](img/eff8b9287a5f38c5adf538f24aacf29e_556_0.png)

We can confirm the disks in *test* with the `vxdisk` command as shown in the following listing:

```bash
# vxdisk list
DEVICE    TYPE      DISK     GROUP     STATUS
c1t0d0    simple    test01   test      online
c1t2d0    simple    -        -         LVM
c2t0d0    simple    test02   test      online
c2t2d0    simple    disk01   rootdg    online
#
```

The disks are now shown as configured with names of *test01* and *test02* and both are *online*. Both of these disks are part of *Group test*.

Next, let’s create a striped and mirrored volume in our new *disk group test*. Selecting *New* from the items on the *vmsa* window brings up the dialog box shown in Figure 9-28.

![](img/eff8b9287a5f38c5adf538f24aacf29e_557_0.png)

Figure 9-28 Creating a New Volume That is Striped and Mirrored

From Figure 9-28, you can see all of the characteristics specified for *vol02*. It is roughly 5 GBytes in size, it is striped, and it has one mirror copy. It is a file system type of *vfs* and has a mount point of */protected*.

After adding this volume, it appears in the *vxlist* window as shown in Figure 9-29:

![](img/eff8b9287a5f38c5adf538f24aacf29e_558_0.png)

Figure 9-29 Volume *vol02*

We could go to the command line to confirm the presence of *vol02* with *vxprint* and no options, as shown in the following listing:

```bash
$ vxprint
Disk group: rootdg

TY NAME       ASSOC        KSTATE   LENGTH     PLOFFS STATE       TU/TUOLD
-dg rootdg     -            -        -          -      -            -
-dm disk01     c2t2d0     -        17782088   -      -            -
v vol01        fsgen      ENABLED  1000000    -      ACTIVE       -
pl vol01-01    vol01      ENABLED  1000000    -      ACTIVE       -
-md disk01-01  vol01-01   ENABLED  1000000    0       -            -

Disk group: test

TY NAME       ASSOC        KSTATE   LENGTH     PLOFFS STATE       TU/TUOLD
-dg test       test       -        -          -      -            -
-dm test01     c1t0d0     -        17782088   -      -            -
-dm test02     c2t0d0     -        17782088   -      -            -
v vol02        fsgen      ENABLED  5000000    -      ACTIVE       -
pl vol02-03    vol02      ENABLED  5000064    -      ACTIVE       -
sv vol02-801   vol02-03   ENABLED  2500032    0       -            -
```

```
ev vo102-502 		vo102-03 		ENABLED 		2500032 		0 		-		-

v vo102-L01 		fsgen		ENABLED 		2500032 		-		ACTIVE 		-
pl vo102-P01 		vo102-L01		ENABLED 		LOGONLY 		-		ACTIVE 		-
ed test01-03 		vo102-P01 		ENABLED 		33 		LOG 		-		-
pl vo102-P02 		vo102-L01		ENABLED 		2500032 		-		ACTIVE 		-
ed test01-04 		vo102-P02 		ENABLED 		2500032 		0 		-		-

v vo102-L02 		fsgen		ENABLED 		2500032 		-		ACTIVE 		-
pl vo102-P03 		vo102-L02		ENABLED 		2500032 		-		ACTIVE 		-
ed test02-05 		vo102-P03 		ENABLED 		33 		LOG 		-		-
pl vo102-P04 		vo102-L02		ENABLED 		2500032 		-		ACTIVE 		-
ed test02-02 		vo102-P04 		ENABLED 		2500032 		0 		-		-
&
```

This output shows our 5 GByte volume as mirrored.

In addition, we want to see /protected as a mounted file system with `df -k`:

```bash
# df -k

Filesystem          kbytes     used    avail  %used Mounted on
/dev/vg00/lvol13    204800   55509  140002     28% /
/dev/vg00/lvol11   199361   45526  152916     26% /stand
/dev/vg00/lvol18    921600  387319  827033     45% /var
/dev/vg00/lvol17   937984  793162  135806     85% /
/dev/vg00/lvol14    204800    1529  190628      1% /tmp
/dev/vg00/lvol16   835584  722803  105775     87% /opt
/dev/vg00/lvol15    204800    1162  190917      1% /home
/dev/vx/dsk/rootdg/vol01
                      1000000   1349  936243     0% /dataspace
/dev/vx/dsk/test/vol02
                      5000000  2693  4695038    0% /protected
#
```

Our new volume, vol02, has been created with a size of 5 GBytes and a mount point of /protected.

Several of the basics of using VxVM were covered in the previous examples. This by no means is an exhaustive coverage of VxVM, but hopefully, it serves as a good introduction. Please refer to the detailed information in the manuals related to VxVM.

Although we focused mostly on `vmsa` in this section there are a number of `vx` commands that you can issue that perform the same functions as the graphical interface. I sometimes like to issue commands to view volume-related work that I have performed in the graphical interface just to confirm the results. Table 9-1 lists some of the most commonly used `vx` commands and their functions.

### Table 9-1 VxVM Commands

| Command | Description |
| :---- | :---- |
| vxsasst | Create and change volumes. |
| vxctl | Manage the vxconfigd daemon. |
| vxdg | Perform tasks related to disk groups. |
| vxdisk | Perform tasks related to disks. |
| vxdiskadd | Used to add disks. |
| vxedit | Change VxVM objects. |
| vxmake | Create VxVM objects. |
| vxmend | Correct configuration problems. |
| vxplex | Perform plex-related tasks. |
| vxprint | Print configuration information. |
| vxsd | Perform tasks on subdisks. |
| vxstat | Print volume statistics. |
| vxtrace | Trace volume tasks. |
| vxunrelocate | Move relocated subdisks. |
| vxvol | Perform volume tasks. |

These commands are covered in the HP documentation set, and there are also man pages available which provide detailed usage information on the commands.
