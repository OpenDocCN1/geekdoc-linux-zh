20. Which of the following commands can be used to search for packages that contain the word \"oobla\" on RPM software repositories?

+   a. yum search oobla

+   b. rpm -qS oobla

+   c. yum list oobla

+   d. rpm -qI oobla

# Hands-on Projects

![](bbox=[0.1, 0.29, 0.25, 0.34])

These projects should be completed in the order given. The hands-on projects presented in this chapter should take a total of three hours to complete. The requirements for this lab include:

+   A computer with Fedora Linux installed according to Hands-on Project 2-1 and Ubuntu Server Linux installed according to Hands-on Project 6-1.

# Project 11-1

In this hands-on project, you use common compression utilities to compress and decompress information on Fedora 20.

+   1. Boot your Fedora Linux virtual machine. After your Linux system has been loaded, switch to a command-line terminal (tty2) by pressing Ctrl+Alt+F2 and log in to the terminal using the user name of root and the password of LNXrocks!

+   2. At the command prompt, type `yum install ncompress` and press `Enter`. Press `y` when prompted to complete the installation of the `ncompress` RPM package (and any package dependencies).

+   3. At the command prompt, type `cp /etc/services ~` and press `Enter` to make a copy of the `/etc/services` file in your home directory. Next, type `ls -l` at the command prompt and press `Enter`. How large is the services file?

+   4. At the command prompt, type `compress -v services` and press `Enter` to compress the services file. What was the compression ratio? Next, type `ls -l` at the command prompt and press `Enter`. What extension does the services file have and how large is it?

+   5. At the command prompt, type `uncompress -v services.Z` and press `Enter` to decompress the services file.

+   6. At the command prompt, type `cp /etc/hosts /etc/initab Desktop` and press `Enter` to copy the `hosts` and `initab` file to your `Desktop` subdirectory.

+   7. At the command prompt, type `compress -vr Desktop` and press `Enter` to compress the contents of the `Desktop` subdirectory. Next, type `ls -lr Desktop` at the command prompt and press `Enter` to view the contents of the `Desktop` directory. Which files were compressed? If there were symbolic links in this directory, how could you force the compress utility to compress these files as well?