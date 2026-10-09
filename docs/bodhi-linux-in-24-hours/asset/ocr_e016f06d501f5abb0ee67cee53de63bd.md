program called . This allows you to create an image (ISO file) of your system, including all your customizations and, if you wish, your documents, photos, and other data files, which you can then install on an optical disc (a recordable DVD) or on a USB memory stick (pen drive). With this DVD or USB stick you can run, and if necessary install, your system on any computer.

Remastersys is on your system, and it can be run from Terminal, but it will make life easier in the future if you set up a personal application launcher for it.

+   1) Run Eversthang and enter the first four letters of *personal*. The Personal Application Launcher dialog box opens.
+   2) Click Add to add a personal launcher; then at the Desktop Entry Editor type **Remastersys** in the Name field, and in the *Application* field *remastersys-gtk*.
+   3) If you want to set up an icon for your launcher, click on the Icon tab, then click on the icon box and navigate to: /usr/share/icons/MaXo-ReMix/apps, then scroll through the list for a suitable icon. Click OK.

+   4) At the General tab, type REMASTERSYS IN THE GENERIC NAME' field, and SYSTEM IN CATEGORIES.
+   5) At the Options tab, make sure that 'Show in Menus' is selected. The other two options should not be selected.
+   6) Click Apply; Then Close. Remastersys will appear in the menu System, under System Tools (if it doesn't, restart Enlightenment).

BEFORE BACKING UP YOUR SYSTEM WITH REMASTERSYS, YOU SHOULD FIRST RUN BLEACHBIT AND BLEACHBIT AS ROOT TO REMOVE UNNECESSARY FILES. YOU SHOULD INCLUDE THE 'FREE DISK SPACE' OPTION TO MAKE THE IMAGE AS COMPACT AS POSSIBLE. (THIS WILL TAKE A LONG TIME TO EXECUTE, AS IT INVOLVES SHUFFLING FILES AROUND ON THE HARD DISK.)

THE INSTRUCTIONS FOR USING REMASTERSYS TO CREATE AN IMAGE OF YOUR SYSTEM ARE AS FOLLOWS:

+   1) Close all open applications, run Remastersys, and at its dialog box choose the Settings tab. Here you can enter any files or directories you wish to exclude from your image. For example, if you wish to exclude your Movies and your Pictures folders, you would enter /home/bobhj32/Movies:/home/bobhj32/Pictures (replacing **bobhj32** by your username).
+   2) Click the Actions tab, close all open windows (apart from the Remastersys window) and click Backup. Remastersys will then set to work creating the ISO image of your system, a process that will take about an hour.

The ISO file will be located in the /home/remastersysy directory. To see it, run Nautilus, click the box at the left of the toolbar (to the left of 'Home' - the box is marked with a small left-