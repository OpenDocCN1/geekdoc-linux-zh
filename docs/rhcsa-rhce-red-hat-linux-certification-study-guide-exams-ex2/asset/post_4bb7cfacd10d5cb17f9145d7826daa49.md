
You should then be able to create partitions and more on the new /dev/sg3 drive just as if it were a local drive, based on the techniques discussed in Chapter 6. Of course, a "persistent mount" as described in the relevant RHCE objective requires that you make sure the iSCSI service starts the next time the system is rebooted with a command like

```
# chkconfig iscsi on
```

To make sure there's an actual mount, you may also need to set up a partition that's actually mounted in the /etc/fstab file. In practice, the actual device file for the iSCSI drive may vary on each reboot. Therefore, such mounts should be configured with the Universally Unique Identifier (UUID) numbers described in Chapter 6.

You do not need to create an iSCSI target storage server for the RHCE exam. But as the configuration of an iSCSI server is relatively simple, you might consider creating one for that purpose. Red Hat developer Daniel Berrangé has created an excellent introduction to the creation of an iSCSI storage server at http://berrange.com/tags/tgtadm/.

## SCENARIO & SOLUTION

| Scenario | Solution |
|---|---|
| You need to set up a daily task to back up files in the /home directory | Set up a script in the /etc/cron.daily directory with appropriate backup commands to copy files from /home. |
| You've been told to set up IPv6 forwarding on a system | Include the net.ipv6.conf.all.forwarding=1 setting in /etc/sysctl.conf, and activate it with the sysctl -p command. |
| You need to set up source code for a single-file RPM | Set up the single file, along with an executable configure script in a dedicated directory; then set it up in a compressed tar archive. |
| You need to set up a special static route over device eth1 | Use the Network Connections tool to set up that special route, given the network address, subnet mask, and desired gateway IP address. |
| You need to set up a system as a Kerberos client | Use the GUI Authentication Configuration tool; the realm should be the uppercase listing for the domain. You'll also need the FQDN for the KDC and Kerberos administration servers (which may be the same). |
| You need to set up an iSCSI initiator | Install the iscsi-initiator-utils package, use the iscsiadm command to discover available iSCSI targets, and make sure the iscsi service is active on reboot. |

## CERTIFICATION SUMMARY

Linux administrators need to configure scripts on a regular basis. Sample scripts are already available in different /etc/cron.* directories. Normally, scripts start with the #!/bin/bash line, which sets up the language for the rest of the script. Administrative scripts can use bash commands, along with operators such as for, if, do, and test. Kernel run-time parameters can be found in the /proc/sys directory. But changes to such files are temporary. For more permanent changes, you'd set up options in the /etc/sysctl.conf file. Changes to that file can be implemented with the sysctl -p command. Many standard options relate to networking.

One new RHCE requirement is to create an RPM from a single file. To do so, you need to know how to set up a source-code archive. The rpmdevtools and rpm-build packages can help. The rpmdev-setuptree command can help set up the needed directories. The rpmdev-newspec command can help create a template for a .spec file. The rpmbuild command can then be used to process the instructions in the spec file along with the packaged source code into an SRPM and an RPM package that can be installed on different systems.

The RHCE objectives include requirements for several special network options. With the help of the Network Connections tool, special IP routes can be configured in a file in the /etc/sysconfig/network-scripts directory. Kerberos clients can be configured in the /etc/sssd/sssd.conf file, referenced through the /etc/nsswitch.conf file. Perhaps the easiest way to configure a Kerberos client is with the GUI Authentication Configuration tool.

## TWO-MINUTE DRILL

Here are some of the key points from the certification objectives in Chapter 12.

### Automate System Maintenance

- [ ] Standard administrative scripts can provide a model for custom scripts to automate system maintenance tasks.
- [ ] Various command operators within scripts include do, for, if, and test.
- [ ] Many Linux administrative scripts start with #!/bin/bash, a reference to the bash shell.

### Kernel Run-Time Parameters

- [ ] Kernel run-time parameters are located in the /proc/sys directory.
- [ ] Many kernel run-time parameters relate to network options such as forwarding and security.
- [ ] Kernel run-time parameters can be configured on a permanent basis with the help of the /etc/sysctl.conf file.

### Create an RPM Package

- [ ] Available source RPMs can be used as a model to help create your own RPMs.
- [ ] RPM source-code components can be found in user home directories, in the rpmbuild/ subdirectory, as configured with the rpmdev-setuptree command.
- [ ] The actual source code can be found in the rpmbuild/SOURCES subdirectory.
- [ ] RPMs are built with the rpmbuild command, based on a .spec file in the rpmbuild/SPECS subdirectory. You can create a standard .spec template with the rpmdev-newspec command.
- [ ] Built RPMs can be found in the rpmbuild/SRPMS and rpmbuild/RPMS subdirectories.

### Special Network Options

- The default network route to an outside network goes through a gateway IP address.
- Special routes to different networks can be configured through certain IP specific network devices.
- To configure a Kerberos client, you need to modify the `/etc/sssd/sssd.conf` file.
- A connection to the Kerberos client also requires a connection to a network authentication service such as LDAP.
- To configure an iSCSI client, you need the iscsi-initiator-utils package, which can be used to connect to iSCSI storage with the `iscsiadm` command.
- To make sure the iSCSI connection survives a reboot, you'll need to activate the iscsi service.

![](img/9139201cfcaf4292284a0eed074928e5_711_0.png)

## SELF TEST

The following questions will help measure your understanding of the material presented in this chapter. As no multiple-choice questions appear on the Red Hat exams, no multiple-choice questions appear in this book. These questions exclusively test your understanding of the chapter. It is okay if you have another way of performing a task. Getting results, not memorizing trivia, is what counts on the Red Hat exams.

### Automate System Maintenance

1. What exit number is associated with success in a script?

2. What operator means "anything but"?

### Kernel Run-Time Parameters

3. What’s the full path to the file associated with the net.ipv4.ip_forward parameter?

### Create an RPM Package

4. When source code is installed from an SRPM by user stephanie in her home directory, what is the full path to the actual source code?

5. What’s the name of the package with a command that can be used to create a spec file template?

6. What common file is needed in a source-code directory to process standard source-code packages? Bonus: what should be different about permissions on that file, when compared to a regular file?

7. What command can be used to create just a regular RPM from source code, based on the test.spec file in the rpmbuild/SPECS subdirectory? Assume all required source code is in the correct location.

8. When user tim builds a regular RPM associated with 64-bit systems, what's the full path to the directory with that RPM?

### Special Network Options

9. What are the three types of IP addresses associated with a special route?

10. In what file is a Kerberos client configured?

11. What is the standard Kerberos realm for the server1.example.com system?

12. What service script that should be running on reboot on a properly configured iSCSI target?

## LAB QUESTIONS

Several of these labs involve configuration exercises. You should do these exercises on test machines only. It's assumed that you're running these exercises on virtual machines such as KVM. Red Hat presents its exams electronically. For that reason, the labs in this and future chapters are available from the CD that accompanies the book, in the Chapter12/ subdirectory. In case you haven't yet set up RHEL 6 on a system, refer to Chapter 1 for installation instructions. The answers for the labs follow the Self Test answers for the fill-in-the-blank questions.
