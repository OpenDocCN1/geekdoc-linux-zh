![](bbox=[0.05, 0.12, 0.15, 0.22])

# # Listing the Software

Although I like the graphical user interface of **swinstall**, you can also issue Software Distributor commands at the command line. One example is the **swlist** command. The **swlist** command is useful for viewing the software you have loaded on your system, viewing the software you have loaded in a depot, or producing a list of depots. A graphical user interface to the **swlist** command can be invoked with the *-i* option and is also available in SAM. With the **swlist** command, you perform many functions, including the following:

+   List the software you have at the specified level with the *-l* option. I will show several examples shortly. The levels you can specify are:

+   * root
+   * depot
+   * bundle
+   * product
+   * subproduct
+   * fileset
+   * file

Levels are delineated by "." so you will see *bundle:*[product]*[:* [subproduct]*[:* [fileset] ]. You can get all kinds of useful information out of **swlist** and use this for other purposes. Some of the things you can do with **swlist** are:

+   • Display the table of contents from a software source.
+   • Specify which attributes you wish to see for a level of software such as name, size, revision, and so on.
+   • Create a list of products that can be used as input to other Software Distributor commands, such as **swinstall** and **swremove**.

When you run **swlist** with no options, you get a list of the software products installed on your system. Let's try a few **swlist** commands with the *-l* option to view software installed on a system (by default, **swlist** will list installed products; you can use the *-s* option to specify a software depot or