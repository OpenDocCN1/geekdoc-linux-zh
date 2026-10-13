In general, you'd apply either the rpmbuild -ba or rpmbuild -bb command to the . spec file from the rpmbuild/SPECS subdirectory.

# Use the rpmbuild Command

If you unpacked the vsFTP source RPM described earlier, there will be a .spec file in the rpmbuild/SPECS subdirectory. The following rpmbuild command can be used to build both the source and binary RPMs for the vsFTP server, from a regular user's home directory:

```
$ rpmbuild -ba rpmbuild/SPECS/vsftpd.spec
```

In many cases, the process of building an RPM from source code requires the installation of development packages. For example, when I ran the noted rpmbuild command on the standard server1.example.com system, it cited a need for four other packages:

pam-devel is needed by vsftpd-2.2.2-6.el6.x86_64
libcap-devel is needed by vsftpd-2.2.2-6.el6.x86_64
openssl-devel is needed by vsftpd-2.2.2-6.el6.x86_64
tcp_wrappers-devel is needed by vsftpd-2.2.2-6.el6.x86_64

The GNU C Compiler package, gcc, is also required. With dependencies, several other packages will probably be required on your system. So before the noted rpmbuild command works, you should install the noted packages with a command like

```
# yum install gcc pam-devel libcap-devel openssl-devel tcp_wrappers-devel
```

Once these developmental and related compiler packages are installed, a regular user will be able to run the aforementioned rpmbuild command to compile the source code for the vsFTP server to create a binary and a source RPM.

Once the build process is complete, the compiled binary RPM can be found in the rpmbuild/RPMS/x86_64 subdirectory; of course, the last bit would vary with the architecture. The collected source RPM can be found in the rpmbuild/SRPMS subdirectory

# Create Custom Source Code

With what you now know about the build process for the vsFTP source RPM, you should be able to create a source-code package. For the purpose of this chapter, I've created a corporate_policies.pdf file. Since source code that's built into an RPM is configured as a gzip compressed tar archive that will be expanded into a directory, it