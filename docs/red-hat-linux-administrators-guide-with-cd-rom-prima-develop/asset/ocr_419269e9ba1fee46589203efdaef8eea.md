or to some other UNIX variant, I simply export the remote GUI application to my own X session by using xhost.

In one case, I needed to use Solaris’s metatool remotely to re-create larger disk partitions from separate physical drives on a Sun Microsystems machine. The only problem was that I was located quite some distance from the machines themselves and had to perform this task remotely on a Linux box since I had no other Sun machines from which I could use the same application. Even if I had had access to a monitor, the machine itself would have required traveling to the new location. Using xhost, I was able to do run the metatool program from the convenience of my own home.

The same general situation has occurred with several of the Linux machines that I currently maintain. Recently a large security hole was discovered in a distribution kernel and I needed to install a new kernel on the 15 or more Linux boxes that I maintain. Rather than attaching a monitor to each machine, since all were headless, I used the xhost command to export the xconfig menu to my own X display.

♦♦♦

# CAUTION

> Like NFS, xhost does not provide the best security if you decide to make certain features available to others. Any network sharing or exporting is allowed at your own discretion.

Here are some simple steps to export remote applications to your own Linux system. In this example, you export linuxconf from a remote machine to your local machine.

+   1. Within your own X session, use telnet to switch to the machine that has the application that you want to export to your own local machine.
+   2. Become superuser by entering su on the remote machine.
+   3. Within the remote machine’s terminal window, enter export DISPLAY=<your local machine’s name>:0.0. For example, on my