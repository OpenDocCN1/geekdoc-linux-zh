# Chapter 14 - Setting Ownership and Permissions

root Many of the permission rules do not apply to root. The superuser can read or write any file on the computer—even files that grant access to nobody (that is, those that have 000 permissions). The superuser still needs to execute bit set to run a program file.

The procedure for setting permissions in a file manager is similar to that for setting the ownership of a file:

+   - You normally adjust these settings using the same dialog box used to adjust ownership, such as the Nautilus dialog box shown earlier in Figure 14.1.

+   - You don't need to be root to adjust the permissions of files that you own.

+   - You should use root access for this job only on files that you own.

As seen in Figure 14.1, there are three Access items associated with the Owner, the Group, and Others:

+   - The Owner item provides two options: Read-Only and Read and Write.

+   - The Group and Others items both provide Read-Only and Read and Write plus the None option. You can use these options to set the read and write permission bits on your file.

Nautilus requires setting the execute bit separately, by selecting the Allow Execution As Program check box. This check box sets all three execute permission bits; you cannot control execute more precisely with Nautilus. You cannot adjust the execute permissions on directories with Nautilus.

# Setting Permissions in the Shell

In a text-mode, you can use chmod to change permissions. This command is rather complex, mostly because of the complex ways that permissions may be changed. You can specify the permissions in two forms: as an octal number or in a symbolic form, which is a set of codes representing the string representation of the permissions.

The octal representation of the mode is the same as that described earlier and summarized in Table 14.2. For instance, to change permissions on report.tex to r-w---, you can issue the following command:

```
$ chmod 644 report.tex
```