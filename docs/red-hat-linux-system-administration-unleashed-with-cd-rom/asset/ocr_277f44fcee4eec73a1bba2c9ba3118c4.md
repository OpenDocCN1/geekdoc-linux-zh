# Keeping Records of Changes Made to the System

The first thing to remember is that you should have a record of changes made to the system since the initial installation that indicates which packages, if any, have been updated. This is especially important for upgrades made to correct security issues, but is important for any packages updated from the vendor. This record should also note any packages that you have installed that were not on the distribution media.

# Reinstalling from Clean Media

The second rule is that reinstallation should be from a medium that there is no possibility that the intruder had access to, preferably removable media that is write protected. A good example of this type of media is the Red Hat distribution CDs. This is important because if you move the installation packages from the CD to a hard drive to facilitate installs over the network, for example, you risk installing corrupted packages if the intruder was able to access your installation server.

# Retrieving Fresh Copies of Updates

Next, once you have installed from the pristine media, retrieve fresh copies of any updates that you may have installed and install them. Again, do not trust previous copies that you have downloaded because the intruder may have tampered with them.

# Snapshotting the System

Finally, once you have everything reinstalled, take a snapshot of the system by backing it up to tape or some other medium. If you do not have a filesystem monitoring program in place, such as Tripwire, consider installing one.

# Summary

This chapter discussed a number of the issues you will face in the event of a security breach on one of your systems. If you gain nothing else from this chapter, you should remember the rules of engagement for dealing with intrusions. I also highly recommend checking out Trinux for your network analysis and disaster recover needs.