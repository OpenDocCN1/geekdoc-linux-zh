the service so that it can restart it in the next step. To kill a running service, the script runs the necessary “K” script with the “stop” argument. K scripts are discussed in the next section.

+   3. In this final step the rc script runs all the “S” scripts with the “start” argument. S scripts are discussed in the next section.

# /etc/rc.d/rc[0-6].d

The rc0.d to rc6.d subdirectories are used for run levels 0 to 6. These directories contain symbolic links to scripts in the /etc/rc.d/init.d directory. For example, if you look at the rc3.d directory in a Red Hat Linux system you will notice that scripts from the /etc/rc.d/init.d directory are linked in two ways. Some scripts are linked as:

```
K{two-digit_number}{script_name}
```

For example K99httpd is a script that is linked to the /etc/rc.d/init.d/httpd script. Other scripts are linked as:

```
S{two-digit_number}{script_name}
```

For example, S99httpd is a script that is linked to the /etc/rc.d/init.d/httpd script. All the scripts prefixed with a letter “K” run with the “stop” argument, and all scripts with a letter “S” run with the “start” argument. The two-digit number is used to set the execution order. Thus a script called S01foo runs before S10bar. The /etc/rc.d/rc script runs the “S” and “K” scripts.

After the rc script is finished, the processing done by init also finishes and the system becomes available in the new run level.

# /etc/rc.d/rc.local

The rc.local script is typically executed once at the end of the run levels 2, 3, and 5. You can add anything that needs to be run once per boot in this file. Simply append whatever command you want to run at the end of this file using a text editor, and the command you add will be run once every time you boot your system.