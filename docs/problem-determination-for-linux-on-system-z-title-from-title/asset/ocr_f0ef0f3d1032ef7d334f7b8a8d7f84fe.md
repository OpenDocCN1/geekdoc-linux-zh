# ## Check the status of DASD recognition

Next you will want to check the status of DASD recognition by checking the following:

+   - The Common I/O
+     
+     - Check `1c5s5` output.
+       - Check whether the address of the target device is displayed.
+       - Check whether DevType and CU type are collect.

+   - The device driver
+     
+     - Check the /sys/bus/ccw/drivers/dasd-eckd directory.
+     - Check whether the symbolic link of the target device is in /sys/bus/ccw/drivers/dasd-eckd.

+   - Online status
+     
+     - Check `1sdasd`.
+     - Check `1c55`.
+     - Check /sys/bus/ccw/drivers/dasd-eckd/0.0.<address>/online.

# ## Check the status of FCP device recognition

You will want to check the status of your FCP device recognition:

+   - FCP port on System z
+     
+     - Check the `1c5s5`.
+     - Use="yes" means that the FCP port is online on System z.
+     - /sys/bus/ccw/drivers/zfcp/0.0.xxxx/online means the same.

+   - FCP port on storage system
+     
+     - Check the /sys/bus/ccw/drivers/zfcp/0.0.xxxx/ directory.
+     - If is a directory that is named with WWPN, FCP port is online on the storage system.

+   - LUN recognition
+     
+     - Check the /sys/bus/ccw/drivers/zfcp/0.0.xxxx/yyy…yyy/ directory (yyy…yyy is WWPN).
+     - There is a directory that is named with the LUN number, meaning that the LUN is recognized.

+   - SCS! disk recognition
+     
+     - Check `1scss1`.
+     - Check /proc/scsi/scsi.