# RHEL Server Optional

A large group of packages not normally associated with server systems. It includes desktop packages and more.

In contrast, the repository categories for third-party rebuild distributions vary. Generally, they include categories such as main and extras, along with supplementary packages and more. In most cases, while the main repository includes just the packages available from the released DVD, updated packages are configured in their own repositories.

Each repository includes a database of packages in a repodata/ subdirectory. That database includes information on each package, including dependencies. That database allows installation requests to that directory to include all dependencies. If you have a subscription to the RHN, access to these repositories is enabled in the rhnplugin.conf file, in the /etc/yum/pluginconf.d directory. That file is discussed later in this chapter.

Later in this chapter, you'll examine how to configure connections to repositories with the configuration files associated with the yum command.

![](bbox=[0.12, 0.6, 0.2, 0.7])

> A dependency is a package that needs to be installed to make sure all the features of a target package is available.

# Install an RPM Package

There are three basic commands that may install an RPM. They won't work if there are dependencies (packages that need to be installed first). For example, if you haven't installed the SELinux policy analysis command line tools package (setools-console) and try to install the SELinux configuration tool package (policycoreutils-gui), you'll get the following message (version numbers may vary):

```
# rpm -i policycoreutils-gui-2.0.83-19.1.el6.x86_64.rpm
error: Failed dependencies:
 policycoreutils-python = 2.0.83-19.1.el6 is needed by policycoreutils-gui-2.0.83-19.1.el6.x86_64
 setools-console is needed by policycoreutils-gui-2.0.83-19.1.el6.x86_64
```

One way to test this is to mount the RHEL 6 DVD with the mount /dev/cdrom /media command. Next, find the noted policycoreutils-gui package in the Packages/ subdirectory. Alternatively, you could download that package directly from the Red Hat Network or a configured repository with the yumdownloader policycoreutils-gui command. This and other yum commands are discussed later in this chapter. Just be aware, some Linux GUI desktop environments automatically mount CD/DVD