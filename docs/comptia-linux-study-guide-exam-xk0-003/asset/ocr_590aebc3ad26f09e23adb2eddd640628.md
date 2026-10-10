Checksum programs are often used on the Internet at large to help users spot corrupt file downloads. A program author may provide a tarball, RPM, or CD-R image file along with an MD5 sum. You can then check the file you download to be sure its MD5 sum matches what the author has posted. If it doesn't match, you can check your download settings (to be sure you're using FTP binary mode, for example), try again and, if the problem persists, report it to the program's author.

# ## Using Package Manager Checksums

Package managers—most notably the RPM Package Manager (RPM)—maintain checksums on all their installed packages. As such, they can be used as intrusion detection tools. In particular, the **-V** (or **--verify**) option to `rpm` performs a package verification:

```
```
# rpm -V postfix
S.5....T c /etc/postfix/main.cf
S.5....T c /etc/postfix/sasl_passwd
S.5....T c /etc/postfix/sender_canonical
```
```

Each line of output reports files that have changed in some way. The first eight characters of the output lines report what has changed: the file size, mode, MD5 sum, device major or minor numbers (for device files), link path mismatch, user ownership, group ownership, or time. A dot (.) in a position indicates that a test passed; any other character denotes a change (the character used depends on the test and is intended to be mnemonic). Following the eight-character block may be another character that denotes the file type—**c** for configuration files, **d** for documentation, **g** for “ghost” files (those not included in the actual package), **l** for a license file, or **r** for a **README** file. Files that haven't changed are *not* displayed in the output.

In the preceding example, three files have changed: `main.cf`, `sasl_passwd`, and `sender_canonical`. All three files are marked as configuration files (the c characters preceding the filenames), and all three have changed file sizes, MD5 sums, and times. Because these are configuration files, these changes aren't particularly suspicious, but a similar pattern of changes in program executables would be cause for concern. Changes to the MD5 sum (the form of checksum used by RPM) are particularly likely to be the result of tampering; they indicate that the file's contents have changed compared to the file in the original package. Time stamp changes can sometimes be completely innocent. Ownership and permissions changes might be the result of unwanted tampering or could be innocent in some cases (say if you've deliberately removed world execute permission to improve security).

You can verify an individual package by providing a package name, as in the preceding example. You can also verify all the packages installed on a system by passing the **-a** option. The result is likely to be a very long list, though, because so many packages include configuration files and other ancillary files that are normally changed. You might want to pass the output to a file that you can peruse later, as in `rpm -Va > rpm-test.txt`.