# # Distros

# # (Re)Master Ubuntu

Point and click your way to a custom spin.

ne reason that’s contributed to the staggering number of Ubuntu respins is the availability of easy-to-use tools that help you create a customised version of the installation. While the process for creating a customised distribution isn’t rocket science, with Ubuntu it’s a walk in the park.

One of the easiest to use is Bodhibuilder, which is a fork of the popular Remastersys script (see box, below). Despite its name, Bodhibuilder can create customised respins of Ubuntu and any of its derivatives like Linux Mint and Bodhi Linux. The latest version of Bodhibuilder works on both 32- and 64-bit installations, and builds UEFI compatible images. The Bodhi Linux project in fact uses this script to churn out their official releases as well.

To create your customised Ubuntu spin, it’s best to first build an installation from scratch. We’d advise you to do this inside a virtual machine to save yourself a lot of hassle. Begin the process by downloading the minimal Ubuntu ISO that includes the least number of components required to boot Linux.

When you install Ubuntu from the minimal ISO, the installer will bring up the tasksel tool to enable you to select the additional components you’d like to install. There are options to help you tailor your installation as a mail server, file server and various other types of servers. We are, however, interested in the several desktop-centric options that cover all the popular desktop environments including Mate, Gnome, Xfce, LXDE and Budgie with both vanilla and extended application suites.

We prefer to start with a minimal desktop and then flesh out the installation from within. Besides the desktop options, it’ll give you options that will fetch programs of a particular genre, such as audio recording/editing suite, photograph touch-up and editing suite, video creation and editing suite, and more. Once you’ve made the selection, the installer will fetch the required components from the online repository and install them just like the installer on a regular Ubuntu ISO. For your first build, we’d suggest you select one of the minimal graphical environments.

# ## Start building

After installation, boot into it and modify things as you see fit. You can install and remove any applications using the package manager and also by downloading pre-packaged binaries for app not in the official repositories. Also feel free to customise the desktop by modifying the various components like the menus, wallpaper and themes.

When you are done customising your installation, you can install Bodhibuilder. The script is available as a pre-packaged binary at the project’s Sourceforge page (https://sourceforge.net/projects/bodhibuilder). Bodhibuilder is intuitive to use once you get familiar with its interface. The first thing you should do is switch to the Settings tab to define the name of your custom distribution. Use the various text boxes under this tab to set up the username of the Live environment, the name of the ISO image file, and the name of the distro as it’ll appear in the GRUB boot menu. The working directory is where the script will generate and place the custom ISO image. It’ll first create a folder named Bodhibuilder under the specified directory to conduct all its operations. Make sure the folder is on a partition that has ample free space and is formatted with a Linux filesystem, like EXT4.

Advanced users get the option to list the files and directories they’d like to leave out of the generated ISOs. Similarly, by default Bodhibuilder will include all icons and locales under the /usr/share/icons and /usr/share/locales directories. You can only include particular icons and locales by listing them in the space provided. There’s also space to list any squashfs images, but it’s best to leave it empty unless you know what you’re doing.

After describing your distro, switch back to the Actions tab that offers build options. Of the note are the Backup and Dist options. Backup will roll the installation into an ISO image with the same settings as your current desktop. It’s meant for your personal use and it includes all your user data and personal information.

For our purpose though, we’ll use the Dist option that will also create an ISO image, but will exclude all your

# ## FORK IN THE ROAD

Remastersys has always been one of the most popular scripts for transforming a customised Ubuntu installation into a bootable ISO image. It drew inspiration from Mandriva’s mivivecd, but was written for Ubuntu. When the original script ceased development, it was forked by several other projects, most notably Bodhi Linux and PinguOS. We’ve used the Bodhi Linux fork called Bodhibuilder in this article and you can just as easily use PinguOS’s fork named Pinguoy Builder.

Besides these, there’s now something of an official fork of the original script. Dubbed Linux Respin, this script is hosted at the original remastersys.org website. Unlike the other two however, Linux Respin focuses on creating custom spins from Debian and Linux Mint. There’s also a version that will work on one of Free Software Foundation’s favourite distributions called Trisquel GNU/Linux. The Linux Respin developers are working to port the script to Fedora installations as well, so keep your eyes peeled for news on that front.

![](bbox=[0.55, 0.76, 0.92, 0.93])

> If you have multiple users, specify the user whose settings will be used as default when using the Backup option.