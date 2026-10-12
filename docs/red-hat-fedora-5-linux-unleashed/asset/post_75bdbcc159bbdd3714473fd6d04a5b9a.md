
# RELEVANT FEDORA AND LINUX COMMANDS

You will use the following commands when managing the kernel and its modules in Fedora:

- gcc—The GNU compiler system
- make—GNU project and file management command
- mkbootdisk—Fedora Core's boot disk creation tool
- sysctl—The interface to manipulating kernel variables at runtime
- mkinitrd—Create a RAM-disk file system for bootloading support

## Reference

- http://www.kernel.org/—The Linux Kernel Archives. The source of all development discussion for the Linux kernel.
- http://www.kerneltraffic.org/kernel-traffic/index.html—Linux Kernel Traffic. Summarized version and commentary of the Linux Kernel mailing list produced weekly.
- http://www.gnu.org/—The Free Software Foundation. Source of manuals and software for programs used throughout the kernel compilation process. Tools such as make and gcc have their official documentation here.
- http://slashdot.org/article.php?sid=01/08/22/145322&mode=thread—The famous AC Patches from Alan Cox, for whom they are named.
- http://www.digitalhermit.com/linux/Kernel-build-HOWTO.html—The Linux Kernel Rebuild Guide; configuration, compilation, and troubleshooting.
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/KernelAnalysis-HOWTO.html—kernel Analysis HOWTO. Describes the mysterious inner workings of the kernel.
- http://www.tldp.org/HOWTO/Module-HOWTO/—Kernel Module HOWTO. Includes a good discussion about unresolved symbols.
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Modules.html—The Linux Kernel Modules Installation HOWTO; an older document discussing recompiling kernel modules.
- http://www.tldp.org/—The Linux Documentation Project. The Mecca of all Linux documentation. Excellent source of HOWTO documentation, as well as FAQs and online books, all about Linux.
- http://www.minix.org/—The unofficial minix website. It contains a selection of links to information about minix and a link to the actual homepage. Although minix is still copyrighted, the owner has granted unlimited rights to everyone. See for yourself the operating system used to develop Linux.
- http://junga.dit.upm.es/~museyas/linux/kernel.hackers-docs.html—A web page with links to Linux kernel documentation, books, hacker tomes, and other helpful information for budding and experienced Linux kernel and kernel module developers. This list also will be found in the /usr/src/kernels/linux-2.6/Documentation/kernel-docs.txt file if you install the Fedora kernel sources.

# PART VI

## Appendix

## IN THIS PART

- APPENDIX A Fedora and Linux Internet Resources 989

# APPENDIX A

## Fedora and Linux Internet Resources

### IN THIS APPENDIX

- Websites and Search Engines
- Usenet Newsgroups
- Mailing Lists
- Internet Relay Chat

Linux enjoys a wealth of Internet support in the form of websites with technical information, specific program documentation, targeted whitepapers, bug fixes, user experiences, third-party commercial technical support, and even free versions of specialized, fine-tuned clone distributions.

This appendix lists many of the supporting websites, FTP repositories, Usenet newsgroups, and electronic mailing lists that you can use to get more information and help with your copy of Fedora.

**IF YOU NEED HELP 24/7**

If you are a small business, corporate, or enterprise-level Red Hat Linux user, do not forget that you can always turn to the source, Red Hat, or third-party companies, such as Dell and HP, who supply Red Hat servers for commercial technical support on a 24/7 onsite basis, by phone, by electronic mail, or even on a per-incident basis. Red Hat offers a spectrum of support options for its software products. You can read more about support options when you purchase Red Hat software at http://www.redhat.com/software/rhel/purchase/. Remember that Fedora is not an officially supported product from Red Hat. If you want help, try http://fedoraforum.org.

The appendix is divided into the following sections:

- Websites with Linux information arranged by category
- Usenet newsgroups pertaining to Linux
- Mailing lists providing Linux user and developer discussions
- Internet Relay Chat groups for Linux information

