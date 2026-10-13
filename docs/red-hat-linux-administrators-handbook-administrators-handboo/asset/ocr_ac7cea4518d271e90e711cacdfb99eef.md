The following is a description of the options:

+   - **-p.** Specifies the location of the rdistd program needed by rdist.
+   - **-o.** Specifies that one or more options are to follow—in this case, remove and quiet.
+   - **remove.** Tells rdist to remove any extraneous files found in the target system in target directories. This provides an easy method for maintaining an identical copy of the files on each student system.
+   - **quiet.** Tells rdist to be as quiet as possible during the operation.
+   - **-f.** Specifies the location of the distfile.

To reduce human error in running this command, create an sh script called redistribute.sh, as shown in Listing 13-2.

# Listing 13-2 The redistribute.sh Script

```
```sh
#!/bin/sh

# This script runs rdist to update Web servers via the
# non-routable lan an-university.edu. The script is run
# by cron at a fixed interval.

# /etc/rc.d/rc.local starts the script to clean up
# left-over tempfiles that might have been left
# at shutdown. This process also removes the
# log file.

# $Author$ (kabir@nitec.com)
# $Version$
# $Id$
# $Date$
# $Status$
########################################
####

# If the script is called with an
# argument then
```
```