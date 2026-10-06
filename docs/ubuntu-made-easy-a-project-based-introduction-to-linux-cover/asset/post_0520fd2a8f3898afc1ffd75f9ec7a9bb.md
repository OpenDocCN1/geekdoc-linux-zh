
![](img/d35fa962e6f9664d66dc83916f426418_213_0.png)

# 9B-1: Installing the GNOME Desktop Environments

For all the changes that installing the GNOME desktop can bring, it is surprising how simple it is to do. Here are the steps:

- 1. Open a Terminal window, type `sudo apt-get install gnome-session-fallback`, and press ENTER.
- 2. Type in your password when prompted and press ENTER.
- 3. You will be asked if you wish to continue. Type y (for yes) and then press ENTER. The process will take up to a minute to complete.
- 4. When you are returned to the user prompt, type `sudo apt-get install indicator-applet-appmenu` and press ENTER. This process should take only a few seconds.
- 5. When you are back at the user prompt again, type `sudo apt-get install gnome-tweak-tool` and press ENTER.
- 6. When prompted, continue by typing y (for yes) and pressing ENTER. This process should take the longest, probably over a minute.
- 7. When the process is complete and you are back at the user prompt, close the Terminal.
- 8. Log out.

# 9B-2: Switching to the GNOME Desktop Environments and Back Again

Once the installation is complete and you have logged out, it is very easy to switch back and forth between desktop environments. At the login screen, click the Ubuntu logo next to your account name, as shown in

176 Chapter 9

