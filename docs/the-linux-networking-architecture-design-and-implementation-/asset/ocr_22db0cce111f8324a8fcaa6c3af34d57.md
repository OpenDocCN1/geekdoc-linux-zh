# A.1 Functionality

553

![](bbox=[0.143, 0.075, 0.856, 0.465])

FIGURE A-2
Browsing the Linux kernel in the LXR source-code browser, using the ip_recv() function as example.

Information about the current development in the beta stage is available at http://1xr.sourceforge.org.

# ### A.1 Navigation through the source code

The entry point into the LXR source-code browser is shown in Figure A–1. This is the root directory for source files of the Linux kernel. From this page, we have the follow-ing possibilities:

+   Browsing to a specific file of the kernel sources: You can click your way to a desired file by clicking the corresponding directories. If you know the file path, you can abbreviate it by directly typing the path in the URL. The path of the desired file is simply written after /source/ in the URL. Figure A-2 shows this by the example of net file /ipv4/ip_input.c.

+   Searching for a file: If you don't know the name of the desired file, you can search for it on the file search page.

+   Searching for a keyword: When working with the Linux source code, we are mainly-interested in functions and data structures (i.e., what was defined as keywords above).

+   Keywords are stored in the reference file of the LXR source-code browser. This file also includes all information about the use of a keyword. Clicking a keyword emphasized as hyperlink or explicitly searching for a keyword on the identifier