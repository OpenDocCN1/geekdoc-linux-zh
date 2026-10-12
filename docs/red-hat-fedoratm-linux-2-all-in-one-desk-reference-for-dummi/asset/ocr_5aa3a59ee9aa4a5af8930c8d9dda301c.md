+   1. **Log in as *root*, and choose *Main Menu:* **System Tools:** *Red Hat Network*. You can also type *up2date* in a terminal window.
+   
+   The Red Hat Update Agent starts, and, if you’re using Up2date for the first time, a dialog box prompts you to install a public key in your GPG key ring. (*GPG* refers to GNP Privacy Guard or GnuPG, a program for encrypting, decrypting, and signing e-mail and other data using the OpenPGP Internet standard.) That public GPG key verifies that the package developer has securely signed the package that Up2date has downloaded. If prompted to do so, click **Yes** to install the public key.
+   
+   2. Up2date displays a window with a welcome message. Click the **Forward** button to proceed.
+   
+   3. Up2date displays a list of what it calls channels — repositories from where the agent downloads package headers. Click **Forward** to continue.
+   
+   By default, the Update Agent uses a channel that works with *Yum* — a command-line package updater/installer that I describe in the next section. The channels are identified in the text configuration file */etc/ *sysconfig/rhn/sources*. Besides *Yum*, the Up2date can also access repositories meant for Apt — another package updater.
+   
+   After you click **Forward**, Up2date figures out what needs to be updated and retrieves a list of all headers from the specified channel.
+   
+   4. After Up2date downloads the headers, it displays a list of packages. You can then scroll through the list and pick the packages you want to update; click the box to the left of a package’s name to select it. Click **Forward** to continue.
+   
+   Up2date then checks for any package dependencies and begins downloading the packages. Progress bars show the status of the download.
+   
+   5. After the download finishes, click the **Forward** button to proceed with the installation.
+   
+   6. Up2date displays progress bars as it installs each package update. Click the **Forward** button when the installation is complete.
+   
+   Up2date displays a message about the package(s) it installs successfully.
+   
+   7. Click the **Finish** button to exit Up2date.

# ### Using Yellow dog Updater, Modified (Yum)

Yellow dog Updater, Modified (Yum) is a command-line utility for updating as well as installing and removing RPM packages. Yum downloads RPM package headers from a specified Web site and then uses the rpm utility to figure out