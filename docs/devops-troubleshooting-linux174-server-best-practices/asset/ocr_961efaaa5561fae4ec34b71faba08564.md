say, your web server. In addition, init scripts commonly accept a few extra options such as restart (stops and then starts the service), status (returns the current state of a service), reload (tells the service to reload its settings from its configuration files), and force-reload (forces the service to reload its settings). When you run an init script with no arguments, it should generally return a list of arguments that it accepts.

# ■ /etc/rc0.d through /etc/rc6.d

These directories contain the init scripts for each respective runlevel. In practice, these are generally symlinks into the actual files under /etc/init.d. What you will notice, however, is that the init scripts in these directories have special names assigned to them that start with an S (start), K (kill), or D (disable) and then a number. When init enters a runlevel, it runs every script that begins with a K in numerical order and passes the stop argument, but only if the corresponding init script was started in the previous runlevel. Then init runs every script that begins with an S in numerical order and passes the start argument. Any scripts that start with D init ignores—this allows you to temporarily disable a script in a particular runlevel, or you could just remove the symlink altogether. So if you have two scripts, S01foo start and S05bar start, init would first run S01foo start and then S05bar start when it entered that particular runlevel.

# ■ /etc/rc5.d

In this directory you will find all of the system init scripts that init runs at start-up before it changes to a particular runlevel. Be careful when you tinker with scripts in this directory because if they stall, they could prevent you from even entering single-user mode.

# ■ /etc/rc.local

Not every distribution uses rc.local, but traditionally this is a shell script set aside for the user to edit. It’s generally executed at the end of the init process, so you can put extra scripts in here that you want to run without having to create your own init script.

Here is an example boot process for a standard System V init system. First init starts and reads /etc/inittab to determine its default runlevel, which in this example is runlevel 2. Then init goes to /etc/rcS.d and runs