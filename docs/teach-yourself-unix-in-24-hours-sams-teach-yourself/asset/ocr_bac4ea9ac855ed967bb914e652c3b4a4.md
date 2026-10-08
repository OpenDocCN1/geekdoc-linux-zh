# 408

# Hour 20

other folks. In this hour, you learn about the standard electronic mail system, Berkeley Mail. I also take a little time to whet your appetite by showing you the Elm Mail System, a full-screen alternative mail program that's widely distributed.

![](bbox=[0.169, 0.226, 0.239, 0.276])

There's a much bigger world than the machine you're on; it's called the Internet. You learn lots about how to use this valuable system in the closing hours of Teach Yourself UNIX in 24 Hours.

JUST A MINUTE

# Task 20.1: Enabling Messages Using mesg

Earlier you learned that all peripherals hooked up to UNIX are controlled by drivers and that each driver has an associated/dev file. If you want to talk with other users on the system, you need to ensure that they can communicate with you, too. (This pertains only to write, however: e-mails regardless of the mesg setting.)

DESCRIPTION

ACTION

+   1. To find out which device I'm connected to the system, I can use the UNIX command tty:
% tty
/dev/ttyAo
The tty device is just another UNIX file, so I can look at it as I'd look at any other file:
% ls -l /dev/ttyAo
crw-x---- 1 taylor 21, 71 Dec 8:34 /dev/ttyAo*
Notice that I own the file and that I have permission, but others do not.
2. To enable other users to communicate with me directly, I need to ensure that they can run programs that can write to my terminal. That is, I need to give them permission to my tty device. Instead of using chmod command—tracking down I'm on and all that—I use a simple alternative, mesg. To turn messages—allowing other users to communicate with me—I specify the y flag to mesg:
% mesg y
% ls -l 'ttyAo'
crw-rw---- 1 tailor 21, 71 Dec 8:13 /dev/ttyAo*
To disable messages (perhaps if I'm busy and don't want to be bothered), I can use the n flag, which says that no, I don't want messages:

![](bbox=[0.063, 0.883, 0.137, 0.963])

20