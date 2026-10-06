Unlike Windows, the Linux filesystem all stems from a single point called root and is represented by a solitary forward slash (/). Your own account folder is located within a subfolder of root called home. This is represented as /home/, to put it into words, the Home folder within root. If your user account were to have the same name as mine, ng, the path to that folder would be /home/ng, or the ng folder within home within root. Whatever the name of your user account or the name of any other accounts you have on your machine happen to be, just remember that when you are lost, your folder and those of all the other folks with user accounts on your machine are located within the Home folder. If you're a more graphically oriented person, the map in Figure 7-6 should help you.

![](bbox=[0.26, 0.281, 0.675, 0.633])

Figure 7-6: The location of your users' folders within the Linux filesystem

# # What's in All Other Folders?

Needless to say, there is more to the Linux filesystem than the root, Home, and user account folders. Several other directories appear at the same level as Home, though for the most part, you shouldn't be mucking around with them unless you know what you're doing. Frankly, most of these folders are write protected, so you should be well protected from yourself. Still, it is natural to be curious about what other folders are there for, since ... well, they are there. So, to satisfy your curiosity a bit, I'll do a little explaining.
in Ubuntu, four folders contain most of the applications on your system. The essential elements of your system are located in /sbin. Other elements that need to be there such as commands and the like, which may not be used, are located in /bin. Most of the applications that you actually think