> CAUTION
> 
> Choosing Whole Hard Disk in the previous step will completely erase your hard drive. Any other operating systems and data you have on the hard drive will be gone forever. Please make sure that this is really what you want to do. Otherwise, you will end up with absolutely nothing but SuSE Linux on the hard drive.

YaST now partitions and prepares your hard drive for SuSE Linux. This process might take some time depending on the size of the space YaST has to work with. YaST will create the following three partitions on your hard drive:

+   - /boot partition—This partition is where your boot files will be kept. This partition is usually very small in size.
+   - / partition—This is the root partition where all your systems will be installed. This partition takes the most space from your hard drive.
+   - Swap partition—This partition is used as virtual memory by Linux. Linux uses swap partition instead of files for its virtual memory. This partition is usually twice as big as the amount of RAM you have, with a maximum size of 128MB.

When YaST is finished preparing your hard drive, it will take you to the package selection screen (see Figure 2.20). This is where you will select which packages to be installed by SuSE Linux. At this point, you have two choices: You can either select one or more of the preset package configurations (recommended) or manually select the packages you want to install (not recommended if this is your first time through the installation process).

# FIGURE 2.20
YaST's package selection/configuration menu.

![](bbox=[0.35, 0.68, 0.85, 0.92])

To select one of the package configurations, highlight the first option in the menu, Load Configuration. As you can see in Figure 2.21, YaST will display a list of common configurations and the approximate amount of hard drive space that each will use. Any configuration that has an asterisk (*) next to it is selected by default regardless of whether you select it. For example, SuSE Minimum System is selected by default because it is a subset of any other