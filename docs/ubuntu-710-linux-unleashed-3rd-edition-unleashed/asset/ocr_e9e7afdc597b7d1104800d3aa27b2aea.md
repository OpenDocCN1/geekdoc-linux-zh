# CHAPTER 16

# File and Print

# IN THIS CHAPTER

In the early days of computing, file and printer sharing was pretty much impossible because of the lack of good networking standards and interoperability. If you wanted to use a printer connected to another computer, you had to save the file to a floppy disk and walk over.

Nowadays, both file and printer sharing have become second nature in a world where it is not unusual for someone to own more than one computer. Whether it be for sharing photographs among various computers or having a central repository available for collaboration, file sharing is an important part of our information age. Alongside this is the need to be able to share printers; after all, no one wants to have to plug and unplug a computer to a printer just so he can print out a quick letter.

Whatever your reasons for needing to share files and printers across a network, you find out how to do both in this chapter. We look at how you can share files using the popular UNIX NFS protocol and the more Windows-friendly Samba system. You also find out how to configure network-attached printers with interfaces such as JetDirect. We look at both graphical and command-line tools, so you should find something to suit the way you work.

+   - Using the Network File System
+   - Putting Samba to Work
+   - Network and Remote Printing with Ubuntu
+   - Creating Network Printers
+   - Using the Common UNIX Printing System GUI
+   - Avoiding Printer Support Problems
+   - Reference

# CAUTION

By default, Ubuntu ships with all its network ports blocked. That is, it does not listen to any requests on any ports when it is first installed. To configure the firewall, you must retrieve and install Firestarter using either synaptic or apt-get. After you have installed this, you can use it to configure the firewall to open specific ports relating to the topics covered in this chapter.

You can find detailed documentation about Firestarter at http://www.fs-security.com/docs/.