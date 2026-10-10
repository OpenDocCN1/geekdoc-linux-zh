3. Up2date displays a list of what it calls channels — repositories from where the agent downloads package headers. Click Forward to continue.

By default, the Up2date Agent uses a channel that works with Yum — a command-line package updater/installer that I describe in the next section. The channels are identified in the text configuration file /etc/sysconfig/rhn/sources. Besides Yum, Up2date can also access repositories meant for APT — the Advanced Packaging Tool used in Debian.

After you click Forward, Up2date figures out what needs to be updated and retrieves a list of all headers from the specified channel.

4. After Up2date downloads the headers, it displays a list of packages. You can scroll through the list and pick the packages you want to update; click the box to the left of a package’s name to select it.

Click Forward to continue.

Up2date then checks for any package dependencies and begins downloading the packages. Progress bars show the status of the download.

5. After the download finishes, click the Forward button to proceed with the installation.

6. Up2date displays progress bars as it installs each package update. Click the Forward button when the installation is complete.

Up2date displays a message about the package(s) it installs successfully.

7. Click the Finish button to exit Up2date.

![](bbox=[0.12, 0.58, 0.2, 0.65])

Fedora Core 5 comes with another graphical utility called Package Updater that you can use to update software packages installed on your Fedora Core system. To start the Package Updater, choose Applications → System Tools → Software Updater or type su - in a terminal window to become root and then type pup.

In Fedora Core, you can also use Yum (which, by the way, stands for Yellow dog Updater, Modified). Yum is a command-line utility for updating as well as installing and removing RPM packages. Yum downloads RPM package headers from a specified Web site and uses the rpm utility to figure out any interdependencies among packages and what needs to be installed on your system. Then it downloads and uses rpm to install the necessary packages. Yum downloads just the headers to do its job, and the headers are much smaller in size than the complete RPM packages. Yum is much faster than the alternative, where you manually download the complete RPM packages using the rpm command.

Typically, you keep your system up to date with the graphical Update Agent because it’s easy to use. However, knowing how to run Yum from the command line is good, just in case you have problems with the Update Agent.