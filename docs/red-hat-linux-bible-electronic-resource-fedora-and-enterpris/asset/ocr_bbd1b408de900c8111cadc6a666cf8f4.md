+   * **Writing shell scripts** — I pulled in my friend, and shell script expert, Kevin Pedigo to completely overhaul the section on writing shell scripts in Chapter 12. Along with new examples, Kevin added descriptions of how to use grep, cut, tr and sed in scripts.
+   * **Improving security** — For Chapter 14, I had security expert Chuck Wolber add new sections on detecting and responding to denial-of-service, intrusion, and other attacks.
+   * **Creating certificates** — Another major enhancement Chuck made to Chapter 14 was a section on creating and obtaining SSL certificates to enable your Red Hat Linux system to provide secure communications.
+   * **A few new options** — As I go through the book, I try to add new descriptions of options to old commands. A couple of note in this edition are the description of `rpm -F` in Chapter 5 (a convenient option to update many packages at once without installing new ones) and `mount -l` in Chapter 10 (to do lazy unmounts when resources are busy).
+   * **Using Linux NFS file sharing from the MAC** — I added a procedure for configuring NFS in Linux (Chapter 26) so that a MAC OS X computer can use a shared NFS directory from the Linux machine.

Besides these sections, procedures throughout the book have been tested and corrected to match changes that have occurred to Red Hat Linux software in this version.

# # Conventions Used in This Book

Throughout the book, special typefaces indicate code or commands. Commands and code are shown in monospace type:

```
This is how code looks.
```

In the event that an example includes both input and output, monospace is still used, but input is presented in bold type to distinguish the two. Here is an example:

```
$ **ftp ftp.hansonhistory.com**
Name (home:jake): **jake**
Password: \*\*\*\*\*
```

The following boxes are used to call your attention to points that are particularly important.

> **NOTE:** A Note box provides extra information to which you need to pay special attention.

> **TIP:** A Tip box shows a special way of performing a particular task.

> **CAUTION:** A Caution box alerts you to take special care when executing a procedure, or damage to your computer hardware or software could result.