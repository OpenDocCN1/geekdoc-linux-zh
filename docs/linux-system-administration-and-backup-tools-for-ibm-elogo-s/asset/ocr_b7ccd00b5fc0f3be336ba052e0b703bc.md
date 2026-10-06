* The letter S denotes that this service should be started when entering a runlevel. The letter K indicates the services that will be killed when entering a runlevel from another runlevel.
* Services are started in order of the number here, with the lowest numbers being first.
* the name of the script to run. The scripts reside in /etc/rc.d/init.d.

Runlevels are user configurable, but the conventional assignments in Linux (which TurboLinux follow):

+   * 0 -- Shut down the machine
* 1 -- Single user mode
* 2 -- Multiple user mode, but no networking
* 3 -- Full networking, text mode login
* 4 -- User configurable
* 5 -- Full networking, graphical login
* 6 -- Initiate a warm reboot

As pointed out earlier, runlevels are user configurable, and TurboLinux provides the turboservice to edit the services at run. When you start turboservice, it presents you with the following window:

![](bbox=[0.147, 0.4, 0.851, 0.642])

Figure 17. Service Status Board window

Note that on this window, runlevels are not mentioned. That is the main screen of turboservice runs in the current runlevel. In this case we are running at runlevel 3, so all the changes we make will be written to

Chapter 5. TurboLinux basic system administration 165