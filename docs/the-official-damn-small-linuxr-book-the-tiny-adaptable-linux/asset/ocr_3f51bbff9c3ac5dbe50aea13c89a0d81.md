use while running with Qemu. After this is set up, it will be the simplest way to have access to your backup files and extensions while running DSL-Embedded.

Most people who are interested in creating a virtual hard drive are running DSL-Embedded from a pen drive. The rest of this section will use the pen drive as a physical reference point for consistency, yet some may want to have this setup sit on the regular hard drive on their personal computer. The steps are the same as what follows; just substitute any reference to a pendrive with your own local path.

To create a Qemu virtual hard drive, you have to use the qemu-img.exe program included in the dsl-embedded.zip file. After it is unpacked, the program sits in the Qemu directory or folder as recognized by MS Windows. The following procedure describes how to create a virtual hard drive for DSL:

+   1. Open a DOS window and navigate to the qemu folder inside your pen drive. In MS DOS, the navigation command is CD. If your pen drive is recognized by Microsoft Windows as drive E, you would type the following:
+   
+      `CD E:\qemu\`

+   2. Use the qemu-img.exe program to create a virtual hard drive. This hard drive will have a physical presence on your pen drive; you will see it there as harddisk. (This virtual hard drive will be used later when selecting the dsl-vhd.bat file to boot dsl-embedded.)
+   
+      After navigating to your Qemu folder, you need to use qemu-img.exe to create your virtual hard drive. The size you choose is limited by the space available on your pen drive, and it is up to you to choose what is best for your needs.

> **NOTE**
> 
> Keep in mind that this hard drive is *virtual* in the sense that it is not a real drive (instead, it is a file on your pen drive). The virtual hard drive is actually *real* in that it takes up real space on your pen drive that you cannot use to store your non-DSL related files.

The command to use with qemu-img.exe is

```
E:\qemu> qemu-img.exe create hard disk SIZE
```

where SIZE is the actual size you want the virtual hard drive to be. For a 64MB virtual hard drive, type

```
E:\qemu> qemu-img.exe create harddisk 64M
```