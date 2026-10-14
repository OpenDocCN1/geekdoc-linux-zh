If this module is available, you will see only the word “Success!” printed on the next line. If the module is not installed, a number of errors will result instead. If you have success with the module check, proceed to the next section. If not, visit the Comprehensive Perl Archive Network (CPAN for short) at [http://www.cpan.org]. Use the search function to find the latest version of Authen-PAM. download it, and follow the instructions in the README file that is included. Briefly, all CPAN Perl modules are installed in the same simple way. First generate a makefile by running the Makefile.PL file, as follows:

```
[root@grover Authen-PAM-0.13]# perl Makefile.PL
```

If successful, run make and make install.

```
[root@grover Authen-PAM-0.13]# make
[root@grover Authen-PAM-0.13]# make install
```

Next, use the Perl command suggested at the beginning of this section to test for the availability of the module. Then add a PAM service called usermin in the appropriate location. Under many Linux distributions, this involves creating a file named /etc/pam.d/usermin that contains the following:

```
#%PAM-1.0
auth       required     pam_unix.so      shadow nullok
account    required     pam_unix.so
password   required     pam_unix.so      shadow nullok use_authtok
session    required     pam_unix.so
```

Now the installation of Usermin should proceed smoothly.

**NOTE** You may be able to download a package of Authen-PAM for your operating system, which is usually preferable from a system maintenance perspective. Also, if you use an RPM-based Linux distribution, you may be able to use cpan2rpm or cpanflute2 to automatically generate a package from the Perl module, if your vendor doesn’t provide a package for you. The use of cpanflute is not discussed in this book. However, it is worth looking into if you frequently install Perl modules, because it makes generating Perl module RPMs a simple and painless process.

# Obtaining Usermin

Lucky for us, Usermin is free under a BSD-style license, just like its more powerful sibling. It can be downloaded for free from the Usermin site or one of its mirrors. For reference the primary Usermin site is [http://www.usermin.com]. Like Webmin, Usermin is available in a tarball, as well as an RPM for Red Hat, MSC Linux, Caldera, Mandrake, and SuSE. Unlike Webmin, there is currently no Solaris package of Usermin. Choose the most appropriate option for your system.