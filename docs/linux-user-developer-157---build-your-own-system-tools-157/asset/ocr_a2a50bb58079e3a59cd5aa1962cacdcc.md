# Photoshop on Linux

> Adobe's recent versions of Photoshop can run under Wine as PlayOnLinux takes care of the complications

Remove old Wine stains
Wine has an uninstaller (GUI and wine uninstaller appname > for the command line. Deleting ~/wine/ will remove all Wine-installed apps, unless you've used PlayOnLinux. With PlayOnLinux, make separate containers while managing installations easy, and each installation lives in ~/PlayOnLinux's virtual drives (vyp, a directory name with spaces and an apostrophe). Each application has a directory hierarchy of the Windows files needed. Within PlayOnLinux, selecting an app and clicking uninstall takes care of it. You can even create a directory with the same name during a PlayOnLinux install and let it overwrite the old one. To remove Wine, while your package manager for sudo apt-get purge remove wine) takes care of the software, your desktop will retain traces, such as “Open with...” options in menus – see the Wine FAQ for help.

Of all the applications keeping people from migrating away from proprietary platforms – and discounting games for now, as few businesses depend upon their ability to run Grand Theft Auto in the office – Photoshop is the strongest anchor to a Windows system for many people.

GNU Image Manipulation Program (GIMP) does more or less the same thing as Photoshop and even has much better batch processing for many jobs, but the UI is different. And however compatible GIMP developers make their offering with Photoshop in terms of functionality and the file formats handled, many users have invested thousands of hours in learning their craft on Adobe's software. They're not keen to move, so let us bring Photoshop and Linux together.

Download the multi-gigabyte zipped file of the Photoshop version you need. We went for Adobe Photoshop CS6 Design and Web Premium, with the DesignWebPremium_CS6_LSI16.7z file weighing in at 4.5GB. Then download the installer program: in our case, DesignWebPremium_CS6_LSI16.exe.

Before starting, do winetricks atmlib or you won't be able to open PSD files! From PlayOnLinux's installation page, select the graphics tab and then ‘Adobe Photoshop CS6’. You'll be told it also works with the CC (Creative Cloud) version of Photoshop.

PlayOnLinux selects the appropriate version of Wine – downloading it if it's not already on the system – and all libraries/DLLs, so the settings optimised for Photoshop CS6 are already installed. A Wizard (see the bottom-left image) walks you through the process.

After clicking through the usual End User Licence Agreement (EULA, possibly the most unread category of documents of our time, but a novel experience on a Linux desktop), unzip and installation begins. You can select a 30-day trial if you have no install key handy. There's a lot of downloading too, including the ubiquitous fetching of Microsoft fonts. Unless you have a lot of RAM, super-fast Internet and a quick SSD hard drive, you may want to put the kettle on at this point. Or even go out for lunch.

Back from lunch? Good. Adobe's claim that you'll get “blazingly fast performance” with the Mercury Graphics Engine could be behind CS6's seeming inability to install properly with Wine on our test machine with an Intel graphics chipset. Our NVIDIA-equipped box (with default Ubuntu installed and no driver tweaking) worked just fine.

Not being of a particularly artistic nature (as shown below), all that can be reported of the quality here is that Photoshop seems to work quite well, with a gold rating for compatibility in the Wine database.

![](bbox=[0.08, 0.62, 0.41, 0.82])

Above PlayOnLinux Installation Wizards are about as straightforward as they come

![](bbox=[0.42, 0.62, 0.95, 0.9])

Right If you get runtime errors, try setting PlayOnLinux too Windows 7 for your version of Photoshop