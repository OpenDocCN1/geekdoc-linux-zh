> NOTE Even though it's easy to put a large shell script in the %pre and %post sections, once your scripts get to a certain complexity, you should probably consider putting them into a script on your Kickstart server that you then retrieve via wget and execute. An extra benefit of this approach is that you could perform logic within the %pre and %post sections to pull custom shell scripts based on the type of server you are installing.

Probably the simplest way to start your pre- or post-installation script is with the Kickstart Configurator tool. Each installation script is set up as a category in the left pane with a section in the right pane where you can write your script. You can even specify a custom interpreter for your shell script via the GUI. Even the GUI provides a warning in these sections that a mistake in these shell scripts can cause the Kickstart as a whole to fail.

An important distinction to make between the pre- and post-installation scripts is that the pre-installation script is run within the installer environment whereas the post-install script by default is run within a chroot environment inside the installed system. That means that you can install additional packages or perform other custom tweaks within the installed system in the post-install section, while in the pre-install section you would mostly want to tweak preseed settings.

# PXE Boot Server Deployment

While the examples I gave earlier are a good place to start, when you want to automate server installs, you ultimately need to set up a PXE boot server to manage the process. After all, do you really want to manually go to each new server and insert a CD-ROM? What if your server is on another continent or you have 200 servers to install? With PXE boot deployment, your new server boots from the network, pulls its install image from the PXE server, and then starts the installation process—all over the network.

There are a number of different services you need for PXE boot deployment to work:

+   - A DHCP server configured for PXE booting to give each install an IP address and point it to the TFTP server and boot program to load
+   - A TFTP server to serve the PXE boot loader program over the network
+   - A Web server to host any Kickstart and preseed files and any custom scripts