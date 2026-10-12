Once the files have been uncompressed, the installation medium needs to be extracted from the cpio files. Because each of these archives has a top-level directory that it unpacks to called Disk1, you should change this directory to another name before starting the next cpio command. This will avoid having all three CDs worth of programs in the same subdirectory. This is done using the cpio and mv commands, as shown next:

```
cpio -idmv ship.db.cpio
mv Disk1 db.Disk1
cpio -idmv ship.ccd.cpio
mv Disk1 ccd.Disk1
cpio -idmv ship.crs.cpio
mv Disk1 crs.Disk1
```

Once the CD or CDs are unpacked, you are ready to start the installation process.

# ## Running the Installer

In order to invoke the installer, you will run the shell program runInstaller. Remember that there are a few prerequisites that must be done before you can run the installer. Here is a summary of those prerequisites.

+   - Kernel parameters must be set.
+   - Shell limits must be set.
+   - You must be logged in as the Oracle user account.
+   - You must be logged into a graphical session with X Windows for the Java installer to work.
+   - The environment variables ORACLE_BASE and ORACLE_SID should be set.

It is recommended that this program be run from the /tmp directory, so use the following commands to invoke the installer.

```
# cd /tmp
# /oracle_stage/db.Disk1/runInstaller
```

**NOTE**
*In order for the Oracle installer to work, X-Windows must be up and running. If you are running the installer via an ssh shell, X-Windows should be running on your local PC and the option “ForwardX11 no” should be set in the .ssh/config file.*