| User | Description |
|---|---|
| dave | This user handles all the tape backups and may only run the BACKUP commands on the machine nebo and the DUMP commands on the machine granite. |
| greg | He can only run the SHELLS commands on machines situated on the LAN. |

# ## Understanding sudo's Advantages over Root Access

Using the sudo program offers distinct advantages over simply giving out root access. As you can see from the preceding example, each user's needs are tailored to their specifications and classifications. Users can be added to categories and removed when they leave. There is room for growth and leniency for making modifications to the file. Removing a person's privileges is simply a matter of commenting out a line.

The sudo program also provides other features, such as the timeout option, which will prompt a user for a password again if he or she allows a certain time to elapse with no input. Normally, you can issue any and all sudo commands without having to type a password after logging in, but if you allow a certain length of time to lapse without typing in any more commands, the password check feature will reassert itself. This prevents unauthorized users from logging in to unattended terminals.

You can also track user activity by logging commands to syslog. This lets the administrator see exactly what was done when a user has made a mistake. This option not only tells the administrator which users are to blame, but can exonerate users as well. In addition, if users issue a sudo command that they are not authorized to invoke, a warning message appears and sudo sends an email message alerting the administrator of an illegal attempt to use a nonvalid sudo command.

The advantages that using sudo has over sharing root access are as follows:

+   * A single file controls all access to systems on and off the network.
+   * The timeout option can decrease the chances of a user leaving root unattended.
+   * The program maintains a list all users and their privileges, tracking who can do what.