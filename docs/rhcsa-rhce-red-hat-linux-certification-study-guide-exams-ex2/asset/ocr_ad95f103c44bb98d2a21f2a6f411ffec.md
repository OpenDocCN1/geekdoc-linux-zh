6. The file that lists the RPMs installed when you first installed the local system is /root/install.log. The /var/log/rpmpkgs file is complete but is updated only once per day.

7. If you've downloaded an RPM from a third party, call it third.i386.rpm, you'll first need to download and install the RPM-GPG-KEY file associated with that repository. You can then validate the associated package signature with a command like (note the uppercase -K; --checksig is equivalent to -K.

```
# rpm -K third.i386.rpm
```

# Dependencies and the yum Command

8. The yum command repositories are normally configured in files in the /etc/yum.repos.d directory. Technically, yum command repositories can also be configured directly in the /etc/yum.conf file.

9. The yum whatprovides /etc/passwd command identifies packages associated with that file.

# More Package Management Tools

10. This is a slightly tricky question, as the yum grouplist command lists the package groups also shown in the Add/Remove Software tool.

11. Allowable time periods for updates, as defined by the Software Update Preferences tool, are hourly, daily, and weekly.

12. The rhn_register command starts the process of registering a system on the RHN.

# LAB ANSWERS

# Lab I

When complete, run the following commands to verify the connection:

```
# yum clean all
# yum update
```

The output should include output similar to the following:

```
Loaded plugins: refresh-packagekit
inst | 3.7 kB 00:00 ...
inst/primary_db | 2.3 MB 00:00 ...
Setting up Update Process
```