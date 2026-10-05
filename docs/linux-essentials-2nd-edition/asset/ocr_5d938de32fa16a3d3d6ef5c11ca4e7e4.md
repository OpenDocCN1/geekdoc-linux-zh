# Chapter 9 • Exploring Processes and Process Data

![](bbox=[0.235, 0.065, 0.928, 0.493])

FIGURE 9.1 Most Linux distributions tell you when updates are available for your system.

# Managing Red Hat Systems

RPM-based distributions include Red Hat, Fedora, CentOS, SUSE Enterprise, openSUSE, and Mandriva. The basic tool for installing software on these distributions is the text-mode rpm command. This program works on local files, though; to use a network repository, you must use another tool, which varies by distribution:

+   - Red Hat, Fedora, and CentOS use the text-mode yum or various GUI frontends to it, such as Yumex.
- SUSE Enterprise and openSUSE use zypper or a GUI front-end such as YaST2.
- Mandriva uses the text-mode rpm or the GUI Rpmdrake.

Because of the variability between these distributions, particularly for network-enabled updates, providing a complete description of all these tools is impractical here. Fortunately, the GUI tools are easy to use and accessible. Every