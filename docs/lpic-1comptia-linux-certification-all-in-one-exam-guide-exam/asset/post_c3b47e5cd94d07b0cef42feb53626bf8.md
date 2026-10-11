
## Verifying Packages

In addition to querying packages, the rpm utility can also be used to verify packages on your system. As you are probably (painfully) aware, software can get corrupted, deleted, or otherwise messed up on any given computer system, regardless of the operating system. You can use the rpm utility to verify your installed packages and make sure everything is working the way it is supposed to. This is done using the -V option.

You can use -V to verify a single package by specifying its package name, such as `rpm -V gftp`. You can also verify all packages on the system by entering `rpm -Va`. Regardless of which option you choose, rpm will return no output if no errors are found. In the next example, the `rpm -V gftp` command was issued at the command prompt. Because the package had no errors, nothing was written to the screen and the rpm utility exited.

```bash
ws1:~ # rpm -V gftp
ws1:~ #
```

If an error does occur, rpm prints out the error message and the associated filename, as shown here:

```bash
ws1:~ # rpm -Va
S.5....T.  c /etc/xinetd.d/vnc
S.5.....T.  c /etc/sane.d/dll.conf
S.5.....T.  c /etc/maven/maven2-demap.xml
-M......  c /etc/cups
S.5....T.  c /etc/environment
....L....  c /etc/pam.d/common-account
....L....  c /etc/pam.d/common-auth
....L....  c /etc/pam.d/common-password
....L....  c /etc/pam.d/common-session
```

The error messages generated during the verification process follow the syntax of `SMD5DLUGT` c `filename`.

The parameters in the error message stand for the following:

- S Indicates a problem in the size of a file
- M Indicates a problem with a file’s mode
- 5 Indicates a problem with the MD5 checksum of a file
- D Indicates a problem with a file’s revision numbers
- L Indicates a problem with a file’s symbolic link
- U Indicates a problem with a file’s ownership
- G Indicates a problem with a file’s group
- T Indicates a problem with the modification time of a file
- c Indicates the specified file is a configuration file
- `filename` Specifies the name of the file that failed verification

In the example we looked at earlier, any one of the preceding letters is represented by a period (.) in the output; it indicates that no problem was found with this parameter for the specified file. A letter displayed indicates a problem was found for this particular parameter for the specified file. For example, the `/etc/xinetd.d/vnc` file had errors S, 5, and T, indicating there was a problem with the size, checksum, and modification time of the file. We also know that it is a configuration file because there’s a c on the line as well.

In the example, notice that most of the errors encountered by rpm were associated with configuration files. This actually isn’t a problem. Configuration files, naturally, get modified all the time and, hence, may fail to verify.

However, if other files, such as executables, fail to verify, then you should be more concerned. Based on the output from `rpm -V`, you may determine that you need to repair an installed package. You can use `rpm` to do this as well, using the `--U --replacepkgs` option. For example, if I determined that I needed to reinstall the gFTP package, I could enter `rpm --U --replacepkgs gftp-2.0.19-7.1.x86_64.rpm` at the shell prompt to force `rpm` to install the gFTP package from the original `rpm` even though it is already installed.

## Extracting files from packages

From time to time, you may need to extract one or more individual files from a package file. One option for doing this is the rpm2cpio utility. This command takes an RPM package file and converts it to a cpio archive.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_337_0.png)

> NOTE We'll discuss how to work with cpio archives in Chapter 10. For now, just think of a cpio archive as the equivalent of a tar archive or a zip file.

The syntax for using rpm2cpio is as follows:

```bash
rpm2cpio package_name > archive_filename
```

For example, if you needed to get a file out of the gFTP rpm package, you could convert it to a cpio archive using the following command:

```bash
rpm2cpio gftp-2.0.19-7.1.x86_64.rpm > gftp.cpio
```

You could then extract the file you need from the cpio archive created using the cpio utility. We'll talk about how to do this in a later exercise.

Let's practice managing RPM packages in the following exercise.

### Exercise 8-4: Managing RPM Packages

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_337_1.png)

> VIDEO For more information watch *Exercise 8-4*.

In this exercise, you will practice managing RPM packages installed on your system. Complete the following:

1. With your system running, open a terminal session.
2. If necessary, change to your root user account by entering `su` - followed by your root user's *password*.
3. List all of the RPM packages installed on your system by entering `rpm -qa` at the shell prompt.
4. View information about the rpm utility itself by entering `rpm -qi rpm`.
5. Identify packages that require the rpm package by entering `rpm -q --whatrequires rpm`. What packages require rpm?
6. Identify components required by the rpm utility by entering `rpm -q --requires rpm`. What is required by rpm?
7. One of the components required by rpm is `libz.so.1`. Determine what package provides this component by entering `rpm -q --whatprovides libz.so.1`. What package provides this component?

## Using yum to Install RPM Packages

In addition to rpm, you can also use the yum command at the shell prompt to install RPM packages. The yum (Yellowdog Updater Modified) command is just a front end to rpm, but it has several key advantages over using rpm alone:

- It allows you to install a package *and* all of its dependencies with a single command. This is huge! Managing dependencies can be a real problem when installing packages with rpm. It’s called “dependency hell.” Here’s what happens: You decide you want to install package X with rpm at the shell prompt. However, when you run the command, you’re informed that package X is dependent upon packages Y and Z; you must install these packages first. So, you download and then try to install packages Y and Z with rpm. Again when you do, you discover that Y is dependent upon packages A, B, and C while package Z is dependent upon packages E, F, and G. Of course, you then discover packages A, B, C, E, F, and G all have dependencies of their own. Before you know it, you’re installing 20 or more separate packages just to get package X installed on your system. What a nightmare! This is where yum really shines! The yum command busts you out of your dependency hell by automatically calculating and installing all of the dependent packages for you.

- It locates packages for you by searching one or more repositories on the Internet. Again, this is a key strength of yum. I can’t tell you how many hours I’ve wasted (before I learned about yum) trying to find version 3.5 of a particular package to meet a dependency requirement and only being able to find version 3.3. With yum, there’s no more digging around the Web trying to find the right package to resolve a dependency issue. It takes care of everything for you.

Once you start using yum, you may never use rpm again! When run from the command prompt, yum finds the latest version of the requested package, downloads it, installs its dependencies, and then installs the requested package itself.

> **CAUTION** The yum utility is not supported by all distributions. It was originally developed for Red Hat systems, so it’s supported well by Red Hat and Fedora. It’s not installed by default on openSUSE but can be installed manually.

The basic syntax for using yum is as follows:

```bash
yum option command package_name
```

Common yum commands are shown in Table 8-1.

For example, in Figure 8-10 the `yum install gcc` command has been entered at the shell prompt to install the GNU C Compiler package on a Fedora system. The yum utility searches the repositories it’s been configured to use, locates the latest gcc package, calculates dependencies, installs dependencies, and then installs the gcc package.