This appendix also lists websites that might be of general interest when using Fedora or specific components such as Xorg. Every effort has been made to ensure the accuracy of the URLs, but keep in mind that the Internet is always in flux!

**KEEP UP-TO-DATE WITH YOU**

Keeping informed about bug fixes, security updates, and other errata is critical to the success and health of a Fedora system. To keep abreast of the most important developments when using Fedora, be sure to register with the Fedora Announcements mailing list. The list tells you about updates that have been issued and what has been fixed as a result. Go to [http://www.redhat.com/mailman/listinfo/fedora-announce-list](http://www.redhat.com/mailman/listinfo/fedora-announce-list) to register for this mailing list. You should also use the `yum` command (as `root`) to keep up with bug fixes, new software packages, or security updates.

## Websites and Search Engines

Literally thousands of websites exist with information about Linux and Fedora. The key to getting the answers you need right away involves using the best search engines and techniques. Knowing how to search can mean the difference between frustration and success when troubleshooting problems. This section provides some Internet search tips and lists Red Hat, Fedora, and Linux-related sites sorted by various topics. The lists are not comprehensive, but have been checked and were available at the time of this writing.

### Web Search Tips

Troubleshooting problems with Linux by searching the Web can be an efficient and productive way to get answers to vexing problems. One of the most basic rules for conducting productive searches is to use specific search terms to find specific answers. For example, if you simply search for "Fedora Linux," you end up with too many links and too much information. But if you search for "Fedora Core sound," you are more likely to find the information you need. If you receive an error message, use it; otherwise, use the Linux kernel diagnostic message as your search criterion.

Other effective techniques include:

- Using symbols in the search string, such as the plus sign (+) to force matches of web pages containing both strings (if such features are supported by the search engine used by web search site)
- Searching within returned results
- Sorting results (usually by date to get the latest information)
- Searching for related information
- Stemming searches; for example, specifying returns for not only **link** but also **linking** and **linked**

Invest some time and experiment with your favorite search engine’s features—more productive searches will result. In addition to sharpening your search skills, also take the time to choose the best search engine for your needs.

### Google Is Your Friend

Some of the fastest and most comprehensive search engines on the Web are powered by **Linux**, so it makes sense to use the best available resources. Out of the myriad number of websites with search engines, http://google.com stands out from the crowd, with 81 million or more users per month. The site uses advanced hardware and software to bring speed and efficiency to your searches. If you are looking for specific Linux resources, take advantage of Google’s Linux page at http://google.com/linux.

Why is Google (named after a math number) so powerful? You can get a quick idea from the company itself at http://google.com/technology/index.html. Part of its success is because of great algorithms, good programming, and simple interface design, but most users really seem to appreciate Google’s uncanny capability to provide links to what you are looking for in the first page of a search return. Google’s early success was also assured because the site ran its search engine on clusters of thousands of PCs running a version of Red Hat Linux!

Google has the largest database size of any search engine on the Web, with more than eight billion web pages searched and indexed. The database size is important because empty search results are useless to online users, and the capability to return hits on esoteric subjects can make the difference between success and failure or satisfaction and frustration. Some of Google’s features include **GoogleScout** link to return similar pages on the results page, the capability to see the exact version of a web page as returned to a search engine (known as a *cached* feature), advanced searches, and more recently, a link to an active Usenet news feed!

To get a better idea of what Google can offer you, browse to http://www.google.com/options/. You will find links to more than two dozen different services and tools covering specialized searches, databases, information links, translators, and other helpful browsing tools.

### Fedora Package Listings

You can quickly and easily view a list of the installed RPM packages installed on your Fedora system, along with a short description of each package, by using the `rpm` command:

```bash
$ rpm -qai | less
```

Fedora users can also use the `yum` command to view package names and information about not only installed packages, but any available updated packages, like this:
