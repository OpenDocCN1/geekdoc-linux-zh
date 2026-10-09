+   3. Configure the bluetooth kernel module.

+   a. At the command prompt, enter `cd /etc` to navigate to the `/etc` directory.

+   b. Enter `vi modprobe.conf` to open the modprobe.conf file for modification.

+   c. Press `Shift+G` to go to the last line.

+   d. Press `O` to switch to the insert mode and move to a new line.

+   e. On a new line, enter `alias blue bcm203x` to specify an alias name for the bluetooth module.

+   f. Press `Esc` to switch to the command mode.

+   g. Save and close the file.

+   h. Enter `logout` to log out.