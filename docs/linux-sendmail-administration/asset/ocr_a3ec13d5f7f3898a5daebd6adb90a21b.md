Take advantage of the tools your Linux system offers. However, if you are forced to upgrade with source code a system that was originally installed via RPM, you should clean out the RPM installation before upgrading.

The next section describes downloading and compiling the latest Sendmail source code. Before installing a new version of Sendmail that you have downloaded and compiled, remove the old RPM version with the --erase option, in this example:

```
[root]# rpm --erase --nodelops sendmail-cf-8.9.3-1
[root]# rpm --erase --nodelops sendmail-8.9.3-1
```

The --nodelops option is used to command line to erase the Sendmail software, even when other packages are dependent on it. Attempting to erase Sendmail without using the --nodelops option displays an error message stating that other software depends on Sendmail, and it is not removed, as shown below:

```
[root]# rpm --erase sendmail
```

removing packages would break dependencies:
sendmail is needed by sendmail-cf-8.9.3-1

Failure to remove the Sendmail RPM package before installing a non-RPM version, such as a version you compile yourself, the system will still think the old RPM version is installed. An rpm --query continues to report the old RPM version number. If the -V option is used to verify the Sendmail RPM package, it may report false and misleading errors. Here is an example of what can happen when the components of Sendmail are changed or upgraded without using RPM and are verified by the rpm command:

```
[craig]$ rpm -V Sendmail
S.5...Tc /etc/aliases
missing /etc/rc.d/rc.2/S80sendmail
S.5...T /var/log/sendmail.st
```

The -V option prints out a line for each file in the package that fails verification. Values are printed at the beginning of the line to indicate which tests were failed. Each letter or number indicates a failure and each dot indicates a test that was passed. The possible values are as follows:

+   - S indicates that the file has the wrong file size.
- M indicates that the file is assigned the wrong file permissions or file type.
- S indicates that the file has an incorrect MD5 checksum.
- D indicates that the file is located on the wrong device.