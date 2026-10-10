Volume Manager section of this chapter, you will want to do so before you make this selection (LVM is Logical Volume Manager.) I am a strong advocate of using Logical Volume Manager with VxFS whenever possible.

+   - Root Swap - The system automatically selects an amount twice the size of your main memory, or a maximum of 1024 MB. You will want to consider your primary swap space very carefully. The L-Class system in our example has 2GBytes of memory and we'll go with the default of 1 GByte of swap as shown.

+   - Languages - We'll install English on our system; however, there are many languages available for Iii systems.

+   - Additional - This is the pick at the bottom right corner of the screen, not the tab area. Here is where you can configure such things as a second swap area, adding a second disk drive to the root volume, and disabling DHCP. With Ili, DHCP, Dynamic Host Configuration Protocol, works with an Ignite-UX server that automatically assigns system name, IP address, and so on.

The major difference between the selections just discussed for Ili and earlier releases of 11.x are the *Operating Environments*. Ili is the first HP-UX release for which *Operating Environments* are available.

Moving to the *Software* tab area, we find software on the installation CD-ROM for Ili that has been marked for installation. Since we have selected the *Mission Critical Operating Environment* there is a lot of software automatically selected as part of this installation.

Figure 1-5 shows some of the software we have selected in the *Software* tab area. We have selected *All* so that we can see all of the software that has been selected as part of the *Mission Critical Operating Environment*. We could scroll down to see additional software.