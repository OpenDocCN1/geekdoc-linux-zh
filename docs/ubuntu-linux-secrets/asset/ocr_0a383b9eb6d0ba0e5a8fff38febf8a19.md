To perform a detailed analysis of your system, select one of the four scanning buttons in the toolbar:

+   - **Scan Home:** to analyze the folders contained in your home folder
+   - **Scan Filesystem:** to analyze the entire filesystem
+   - **Scan Folder:** to single out a folder to analyze
+   - **Scan Remote Folder:** to scan a remote filesystem

Be careful when selecting to scan the entire filesystem or a remote filesystem. Analyzing the disk space requires reading the entire disk area. This process can take some time, depending on the size of the disk and, in the case of a remote scan, network connectivity speeds.

The result of a complete scan is shown in Figure 18-10.

![](bbox=[0.177, 0.321, 0.832, 0.659])

**Figure 18-10:** A complete disk scan analysis.

The treemap view can seem confusing at first, but once you get the hang of it you’ll see that you can glean quite a bit of information from the treemap.

The treemap works from the core of the diagram outward. The core represents the top level of the tree. In my example, because I performed a home scan, the core is my home folder, /home/rich. If you hover the mouse pointer over the core, it shows the name of the folder and the amount of disk space used by that folder.

The next layer of rings depicts the next level of folders. In my home folder I have three subfolders. Each subfolder is a section of the first-layer ring, and its size is relative to the amount of used disk space in that subfolder.

The second layer of rings relate to the first layer. If there are subfolders beneath a subfolder, they appear in the second layer of rings, above their parent folder. Again, each folder in the second layer has a size relative to the amount of disk space it uses.