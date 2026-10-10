One consequence of mounting the root file system over NFS is that we can execute on the target program files that physically reside on the host’s file system. This allows us to test target software without having to program it into flash. And of course, programs running on the target can open files on the NFS-mounted host volume.

One of the directories on the target file system is `/home`. Under `/home/samples/src/` are several subdirectories, each representing a project described later on in the book.

![](bbox=[0.32, 0.25, 0.7, 0.4])

# Figure 7.2 The host and the target.

Start up `minicom` in a shell window, and boot the target board. When the boot completes, log in as root and execute `ls /home/samples` in the `minicom` window. You will see the same files and subdirectories that are in `~/bbbfs/home/samples` on your workstation.

Note that USR0 is already blinking. If you `cat /sys/class/leds/beaglebone:green:usr0/trigger` (do not forget TAB autocompletion), you will see that USR0 is being used as a “heartbeat”. If you `cat` the trigger file for the other LEDs, you will see that they also have specific triggers. These triggers would interfere with our led program, so we need to turn them off.

`/sys` is another pseudo file system like `/proc` that was described in Chapter 3, Introducing Linux. Like `/proc`, `/sys` is a mechanism to communicate between user space and kernel space. In this particular instance, we can exercise control over system peripherals. Have a look at the script file `samples/src/leds/leds-off.sh`. It writes the string “none” to the trigger files of all four LEDs. This says do not trigger the LEDs on anything.

Now, to execute the led program, do:

```
```
cd /home/samples/src/led
./led
```
```

The program prints a greeting message and then sequentially flashes the four LEDs. Incidentally, the “./” notation in the command represents the current directory. The reason for that is that the current directory is not normally part of a normal user’s path. To do so is considered a security risk.