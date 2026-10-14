![](bbox=[0.291, 0.104, 0.793, 0.31])

**Figure 12-1** Ubuntu recovery mode menu

+   - **clean**  
+     The clean option attempts to clear up some free space on your system in case you have filled up / and can’t access the system.
+   
+   - **dpkg**  
+     This option will perform an apt-get update and upgrade and will attempt to repair any problems you might have with half-installed packages. You might choose this option if a package did not fully install or upgrade correctly and its init script is stalling out so the system can’t boot fully. This choice could potentially fix the package problems.
+   
+   - **grub**  
+     If you select this option, the rescue mode will update GRUB—handy if you have accidentally trashed your GRUB configuration.
+   
+   - **netroot**  
+     This mode is the most useful of the options in this menu as it just drops you to a root shell on your booted server. I will spend the rest of this section focused on what you can recover with this option.
+   
+   - **root**  
+     This mode is like the netroot option only without networking enabled.