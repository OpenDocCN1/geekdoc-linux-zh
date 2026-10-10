An error occurs while trying to access an Ignite server or cold-install file.

You have specified the BOOT or ALTBOOT device, but the corresponding device has not been configured in vp_name.

NOTE: If the boot device has not been configured properly the vpboot command will complete without errors, but the virtual partition will not boot. Two possible reasons for this could be:

+   * The BOOT or ALTBOOT attribute was assigned to a device other than a disc or tape.
+   * The file at the default or configured kernel path does not exist or is not a bootable image.

# AUTHOR

vpboot was developed by the Hewlett-Packard Company.

# SEE ALSO

vpcreate(1M), vpmodify(1M), vpremave(1M), vpreset(1M),
vpstatus(1M), vpreources(5), vpartition(5).