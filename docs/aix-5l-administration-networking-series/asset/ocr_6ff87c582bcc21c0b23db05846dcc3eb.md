# ## Cloning AIX Systems to New Hardware

We are getting a lot of new machine upgrades. Most of our H-50 and below RS/6000 machines are being replaced by either H-80 RS/6000s or 6H1 pSeries machines (some of these machines have the same CPU). Each system changeover requires using the cloning procedures to different hardware. This is really very straightforward and easy to do once you get the procedure down.

The first thing that you want to do is run a **fresh mksysb** on the current machine. Make sure that all of the applications are stopped. Bring down all of the databases. Get all of the users off the system and then lock out all nonroot users by creating an /etc/nologin file. I think you get the picture: we want a completely idle system before running the **mksysb** backup. You should also extract a file from the **mksysb** tape using the following procedure to ensure that the backup is good. This procedure assumes the rmt0 tape drive is used. Restoring a single file from a **mksysb** tape requires the nonrewinding tape mode (dev/rmt0.1). This can be time-consuming, so it may help to also make an online **mksysb** backup to a non-rootvg or NFS filesystem. If you use this method, make sure that the root users on both systems can write large files and the filesystem is large file enabled. Insert the newly created **mksysb** tape in the tape drive and run the following commands:

+   *   `# tctl -f /dev/rmt0 rewind` Rewind the tape
+       *   `# tctl -f /dev/rmt0.1 f3` Fast forward 3 records (/dev/rmt0.1 = no rewind)
+       *   `# restore -xvpf /dev/rmt0.1 .etc/hosts` Extract the /etc/hosts file from tape

**NOTE** Do not forget the dots. If you omit the dot before .etc/hosts, the file will not be installed.

If this procedure is successful, then we most likely have a good backup. The only way to really know if you have a good **mksysb** backup is to restore the system! The next steps will guide you through the cloning process:

+   1.  Insert the current AIX release CD-ROM, the same AIX version that the **mksysb** backup was done on, into the CD-ROM drive.
+       2.  Insert the **mksysb** tape into the tape drive.
+       3.  Power down the system.
+       4.  Ensure that all of the external devices, if any, are powered on.
+       5.  Turn the key mode switch, if present, to the "Service" position (Micro Channel machines).
+       6.  Turn the power on.