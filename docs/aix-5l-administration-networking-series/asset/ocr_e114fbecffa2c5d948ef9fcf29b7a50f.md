# Event Recovery and Retry

You can specify a script or AIX command to execute to attempt to recover from a cluster event command failure. If the recovery command succeeds and the retry count is greater than zero, the cluster event command is rerun. The arguments passed to this command are the event name and the arguments passed to the event command.

You can also specify the number of times to run the recovery command. Set the Recovery Counter field to one (1) or greater if a recovery command is specified.

# Customized Event Duration

In HACMP 4.5, you can use SMIT to customize the time period allowed for a cluster event to complete before HACMP issues a system warning for it. Prior to HACMP 4.5, the timeout period was set to six minutes by default and could be changed only using the command line. If a cluster event lasted longer than six minutes, then every 30 seconds HACMP automatically issued a `config_too_long` warning message that was logged in the `/tmp/hacmp.out` file.

# Automatic Error Notification

HACMP builds on the AIX error notification feature by providing a means of automatically turning on prespecified error notification methods for certain failures. This can be done in one step through the SMIT interface, saving the time and effort normally spent defining each notify method manually. The predefined notify methods are automatically enabled on all nodes in the cluster for the following devices:

+   * All disks in the rootvg volume group
+   * All disks in HACMP volume groups, concurrent volume groups, and filesystems. (To avoid single point of failure, the JFS log must be included in an HACMP volume group.)
+   * All disks defined as HACMP resources
+   * SP switch adapter

# Custom Pager Notification

You can define a notification method through the SMIT interface to issue a customized page in response to a cluster event. In version 4.5, you can send a test message after configuring a pager notification method to confirm that the configuration is correct.

You can configure any number of notification methods, for different events and with different text messages and telephone numbers to dial. The same notification method can be used for several different events, as long as the associated test message conveys enough information to respond to all of the possible events that trigger the page.