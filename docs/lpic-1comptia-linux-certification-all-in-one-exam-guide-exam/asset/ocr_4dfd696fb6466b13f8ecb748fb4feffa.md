# **Exercise 8-3: Uninstalling RPM Packages**

![](bbox=[0.15, 0.12, 0.79, 0.19])

In this exercise, you will practice uninstalling the `gftp` client you installed in the previous exercise. Complete the following:

+   1. With your system running, open a terminal session.
+   2. If necessary, change to your root user account by entering `su –` followed by your root user's *password*.
+   3. At the shell prompt, enter `rpm -e gftp`. You should see a message indicating that `gftp` has been erased.

Let’s next discuss how you can update RPM packages.

# ### Updating Software

The ability of the `rpm` utility to manage dependencies is a real time saver. However, it brings up the issue of updates. What if you have a package installed that needs to be updated, but it has many other packages that are dependent on it? Do you have to uninstall all of them before you can update the package? That would be a real pain!

Fortunately, this isn’t the case. The `rpm` utility can be used to update an existing package without having to uninstall all of its dependent packages. This is done using the `-U` option with `rpm`. Using this option, the `rpm` utility will remove any existing older packages and then install a newer version of the package. For example, suppose you had an older version of `gftp` installed on your system and wanted to upgrade to version 2.0.19. To do this, you would enter `rpm -U gftp-2.0.19-7.1.x86_64.rpm` at the shell prompt. Here is an example:

```
```console
ws1:/home/tux/Downloads # rpm -Uhv gftp-2.0.19-7.1.x86_64.rpm
Preparing...                          ########################################### [100%]
   1:gftp                               ########################################### [100%]
ws1:/home/tux/Downloads #
```
```

> > **TIP** If you try to use the `-U` option to update a package that hasn’t actually been installed yet, rpm will just install it. In fact, I actually just use `-U` all the time, regardless of whether I’m installing or updating a package. You can also use the `-h` and `-v` options with `-U` to display a progress indicator.

Let’s next discuss how you can query packages installed on your system.

# ### Querying Packages

In addition to installing and upgrading packages on your system, the `rpm` command can also be used to query packages for information. This can be done using the `-q` (for *query*) option with `rpm`. Using the `-q` option, you can list all the packages installed on