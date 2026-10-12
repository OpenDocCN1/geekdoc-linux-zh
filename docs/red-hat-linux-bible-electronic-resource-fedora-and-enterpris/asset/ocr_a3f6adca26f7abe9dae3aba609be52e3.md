command to print and the `lpc` command to see a printer queue. Both Postfix and Sendmail have a `newaliases` command and `mailq` commands for updating aliases and checking the mail queue, respectively.

So, to the user, a change in mail or printing services should (in theory) be nearly invisible. Users can print documents using the same commands they always used and the documents will be printed. Users can send mail as they always did and the fact that a different mail transport is being used should make no difference.

# Getting Linux Software "up2date"

The `up2date` facility is the preferred method from Red Hat, Inc. for updating Fedora and Red Hat Enterprise Linux software. Using `up2date`, you can determine if any software packages in your Linux distribution have updates available, and you can ask to have them downloaded and installed automatically.

Fixes and improvements continue after a distribution, such as Fedora Core or Red Hat Enterprise Linux, is released. You can incorporate those fixes and features into Red Hat Linux, using a connection to the Internet and `up2date`.

This section tells you how to determine which updates are available to your Red Hat Linux system. Then it describes how you can register to use the Red Hat Network and use the `up2date` tool to gather those updates.

> **NOTE:** The `up2date` service is used for getting fixes to your Red Hat Linux system. It is not used to pick up every change that occurs to the software packages included with Red Hat Linux.

With the transition from Red Hat Linux to Fedora and Red Hat Enterprise Linux, changes in what `up2date` supports are among the most significant changes to the latest distributions from Red Hat. In particular, `up2date` has been modified to allow you to not only download software from Red Hat FTP sites, but also from repositories of software built to work with the `apt` and `yum` facilities.

> **CROSS REFERENCE:** For detailed descriptions of `apt` and `yum`, refer to Chapter 5.

# Getting updates from the Red Hat Network

Red Hat has created a system that automatically notifies you of available updates and lets you easily download and install them on your Red Hat Linux system. The service is called Red Hat Network. Registering with the Red Hat Network allows you to run the `up2date` program from your Red Hat Linux computer whenever you are ready to do the updates.

Red Hat Network provides a mechanism that can:

+   * Alert you to the latest fixes and enhancements available for Red Hat Linux.