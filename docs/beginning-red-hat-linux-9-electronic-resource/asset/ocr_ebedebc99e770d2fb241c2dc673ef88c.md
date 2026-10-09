It is vital that we are confident the system is in a sound state before initializing the database, otherwise there's little point in using Tripwire. After the database is initialized, it's a good idea to put a copy on write-once media (e.g. CD-ROM) so that it cannot be altered:

```
# tripwire --init
Please enter your local passphrase:
Parsing policy file: /etc/tripwire/tw.pol
Generating the database...
*** Processing Unix File System ***
Wrote database file: /var/lib/tripwire/rh9.twd
The database was successfully generated.
```

# Setting up Tripwire to Run Automatically

We've already seen how logwatch is set up to run automatically every day at 04:02. We can very easily set up Tripwire to run at the same time.

Create a two-line script called /etc/cron.daily/run-tripwire containing the following lines:

```
#!/bin/sh
/usr/sbin/tripwire --check
```

Make sure the script is owned by root and has permissions of 500 (r-x------) so it is executable only by root. This script invokes Tripwire and gets it to check the system's integrity according to the rules in the policy file, and using the database we just created as its baseline. When cron runs this script at 04:02 every day its output is sent to root (or whoever is configured in the MAILTO variable in /etc/crontab).

# Updating the Tripwire Database

We'll test the script by running it now. Type /etc/cron.daily/run-tripwire on the command line as root, and check that Tripwire runs successfully. Examine the output produced carefully, and we should see that Tripwire has spotted the addition of the run-tripwire script to /etc/cron.daily and flagged it as a critical change.

To stop Tripwire from reporting this change, which we made and know is OK, as a policy violation every time it runs, we need to update Tripwire's database. We do this by running tripwire --update, specifying a Tripwire report file that we wish to use for the update. To see what files are available, run ls -ltr /var/lib/tripwire/report; choose the last report listed as this will be the most recent one.

The command to run (all on one line) is then:

```
# tripwire --update --twrfile /var/lib/tripwire/report/rh9-20030209-040304.twr
```