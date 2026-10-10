repositories, and then setting up a local repository to save downloading these for a number of machines on your network. When you have downloaded the packages, you need to generate the correct information for a repository. This is achieved using the `createrepo` utility, which extracts all the data from the rpm files to generate the necessary metadata for yum. The command to create the metadata from the rpm files in the /rpm_directory is as follows:

```
Createrepo /rpm_directory
```

This can then be included into its own file in the /etc/yum.repo.d directory.

# Adding a Repository in Debian

The method of adding a repository that uses the APT packaging tool is different. The file /etc/apt/sources.list contains a list of available software repositories, and it can be updated manually or (if installed) by a graphical manager tool. If you want to add a new repository manually, the format to follow is: package type, Web address (URL), distribution, and section. For example, one of the lines in sources.list could be

```
deb http://security.debian.org/ lenny/updates main contrib
```

# EXERCISE 7.3: Adding a New Software Repository

You want to add a repository you know exists at ftp://ftp.nerim.net/debian- marillat/. This is achieved by

+   1. Opening the file /etc/apt/sources.list using your favorite editor, such as vi.

+   2. Adding in the line:

```
deb ftp://ftp.nerim.net/debian-marillat/ etc main
```

+   3. Save and exit from the editor.

+   4. You have now added the new repository to your system.

# SUMMARY OF EXAM OBJECTIVES

Within this chapter, you learned how to download and install applications using a variety of methods, both from binary packages and using source code. Initially, we looked at the software package formats that you will most likely encounter on the Linux systems you are administering – RPM and DEB packages. The RPM format of software packages was developed by Red Hat