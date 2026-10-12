+   - **Minolta** — Image 5, Image 7, and Dimage X.
+   - **Nikon** — CoolPix 2500, 885, 5000, 775, and 995.
+   - **Olympus** — Brio Zoom D-15, C-100, C-200Z, C-2040, C-220Z, C-2Z, C-3020Z, C-3040Z, C-4040Zzoom, C-700, C-700UZ, C-860L, D-510, D-520Z, E-10, and E-20.
+   - **Pentax** — EI2000, Optio 330, and Optio 430.
+   - **Sony** — DSC-F505, DSC-F505V, DSC-F707, DSC-P1, DSC-P20, DSC-P5, DSC-P71, DSC-S30, DSC-S70, DSC-S75, DSC-S85, MVC-CD300, and MVC-FD92
+   - **Vivitar** — Vivicam 3550
+   - **Yashica** — Finecam s3

To Linux, the USB mass storage camera appears as a SCSI drive containing a VFAT file system with image files on it. Here's a procedure for using your digital camera as a USB storage device:

+   1. Using a cable provided with your digital camera, connect your camera to a USB port on your computer and turn it on so it is ready to send and receive data.
+   2. Boot your computer to Red Hat Linux.
+   3. Open the `/etc/fstab` file as root user and see if an entry was created for your digital camera. If you have no other SCSI devices on your computer, the camera will probably be detected as `/dev/sda1` device. Here is what the entry might look like:
+   ```text
+   /dev/sda1     /mnt/camera       auto    defaults, user,noauto     0 0
+   ```
+   If no such entry appears, create the entry, possibly using `vfat` instead of `auto`. Create the mount point directory (as root user, type `mkdir /mnt/camera`).
+   4. As root user, type the mount command to mount the camera: **`mount /mnt/camera`**.
+   5. Open the `/mnt/camera` as you would any other directory from the shell or from a file manager. Copy, delete, move, and rename files as you would any files on your hard disk.
+   6. When you are done, be sure to unmount the camera as follows (as root user from a Terminal window).
+   ```text
+   # umount /mnt/camera
+   ```

> **CAUTION:** If you unplug your camera without unmounting the file system, it could damage the files on your camera.

You can follow the procedure above to use other USB mass storage devices (CD drives, keychains, and so on) in Linux. Use different mount directories (such as `/mnt/keychain`) and check which SCSI device is being assigned to the USB storage device.