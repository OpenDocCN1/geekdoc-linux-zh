Use the pgrep command to verify whether the service has been stopped or started:

```
pgrep -f <service>
```

The pgrep utility examines the active processes on the system and reports the process IDs of the processes. See Chapter 9, “Process Control,” for details on this command.

# Adding Scripts to the Run Control Directories

If you add a script, put the script in the /etc/init.d directory, and create a link to the appropriate rc<n>.d directory. Assign appropriate numbers and names to the new scripts so that they will be run in the proper sequence.

# STEP BY STEP

# 1.2 Adding a Run Control Script

+   1. Become superuser.
2. Add the script to the /etc/init.d directory:
   # cp <filename> /etc/init.d
   # chmod 0744 /etc/init.d/<filename>
   # chown root:sys /etc/init.d/<filename>
3. Create links to the appropriate rc<n>.d directory:
   # cd /etc/init.d
   # ln <filename> /etc/rc2.d/S<nn>filename
   # ln <filename> /etc/rc<n>.d/K<nn>filename
4. Use the ls command to verify that the script has links in the specified directories:
   # ls -l /etc/init.d/ /etc/rc2.d/ /etc/rc<n>.d/

The following example creates an rc script named “program” that will start up at run level 2 and stop at run level 0:

```
# cp program /etc/init.d
# cd /etc/init.d
# ln /etc/init.d/program /etc/rc2.d/S100program
# ln /etc/init.d/program /etc/rc0.d/K100program
# ls -l /etc/init.d /etc/rc2.d /etc/rc0.d
```