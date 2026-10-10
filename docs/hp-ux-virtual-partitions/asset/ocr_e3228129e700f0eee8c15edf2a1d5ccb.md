# Disk Reconfiguration Flow Diagram - Part 3

From Part 2.

Mirror all logical volumes on `cl060` to `cl030` with `lvextend`.  
`# lvextend -m 1 /dev/vg00/lvol1 /dev/disk/cl030`  
lvol2  
lvol3  
lvol4  
lvol5  
lvol6  
lvol7

Verify that logical volumes are mirrored with `lvdisplay`.  
`# lvdisplay -v /dev/vg00/lvol* | more`

Reboot system to confirm all changes have taken effect. Put key in “Service Mode” and type `tc` to get into Command Mode and create core dump with `Transfer Control` (`tc`) command.  
`CM> tc`

After reboot save core dump to tape with `savecore`. `/var/adm/crash` is a required part of this command even though it wasn’t used.  
`# savecore -i /dev/rmt/0m /var/adm/crash`  
Send tape to HP Response Center to verify that core dump can be read.

Optionally, you can extract core dump from tape and put in `/var/adm/crash`  
`# savecore -xt /dev/rmt/0m /var/adm/crash`

+   * F19
+   * F20
+   * F21
+   * F22
+   * F23

# Figure 9-15  Disk Reconfiguration Flow Diagram - Part 3 (Reinstate Mirrors)