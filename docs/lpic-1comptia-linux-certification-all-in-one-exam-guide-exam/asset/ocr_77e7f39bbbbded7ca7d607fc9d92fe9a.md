If an error does occur, rpm prints out the error message and the associated filename, as shown here:

```
```
ws1:~ # rpm -Va
S.5....T.  c /etc/xinetd.d/vnc
S.5.....T.  c /etc/sane.d/dll.conf
S.5.....T.  c /etc/maven/maven2-demap.xml
-M......  c /etc/cups
S.5....T.  c /etc/environment
....L....  c /etc/pam.d/common-account
....L....  c /etc/pam.d/common-auth
....L....  c /etc/pam.d/common-password
....L....  c /etc/pam.d/common-session
```
```

The error messages generated during the verification process follow the syntax of **`SMD5DLUGT` c `filename`**

The parameters in the error message stand for the following:

+   * S Indicates a problem in the size of a file
+   * M Indicates a problem with a file’s mode
+   * 5 Indicates a problem with the MD5 checksum of a file
+   * D Indicates a problem with a file’s revision numbers
+   * L Indicates a problem with a file’s symbolic link
+   * U Indicates a problem with a file’s ownership
+   * G Indicates a problem with a file’s group
+   * T Indicates a problem with the modification time of a file
+   * c Indicates the specified file is a configuration file
+   * `filename` Specifies the name of the file that failed verification

In the example we looked at earlier, any one of the preceding letters is represented by a period (.) in the output, it indicates that no problem was found with this parameter for the specified file. A letter displayed indicates a problem was found for this particular parameter for the specified file. For example, the /etc/xinetd.d/vnc file had errors S, 5, and T, indicating there was a problem with the size, checksum, and modification time of the file. We also know that it is a configuration file because there’s a c on the line as well.

In the example, notice that most of the errors encountered by rpm were associated with configuration files. This actually isn’t a problem. Configuration files, naturally, get modified all the time and, hence, may fail to verify.

However, if other files, such as executables, fail to verify, then you should be more concerned. Based on the output from `rpm -V`, you may determine that you need to repair an installed package. You can use `rpm` to do this as well, using the `--U --replacepkgs` option. For example, if I determined that I needed to reinstall the gFTP package, I could enter `rpm --U --replacepkgs gftp-2.0.19-7.1.x86_64.rpm` at the shell prompt to force `rpm` to install the gFTP package from the original `rpm` even though it is already installed.