
# 132 CHAPTER 4 INTRODUCTION TO UBUNTU LINUX

![](img/45ff4cd21497435daa35084a84b95d07_182_0.png)

**Figure 4-22** The Software windows, Updates tab

Other Software You can add, edit, and remove repositories from the Other Software tab. The adjacent security box concern concerning adding repositories. Unless you are working with software that is not distributed by Ubuntu, you do not need to add any repositories. To add a CD/DVD as a repository, click **Add CD-ROM.**

Updates The top part of the Updates tab (Figure 4-22) specifies which types of updates you want the Update Manager to monitor. Typically you will want to import security updates and recommended updates. In the middle section of this tab you can specify if and how often the Update Manager will check for updates and what to do when it finds updates. The drop-down list **Show new distribution releases** allows you to specify whether you want the Update Manager to inform you when you can upgrade the system to a new release of Ubuntu and whether you are interested in all releases or just LTS (page 31) releases.

Authentication The Authentication tab holds keys for trusted software providers. Ubuntu uses these keys to authenticate software, which protects the system against malicious software. Typically Ubuntu provides these keys automatically.

Statistics The Statistics tab allows you to participate in a software policy contest.

# THE UBUNTU SOFTWARE CENTER

You can use the Ubuntu Software Center window (Figure 4-23) to add and remove applications from the system. It is simpler and has fewer selections than synaptic (besides next).

# UPDATING, INSTALLING, AND REMOVING SOFTWARE PACKAGES 133

![](img/45ff4cd21497435daa35084a84b95d07_183_0.png)

**Figure 4-23** The Add/Remove Applications window

Open this window by selecting Main menu: Applications⇔by giving the command software-center from a terminal emulator or Run application window (ALT-F2).

When you select a category of applications from the window when you open it, the Ubuntu Software Center displays a list of applications in that category on the right side of the window. If you know the name of the application you want to install, you can query for it by entering the name or part of the name in the text box at the upper-corner right of the window. The Ubuntu Software Center displays lists of applications that satisfy your query.

Scroll through the applications displayed on the right side of the window. When you click/highlight an application, the window displays two buttons: **More Info** and **Install**. When you click the first button to display information about the application. When you click Install, the Ubuntu Software Center asks for your password and starts downloading and installing the application. While it is working, you can search for and select additional applications to install. When it is finished, the Ubuntu Software Center puts a green check mark next to the name of the package. Close the window. Packages you installed should be available on the Main menu.

# synaptic: FINDS, INSTALLS, AND REMOVES SOFTWARE

This section describes how to use synaptic to find, download, install, and remove software packages. Open the Synaptic Package Manager window by selecting System⇔Administration⇔Synaptic Package Manager from the Main menu or by

# 134 CHAPTER 4 INTRODUCTION TO UBUNTU LINUX

![](img/45ff4cd21497435daa35084a84b95d07_184_0.png)

Figure 4-24 The Synaptic Package Manager from a terminal emulator or Run Application giving the command synaptic from a terminal emulator or Run Application window (ALT-F2). Figure 4-24 shows the initial window. The first time you run synaptic, it reminds you to reload package information regularly. You can do so by clicking *Reload* on the toolbar.

The Synaptic Package Manager displays a lot of information. Maximizing this window and widening the left column (by dragging the handle) may make it easier to use. When the **Sections** button is highlighted in the left column, the top of the left column holds a list box containing categories of software. Initially **All** is selected in this list box, causing the window to display all software packages in the list box at the top of the right column.

You can show the list of packages in the list box by clicking **Search** on the toolbar. To do so, display the Find window by entering the name or part of the package you are looking for in the text box labeled **Search**. (Alternatively, you can search using the text box labeled **Quick search** on the main window.) For example, display all packages exim4 in the text box labeled **Search** and select **Description** and **Name** from the drop-down list labeled **Look in** (Figure 4-25). Click Search. The Synaptic Package Manager displays the list of packages meeting the search criteria specified

![](img/45ff4cd21497435daa35084a84b95d07_184_1.png)

Figure 4-25 The Find window

# UPDATING, INSTALLING, AND REMOVING SOFTWARE PACKAGES 135

![](img/45ff4cd21497435daa35084a84b95d07_185_0.png)

**Figure 4-26** The Synaptic Package Manager window displaying chess programs in

The Synaptic Package Manager window displaying chess programs in (Figure 4-26) shows how to select packages for installation. To select a package for installation, click the **Mark** button. The package will be marked for installation. To remove a package, click the **Unmark** button. To apply the changes, click **Apply** on the toolbar. The synaptic utility keeps you informed of its progress. When it is done, it displays the Changes applied window. Close and then close the Synaptic Package Manager window. Now it appears on the Main menu: Applications⇔Games.

![](img/45ff4cd21497435daa35084a84b95d07_185_1.png)

**Figure 4-27** Mark required changes

# 186 CHAPTER 4 INTRODUCTION TO UBUNTU LINUX

To apply the changes you have marked, click Apply on the toolbar; synaptic displays a window. (If you were installing and/or removing packages, this summary would be longer.) Click Apply.

# WHERE TO FIND DOCUMENTATION

Distributions of Linux, including Ubuntu, typically do not come with hardcopy reference manuals. However, online documentation has always been one of Linux's strengths. The man (or manual) and info pages have been available since early releases of the operating system. Ubuntu provides a graphical help center. Surprisingly, with the ongoing growth of Linux and the Internet, the sources of documentation have expanded as well. This section discusses some of the places you can look for information on Linux in general and on Ubuntu in particular. Also see Appendix B.

# UBUNTU HELP CENTER

To display the Ubuntu Help Center window (Figure 4-28), click the blue object with a question mark in it on the Top panel or select Main menu: System⇔Help and Support. Click topics in this window until you find the information you are looking for. You can also search for a topic using the text box labeled Search.

# man: DISPLAYS THE SYSTEM MANUAL

In addition to the graphical Ubuntu Help Center, the textual utility displays man pages from the system documentation. This is helpful when you know which you want to use but forgot exactly how to use it. You can also refer to the man pages to get more information about specific topics or determine which features are available with Linux. Because the descriptions in the system documentation are often terse, they are most helpful if you already understand the basic functions of a utility.

# Online pages

The Ubuntu.com site holds dynamically generated copies of man pages from every package of every supported Ubuntu release. In addition to presenting man in easy-to-read HTML format, this site does not require you to install a holding utility to read its man page. It also allows you to read man pages for a release you do not have installed.

Because man is a character-based utility, you need to open a terminal emulator (page 125) to run it. You can also log in on a virtual terminal (page 149) and run man from there.
