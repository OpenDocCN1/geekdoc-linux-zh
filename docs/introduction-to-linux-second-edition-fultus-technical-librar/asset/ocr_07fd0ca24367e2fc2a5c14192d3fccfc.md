+   * Run the command find /. What effect does it have on system load? Stop this command.
+   * In graphical mode, start the xclock program in the foreground. Then let it run in the background. Stop the program using the kill command.
+   * Run the xcalt directly in the background, so that the prompt of the issuing terminal is released.
+   * What does kill -9 -1 do?
+   * Open two terminals or terminal windows again and use write to send a message from one to the other.
+   * Issue the dmesg command. What does it tell?
+   * How long does it take to execute ls in the current directory?
+   * Based on process entries in /proc, owned by your UID, how would you work to find out which processes these actually represent?
+   * How long has your system been running?
+   * Which is your current TTY?
+   * Name 3 processes that couldn't have had init as an initial parent.
+   * Name 3 commands which use SUID mode. Explain why this is so.
+   * Name the commands that are generally causing the highest load on your system.

# 4.6.2 Booting, init etc.

+   * Can you reboot the system as a normal user? Why is that?
+   * According to your current run level, name the steps that are taken during shutdown.
+   * How do you change the system run level? Switch from your default run level to run level 1 and vice versa.
+   * Make a list of all the services and daemons that are started up when your system has booted.
+   * Which kernel is currently load at startup?
+   * Suppose you have to start some exotic server at boot time. Up until now, you logged in after booting the system and started this server manually using a script named deliver_pizza in your home directory. What do you have to do in order to have the service start up automatically in run level 4, which you defined for this purpose only?