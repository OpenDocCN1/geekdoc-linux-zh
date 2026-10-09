groups before and after operating system upgrades. Each AIX BOS installation destroys all or part of rootvg.

# Mirroring rootvg

If you do not mirror the root volume group, you have a single point of failure. Always mirror rootvg! I have seen too many unnecessary system rebuilds because rootvg was not mirrored. Mirroring rootvg is a straightforward process and consists of the following steps, in which we are going to mirror rootvg to a new disk called hdisk1:

+   1.  Add hdisk1 to the rootvg for mirroring:
+   ```bash
+   # extendvg rootvg hdisk1
+   ```

+   2.  Use this command if all the rootvg logical volumes were created properly:
+   ```bash
+   # mirrorvg rootvg # This command will do it all if no errors occur
+   ```

+   3.  Or (if a problem was encountered) manually mirror rootvg and do not mirror the dump device (lv00 in example):
+   ```bash
+   # lsvg # To make sure there are two drives in rootvg
+   # lsvg -l rootvg # To see if anything is mirrored already
+   # lsvg rootvg # To check available space
+   ```

+   4.  Mirror each logical volume:
+   ```bash
+   # for N in $(lsvg -l rootvg | grep synced | awk '{print $1}' | grep -v lvol0)
+   > do
+   > echo $N
+   > mircopy $N 2
+   > done
+   ```

+   5.  Sync the volume group:
+   ```bash
+   # syncvg -v rootvg
+   # lsvg -l rootvg
+   ```

+   6.  Configure the boot devices:
+   ```bash
+   # ipl_varyon -i
+   PNAME        BOOT DEVICE     PVLD             VOLUME GROUP ID
+   hdisk0         NO             0000104735ac2310     000010472822f021
+   hdisk1         YES            000010472822e532     000010472822f021
+   
+   # bosboot -a -d /dev/hdisk0
+   
+   bosboot: Boot image is 6955 512 byte blocks.
+   
+   # ipl_varyon -i
+   ```