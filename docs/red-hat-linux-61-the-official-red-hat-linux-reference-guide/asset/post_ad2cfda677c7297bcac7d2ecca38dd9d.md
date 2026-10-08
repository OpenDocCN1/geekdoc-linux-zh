
# Chapter 19. Tripwire

Use the following command to update the Tripwire database, where name is the name of the most recent report file:

/usr/sbin/tripwire --update --twrfile /var/lib/tripwire/report/<name>.twr

Tripwire will display the report file using the default text editor specified on the EDITOR line of the Tripwire configuration file. This gives you an opportunity to deselect files you do not wish to update in the Tripwire database.

> Important
> it is important that you change only authorized integrity violations in the database.

All proposed updates to the Tripwire database start with an [x] before the file name, similar to the following example:

+   Added:
[x] "/usr/sbin/longrun"

Modified:
[x] "/usr/sbin"
[x] "/usr/sbin/cpqarray

If you want to specifically exclude a valid violation from being added to the Tripwire database, remove the x.

To edit the file editor, vi type i and press [Enter] to enter insert mode and make any necessary changes. When finished, press the [Esc] key: :wq, and press [Enter].

After the editor closes, your local password and the database will be rebuilt and signed.

After a new Tripwire database is written, the newly authored integrity violations will no longer show as warnings.

## 19.8. Updating the Tripwire Policy File

If you want to change the Tripwire files in its database, change element configuration, or modify the severity at certain violations are reported, you need to edit your Tripwire policy file.

First, make whatever changes are necessary to the sample policy file /etc/tripwire/twpol.txt. If you delete this file (as you should when you have finished configuring Tripwire), you can re-generate it by using the following command:

```
twadmin --printpolfile > /etc/tripwire/twpol.txt
```

A common change to this policy file is to comment out all files that do not exist on your system so that if your system does not have /etc/smb.conf file, you can tell Tripwire not to look for it by commenting out its line in twpol.txt with the # character as in the following example:

```
# /etc/smb.conf --= $(SEC_CONFIG);
```

Next, you must generate a new, signed /etc/tripwire/tw.pol file and generate an updated database file based on this policy information. Assuming /etc/tripwire/twpol.txt is the edited policy file, use this command:

```
/usr/sbin/twadmin --create-polfile -S site.key /etc/tripwire/twpol.txt
```

You will be asked for the password. Then, the twpol.txt file will be encrypted and signed.

It is important that you update the Tripwire database after creating a new /etc/tripwire/tw.policy file. The most reliable way to accomplish this is to delete your current Tripwire database and create a new database using the new policy file.

If your Tripwire file is named bob.domain.twd, type this command:

```
rm /var/lib/tripwire/bob.domain.twd
```

Then type the following command to create a new database using the updated policy file:

```
/usr/sbin/tripwire --init
```

To make sure the database was correctly created, run the first integrity check manually and view the contents of the resulting report. See Section 19.5 Running an Integrity Check and 19.6 Tripwire Reports for more on these tasks.

## 19.8.1. Tripwire and Email

You can configure Tripwire to send an email to one or more accounts if a specific type of policy is violated. In order to do this, you need to figure out what rules should be monitored and who should get the email when those rules broken. On large systems with multiple administrators, you may have different sets of people depending on the types of violations.

Once you have determined what and when policy to report to them, edit the /etc/tripwire/twpol.txt file, adding an emailto= line to the rule directive for each appropriate rule. Do this by adding a comma after the severity line and putting emailto= on the next line, followed by one or more email addresses. More than one email address can be specified if the addresses are separated by semicolon.

For example, if two administrators, John and Bob, need to be notified when a networking program is modified, change the Network Programs rule in the policy file to look like this:

```
rulename = "Network Programs",
severity = $SIG,
emailto = John@domain.com;bob@domain.com
```

After changing the policy, follow the instructions in Section 19.8 Updating the Tripwire Policy File to generate an updated, encrypted, and signed copy of Tripwire file.

## 19.8.1.1. Sending Test Email

To test Tripwire's email notification, use the following command:

```
/usr/sbin/tripwire --test --email@email.address
```

A test email will immediately be sent to the email address by the tripwire program.

## 19.9. Updating the Tripwire Configuration File

If you want to change Tripwire's configuration file, you should first edit the sample configuration file /etc/tripwire/twcfg.txt. If you deleted this file (whenever you finished configuring Tripwire), you can regenerate it by issuing the following command:

```
twadmin --printcfgfile /etc/tripwire/twcfg.txt
```

Tripwire will not recognize any configuration changes until the configuration text file /etc/tripwire/tw.pol is correctly signed and reverted with the twadmin command.

Use the following command to regenerate a configuration file from the /etc/tripwire/twcfg.txt text file:

```
/usr/sbin/twadmin --create-cfgfile -S site.key /etc/tripwire/twcfg.txt
```

Since the configuration file does not alter any Tripwire policies or files tracked by the application, it is not necessary to regenerate the Tripwire database.

## 19.10. Tripwire File Reference

Before working with Tripwire, you should know where important files for the application are located. Tripwire stores its files in a variety of places depending on their role.

- Within the /usr/sbin/ directory, you will find the following programs:
- tripwire
- twadmin
- twprint

- Within the /etc/tripwire/ directory, you will find the following files:
- twinstall.sh — The initialization script for Tripwire.
- twcfg.txt — The sample configuration file supplied by the Tripwire RPM.
- tw.cfg — The signed configuration file created by the twinstall.sh script.
- twpol.txt — The sample policy file supplied by the Tripwire RPM.
- tw.pol — The signed policy file created by the twinstall.sh script.
- Key Files — The local and site keys created by the twinstall.sh script which ends with a .key file extension.

- After running the twinstall.sh installation script, you will find the following files in the /var/lib/tripwire/ directory:
- The Tripwire Database — the database of your system's files and has a .twd file extension.
- Tripwire Reports — the report/ directory where Tripwire reports are stored.

The next section explains more about the roles these files play in the Tripwire system.

### 19.10.1. Tripwire Components

The following describes in more detail the roles listed in the previous section play in the Tripwire system.

### /etc/tripwire/tw.cfg

This is the encrypted Tripwire configuration file which stores system-specific information, such as the location of Trip data files. The twinstall.sh installer script and twadmin command generate this file using the information in the text version of the configuration file, /etc/tripwire/twcfg.txt.

After running the installation script, the system administrator can change parameters by editing /etc/tripwire/twcfg.txt and regenerating a signed copy of the tw.cfg file using the twadmin command. Seeing Section 19.9 Updating the Tripwire Configuration File for more information on how to do this.
