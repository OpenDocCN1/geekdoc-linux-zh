# 116 Part II + The SUSE System

When we enter enters and leaves with respect to runlevels, we are talking about changing one runlevel to another using the init or telinit process, or booting down the system.

You never stop a runlevel in Unix—you move from one runlevel to another. For example, if the system loads runlevel 5 by default, it will continue to run at runlevel until you tell it to move to another one. If you wanted to shut down the machine, you would move into runlevel 0. This would trigger init to run all of the Kill scripts in /etc/init.d/rc0.d and then all of the Start scripts (of which there are none).

The Start and Kill scripts in a runlevel are actually symbolic links to files in /etc/init.d, which are all the service scripts for daemons and processes that can be controlled by init. Using symbolic links rather than runlevel specific scripts enables the system to share scripts across different runlevels. The directory associated with each runlevel that to start a service can simply contain a symbolic link to the same master script, saving disk space and simplifying maintenance of the service scripts. Updating the master service script in /etc/init.d automatically makes these changes available to any other runlevel that refers to the Start script.

The files in /etc/init.d contains a few features that are unique to the init system. The scripts are nearly always bash scripts that take at least two arguments, start and stop. If you directly run one of these scripts with the start option, it would try to load the application that the script controls. Similarly, if you pass the stop parameter to the script, it attempts to shut down the application cleanly. In the SUSE world, we use rcservename scripts to control this behavior instead of accessing the /etc/init.d directly. If you wanted to stop the Apache web server process, you could type the command rcapache2 stop.

If you move to the specific runlevel directory and take runlevel 3 as an example, you will see many symbolic links in /etc/rc.rc3.d that begin with an S or a K, but you will notice that some of these point to the same script in the directory /etc/init.d.

When the init process runs a Start script, it calls the script that the link points to with the argument start. When the init process runs a Kill script, it calls the script that the link points to with the argument stop.

Start and Kill scripts usually have numbers after the S or K. This number signifies the relative order that the scripts are executed. A lower number means that the scripts are executed earlier than one with a higher number when entering or leaving a runlevel. Sequencing Start and Kill scripts is a very significant part of the boot