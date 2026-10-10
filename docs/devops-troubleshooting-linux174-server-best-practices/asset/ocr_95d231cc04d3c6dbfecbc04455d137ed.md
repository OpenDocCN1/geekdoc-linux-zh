start and stop. In this case, the script will start when any runlevel is entered and will stop when the runlevel is not set.

The next couple of lines export some environment variables, and then the task option tells init that this script will not be persistent—it will execute and then stop.

The actual programs that are run from an Upstart script are defined with either the script or exec options. In the case of the exec option, Upstart executes the command and all of the arguments that follow the exec option and keeps track of its PID. With the script option, Upstart treats the lines that follow as a shell script until it reaches the end script line.

Even though Upstart is designed to be event-driven, it still provides methods to check the status of Upstart jobs and start and stop them as appropriate. You can check the status, start, and stop Upstart scripts with the appropriately named status, start, and stop commands. One Upstart job on an Ubuntu server is the tty1 job and it starts the getty program on tty1. This gives an administrator a console when he or she presses Alt-F1. Let’s say, however, that for some reason you believe that the console was hung. Here’s how to check the status and then restart the job:

```
```
$ sudo status tty1
tty1: start/running, process 789
$ sudo stop tty1
tty1 stop/waiting
$ sudo start tty1
tty1 start/running, process 2251
```
```

You can also query the status of all available Upstart jobs with initctl list:

```
```
$ sudo initctl list
mountall-net stop/waiting
rc stop/waiting
rsyslog start/running, process 640
tty4 start/running, process 708
udev start/running, process 299
upstart-udev-bridge start/running, process 297
userdata-other stop/waiting
```
```