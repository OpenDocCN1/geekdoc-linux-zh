```
/dev/hda1           1             1        800    1612768+  83  Linux native
/dev/hda2          801           801        833     66528   82  Linux swap
/dev/hda3          834           834       1023     383040   83  Linux native
Command (m for help):
```

Now that I have all my Linux partitions ready to go, I'm ready to install the software. From the command prompt in fdisk, I type w to write the partition table to the hard drive and exit. Now we're back at the familiar-looking root prompt.

# RUNNING THE SLACKWARE SETUP PROGRAM

Now you're ready to run the Slackware Setup program. To do so, type setup at the prompt:

```
# setup
```

The initial screen should look something like Figure 1-4.

![](bbox=[0.15, 0.53, 0.78, 0.72])

Figure 1-4: The Slackware Setup screen

Scroll down to select "TARGET" and format all of the Linux partitions. Make sure you write down which ones are which. For example, my disk looks like this:

```
/dev/hda1 /       300MB
/dev/hda2 /home   300MB
/dev/hda3 /usr    600MB
/dev/hda4 swap    64MB
```