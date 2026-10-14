+   6. Which option to the `rpm` command can be used to uninstall an RPM package?
+      a. `u`
+      b. `e`
+      c. `r`
+      d. `x`

7. What command will list the files in the installed bash RPM package? ____________________

+   8. Which of the following commands will install an RPM package? (Choose all that apply.)
+      a. `rpm -U packagename`
+      b. `rpm -i packagename`
+      c. `rpm -e packagename`
+      d. `yast -i packagename`

# ## Discovery Exercises

![](bbox=[0.035, 0.444, 0.22, 0.516])

# ### Installing RPM Software Packages

Use the Internet to find an RPM package that has been compiled for use on SUSE Linux. (Some common Internet resources include http://rpmfind.net/linux/RPM/ and http://rpm.pbone.com.) Next, use the appropriate command to verify that the package has not already been installed. Following this, download the RPM package, install it on your system, and use the appropriate commands to view the files installed and version information. When finished, use the appropriate commands to remove the software package from your system.

# ### Installing Software Packages from Source

Although most software packages for SUSE Linux are available in RPM format, you can also download and install software from source code that is freely available on the Internet. Use the Internet to find the source code for a program that you do not have installed on your system (the best Internet resources for source code is http://sourceforge.net/). Following this, download the source code (with a .tar.gz or .tgz extension) and extract it using the command `tar --zxvf filename`. Enter the directory that was created and run the following commands to compile and install the software on your system:

```
```bash
./configure
make
make install
```
```

Although these steps will work for most source code programs, additional steps might be required. Read the README and INSTALL files in the source code directory to learn more about how to compile and install the program that you have downloaded. When finished, execute your program.