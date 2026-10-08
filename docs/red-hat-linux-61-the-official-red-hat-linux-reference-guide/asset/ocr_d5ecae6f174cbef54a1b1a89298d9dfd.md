# 19.4. Initialize the Tripwire Database

When initializing its database, Tripwire builds a collection of file system objects based on the rules in the policy file. This database serves as the baseline for integrity checks.
To initialize the Tripwire database, using the following command:

```
/usr/bin/tripwire --init
```

This command can take several minutes to run.
Once you finish these steps successfully, Tripwire has the baseline snapshot of your file system to check for changes in critical files. After initializing the Tripwire database, you should run an initial integrity check. This check should be done before connecting to the network and putting it into production. For further instructions, see Section 19.5 Running an Integrity Check.
Once Tripwire is configured to your satisfaction, you are free to place the system in production.

# 19.5. Running an Integrity Check

By default, the Tripwire RPM installs a shell script tripwire-check to the /etc/cron.daily/ directory. This script automatically runs an integrity check every day.
You however, run a Tripwire integrity check at any time by typing the following command:

```
/usr/bin/tripwire --check
```

During an integrity check, Tripwire compares the current state of file system objects with the properties recorded in its database. Violations are printed to the screen and an encrypted copy of the report is created in /var/lib/tripwire/report/. You can view the report using the twprint command as outlined in Section 19.6 Viewing Tripwire Reports.
If would like to receive an email when certain types of integrity violations occur, you can configure this in the policy file. See Section 19.8.1 Tripwire and Email for instructions on how to set up and test this feature.

# 19.6. Examing Tripwire Reports

The /usr/bin/twprint command is used to view encrypted Tripwire reports and databases.

# 19.6.1. Viewing Tripwire Reports

The twprint -r command will display the contents of a Tripwire report in clear text. You must, however, tell twprint which report file to display.
A twprint command for printing Tripwire reports looks similar to the following:

```
/usr/bin/twprint -m --twfle /var/lib/tripwire/report/<name>.twr
```

The -m option in the command directs twprint to decrypt a Tripwire report. The --twfle option directs twprint to use a specific Tripwire report file.
The name of the report that you want to see includes the name of the Tripwire checked to generate the report, the creation date and time. You can review previously saved reports at any time. Simply ls /var/lib/tripwire/report to see a list of Tripwire reports.
Tripwire reports can be rather lengthy, depending on the number of violations found or errors generated. A sample report starts off like this: