![](bbox=[0.154, 0.155, 0.841, 0.373])

Figure 9.5 - Executing sp.pl

# ### 9.4 Exercises

#### Exercise #1

In this exercise, you will setup a Perl DB2 environment on a SUSE Linux Enterprise Server 10 SP1, assuming a valid DB2 V9.7 product has been installed first. Please note that you have to be the `root` user to perform the setup. The setup procedure is similar if you are using other operating systems.

+   1. Install Perl 5.8 or later.
+      - Perl 5.8.8 comes with the standard installation of SUSE Linux Enterprise Server 10 SP1, so it's not required to install the Perl language environment separately in this exercise.
+   
+      You can run the following command in the shell to check the version of your Perl language:
+   
+      `perl -v`
+   
+      If your version of Perl is lower than 5.8, follow *section 9.2* on how to install Perl language on your platform.
+   2. Install the Perl DBI module
+      - Download the latest Perl DBI source file from http://search.cpan.org/~timb/DBI/
+   
+      At the time of this writing, the latest version of DBI source is `DBI-1.611.tar.gz`
+      - Login to the Linux server as the `root` user and perform the following commands in the directory where the source file `DBI-1.611.tar.gz` is located:
+   
+   ```
+     tar xvzf DBI-1.611.tar.gz
+     cd DBI-1.611
+     perl Makefile.PL
+   ```