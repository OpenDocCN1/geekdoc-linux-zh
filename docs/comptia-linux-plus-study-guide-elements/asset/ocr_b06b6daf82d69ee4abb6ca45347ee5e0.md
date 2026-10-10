# 306

# Chapter 7 • Managing Packages and System Backups

If you prefer to use GUI tools rather than command-line tools, you should be aware that GUI front-ends to yum exist. Examples include Yum Extender (yumex) and kyum. You can use the text-mode yum to install these front-ends, as in `yum install yumex`. Figure 7.1 shows Yum Extender in action. To use it, click the Updates, Available, Installed, or All button to show the relevant types of packages. You can enter a search term in the line below these options (Figure 7.1 shows samba in this field) to restrict the package selection. You can then check or uncheck the tick boxes next to specific package names to mark them for installation or removal. When you’ve made your selections, click Process Queue to implement the changes.

# FIGURE 7.1 The Yum Extender (yumex) program provides a GUI front-end to Yum.

![](bbox=[0.19, 0.33, 0.78, 0.68])

Yum is configured via the `/etc/yum.conf` file, with additional configuration files in the `/etc/yum.repos.d/` directory. The `yum.conf` file holds basic options, such as the directory to which Yum downloads RPMs and where Yum logs its activities. Chances are you won’t need to modify this file. The `/etc/yum.repos.d/` directory, on the other hand, potentially holds several files, each of which describes a Yum repository—that is, a site that holds RPMs that may be installed via Yum. You probably shouldn’t directly edit these files; instead, if you want to add a repository, manually download the RPM that includes the repository configuration and install it using `rpm`. The next time you use Yum, it will access