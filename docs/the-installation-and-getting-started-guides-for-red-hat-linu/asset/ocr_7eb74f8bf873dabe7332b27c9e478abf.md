can edit the config file by hand or you can run Xconfigurator again and pick a monitor from our list that more closely matches the specs of your monitor.

The final configuration step consists of selecting the video modes that you want to include in your XF86Config file. Use the arrow keys to move the cursor up and down the list under each color depth (8, 16 and 24 bit). Use the [Spacebar] to select individual resolutions and the [Tab] key to move between color depth fields. When you have selected the video modes you want to use move the cursor to the "OK" button and press [Enter], or use the [F12] shortcut. An information screen will give you the most current information on selecting video modes, starting and stopping the X server.

# If You've Already Installed X

If you selected the "X Window System" component when you installed Red Hat Linux, but didn't choose to start X automatically when the system boots, you're all set. All you'll need to do is to get X running. As it turns out, there are two ways to do this. You can:

+   - Start X manually after you log in.
+   - Start X automatically whenever the system boots.

Let's start with the manual procedure.

# Starting X Manually

Red Hat Linux, during the installation, gives you the option of starting X automatically. If you didn't choose this option, you'll see the character-cell login prompt you saw when you first booted your Red Hat Linux system. In order to get X started, you'll first need to log in. Do so (using your non-root account), and then enter the startx command. The screen should go blank, and (after a short delay) you should see a graphical desktop with one or more windows. The appearance of the desktop you'll see will vary, depending on the packages you installed and other variables. (See Chapter 1 for more info.)