Pentium III-class system with more RAM and available disk space than we mentioned earlier.

# SMS Features

One question you have to ask yourself before deciding on deploying SMS is if it will provide the services and functionality you need. Table 15.5 details the important features of Microsoft Systems Management Server 2.0.
Hopefully this section has provided enough information for you to decide if SMS can benefit your network environment.

# THE WINDOWS 2000 REGISTRY

The Windows 2000 Registry stores information on virtually every aspect of the operating system. Software packages also use the Registry to store application-specific configuration data. The Registry itself is not a new concept. In fact, Microsoft replaced the familiar ini files with the Registry in Windows 95. You can view and edit data in the Registry using regedt32.exe, which can be executed from the Start menu's Run dialog, or from a command prompt. Figure 15.9 shows the Registry Editor.

The Windows 2000 Registry is hierarchical, meaning it has a parent-child structure, much like the files and folders on a disk. The Registry consists of subtrees, which themselves contain keys and values. The actual data is stored on disk in Registry hives, in %SystemRoot%\system32\config. Table 15.6 details the different subtrees contained in the Registry.

Each subtree can contain multiple keys, and those keys can themselves contain keys and values. Table 15.7 details the different components of the subtrees.

You can use the Registry Editor to search for specific keys and values, edit existing keys and values, and create new keys and values. The Registry Editor will also allow you to modify the security settings on subtrees and their components. We caution you to be very careful when manipulating the Windows 2000 Registry as it is very easy to leave a software application and/or your system in an unstable state. You should only directly modify the Registry when it is absolutely necessary to do so. However, searching the Registry is a very convenient method of determining application and system settings.

# Summary

As your infrastructure grows, managing user data as well as application files can become a full-time job. Users outgrow their disk resources and application software changes almost daily. In this chapter, we discussed some of the possible ways to manage the software in your environment.