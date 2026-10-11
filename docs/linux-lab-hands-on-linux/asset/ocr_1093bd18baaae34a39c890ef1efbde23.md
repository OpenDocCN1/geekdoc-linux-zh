+   - The `-h` option makes rpm to display progress meters, which is as follows:
+     - `# rpm -ivh evolution-2.0.4-6.src.rpm`

# ## Querying Software

Querying is the process to make enquiry on the software packages and check whether the RPMs are installed. This process in undertaken after the software is installed. So, we can say that querying performs two functions, which are as follows:

+   - Enquiring of the software packages
+   - Verifying the installed software packages

Let’s learn about these in detail one by one.

# ## Enquiring of the Software Packages

The enquiry of the installed software packages can be done using the following command:

```
`[root@localhost ~]# rpm -q`
```

If the details about the software packages, such as the name, version and release number of the installed software package has to be displayed, then the following command can be used:

```
`[root@localhost ~]# rpm -q < package name>`
```

# # Verifying the Installed Software Package

Verification is done to check whether the software packages are installed successfully or not. The command used to verify a software package is as follows:

```
`[root@localhost ~]# rpm -V`
```

The command used to verify a software package having a specific file is as follows:

```
`[root@localhost ~]# rpm -vf /usr/home/user1`
```

The command used to verify all installed software packages is as follows:

```
`[root@localhost ~]# rpm - va`
```

# # Removing Software

Software can be removed or uninstalled using RPM. The software, which is not in use currently, has to be removed so that the space occupied by it is saved for other programs. Software can be uninstalled using RPM on a command line and graphical interfaces.