Figure 9-24. Another menu (Figure 9-25) will appear, showing you the available desktop environments. These should be GNOME (for GNOME Shell), GNOME Classic (for the good ol' GNOME of days past), GNOME Classic (No effects) (for graphically challenged systems), Ubuntu (the default Ubuntu environment), and Ubuntu 2D (the default fallback mentioned in Chapter 3).

Just select the environment you want to use for the session you are about to log in, after which you will be returned to the regular login screen. Type your password there, press ENTER, and:

![](img/d35fa962e6f9664d66dc83916f426418_214_0.png)

Figure 9-24: The Ubuntu logo in the login screen

![](img/d35fa962e6f9664d66dc83916f426418_214_1.png)

Figure 9-25: Selecting which desktop environment you want from the login screen

# Project YC: Switching from Unity to Cinnamon

Recently vying with Ubuntu in terms of popularity is another Linux distribution, based on Ubuntu, called Mint. Mint uses a desktop called Cinnamon, which might be described as a cross between GNOME Classic and MS Windows. It is a simple and yet very familiar-feeling environment, which might explain its popularity. Frankly, you don't have to switch to Mint to get it; you can do it yourself. To install Cinnamon (shown in Figure 9-26), you will have to add a repository to those already used by apt-get and the Ubuntu Software Manager, so you are branching out of the purist of the Ubuntu world, to speak. But if you want to give it a try, here's how you do:

- 1. Type sudo add-apt-repository ppa:gwendal-lehiban-dev/cinnamon-stable in your Terminal, and press ENTER. This adds the repository.
- 2. Type your password when prompted and press ENTER.
- 3. You will be asked if you want to continue with the process of adding the PPA or cancel. Press ENTER to continue (CTRL-C to cancel, just as it says in the Terminal).
- 4. Once you are back at your user prompt, update the database, as you learned to do in Chapter 8, by typing sudo apt-get update and pressing ENTER. This process will take a minute or so.

![](img/d35fa962e6f9664d66dc83916f426418_215_0.png)

Figure 9-26: The Cinnamon desktop environment

- 5. Next, install Cinnamon by typing sudo apt-get install cinnamon and pressing ENTER.
- 6. You will be asked if you want to continue. Type y and press ENTER. The download and installation will take a couple of minutes or so.
- 7. Once the installation is complete, you will be back at your user prompt. You can then choose the Terminal.

To see your new desktop environment, log out and then, once at the login screen, click the Ubuntu logo next to your username. At the top of the list that appears (which you saw earlier in the chapter when switching to the GNOME desktops), you will see a new entry in the list: Cinnamon. Click that and then proceed with the normal login procedures.

Once in the Cinnamon environment, you might want to make a few customizations so that the remnants of the Unity's Ambiance theme do not seem out of place with Cinnamon's Adwaita. To make the changes, follow these steps:

- 1. Click the Menu in the bottom-left corner of the screen, hover your mouse over Preferences, and click Cinnamon Settings.
- 2. In the Cinnamon Settings window, click the Other settings tab. Then, from the drop-down menu button next to the words GTK+, select Adwaita.
- 3. If you like, you can also change the icon theme by choosing among the choices in the drop-down menu button next to Icon theme.

178 Chapter 9

# 10

## GUTENBIRD
### Setting Up and Using Your Printer and Scanner

![](img/d35fa962e6f9664d66dc83916f426418_216_0.png)

Two of the most common computer peripherals are printers and scanners. This only makes sense, because it is those two tools that turn a web-surfing, game-playing, music-churning, number-crunching box of chips into a meaningful publishing tool—a virtual publishing house, if you will. These devices help you convert digital information into hard copy (in the case of printers) and convert hard copy into digital information (in the case of scanners). It is not surprising, therefore, that these tools often come together these days in the form of multifunction printers.

In this chapter, you will learn how to connect these useful devices to your computer, how to set them up, and how to use them. You'll also learn how to find and install new fonts so you can make your printed documents look their best. If you're more into working with your digital camera than with a scanner, you might want to sneak a peek at Chapter 13; otherwise, put on your printer's smock and read on.

# Printers

Unless the only thing you use your computer is for playing games, listening to MP3s, or stopping doors on hot, breezy days, you will no doubt want to hook up your machine to a printer. Despite the paperless-office era that the personal computer was supposedly going to usher in, it seems that the computer's strength as a desktop-publishing and general work tool has made producing-quality printed documents an even more attractive proposition than ever before.

# Confirming Your Printer Is Supported

Setting up a printer to work with your new system is a pretty easy task, and it seems that printer support in the Linux world gets better with each release. In general, support for most printers is pretty good, with very few cases and models struggling with compatibility.

If you really want to make sure your printer is supported, try it by following the instructions in the next section. If you are thinking about buying a printer or are trying to decide whether to switch to Linux, go to http://www.openprinting.org/printers where you can check an online database whether your printer is currently supported and, if so, to what degree. Listings for supported printers also include information on which drivers are best for your purposes. If you're thinking of buying a printer for your Linux system, those manufactured by HP and Epson tend to be a pretty safe bet. You may also consult Ubuntu's list at https://wiki.ubuntu.com/HardwareSupportComponentsPrinters

# Getting Ubuntu to Recognize and Set Up Your Printer

Printer handling in Ubuntu is pretty much a no-brainer, but Ubuntu automatically detects printers. If you have a USB printer, connect it to your computer and then power up your printer (vice versa should work fine, too). If Ubuntu recognizes your printer—and it will be set up automatically in the background, without needing to click a single button. The process only takes a couple of seconds, so you should be ready straightaway. To check that everything is fine, click the power button on the far right of the top panel and select Printers from the menu that appears (alternatively, search for Printers in the Dash). If your printer has been set up correctly, the Printing window will contain an icon with the make and model of your printer listed beneath it. There is nothing more for you to do in this case—your printer is set and ready to roll.

It is also possible, however, that Ubuntu will recognize your printer but not find a driver that is an exact match for. In this case, a window will pop up after you connect the printer, offering a substitute driver. If you find yourself in this situation, it wouldn't be a bad idea to print a test page to see whether the substituted driver worked as it should. You can do this by selecting Printers from the top panel's power button menu and then double-clicking your printer in the Printing window that appears. Printer Properties window will open. Make sure that Settings is selected from the list to the left of.
