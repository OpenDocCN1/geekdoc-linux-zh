+   3. Create the spool directory `/var/spool/lpd/fax` on each client system that will be printing to the fax queue.

# # EXTENDING EFAX WITH QFAX

Although Efax can easily be used to deploy an outgoing fax server for small businesses and workgroups, it lacks some key features necessary for a more robust, large-scale fax server. Some of these missing features are provided for with the Qfax packages:

+   - Sending outgoing faxes by email
+   - Automatically generating cover pages
+   - Spooling outgoing faxes

# ## INSTALLING QFAX

The current version of Qfax is 1.3 and is available as the file `qfax1.3.tar.gz` from `http://metalab.unc.edu/pub/Linux/apps/serialcomm/fax/qfax1.3.tar.gz`. Download the file and extract it in a convenient location with the command:

```
tar zxvf qfax1.3.tar.gz
```

Qfax is extracted into the current directory, so make sure you are in the exact directory where you want to place the source code distribution. Qfax does not extract into a subdirectory of the current directory.

After you have extracted Qfax, installation requires several steps:

+   1. Create a fax user.
+   2. Create a FaxMaster mail alias.
+   3. Create an email to fax gateway.
+   4. Create a spool directory for faxes.
+   5. Create a fax configuration directory.
+   6. Configure Qfax.
+   7. Specify privileged users.
+   8. Edit the `fax.rc` file.
+   9. Create the `fax.db` file.
+   10. Create the `.fax` file.
+   11. Compile and install Qfax.
+   12. Schedule fax queue processing.

These steps presume that you have installed and configured Efax already.