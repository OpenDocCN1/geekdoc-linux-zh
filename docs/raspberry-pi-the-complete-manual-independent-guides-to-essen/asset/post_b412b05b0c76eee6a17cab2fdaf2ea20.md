
# Getting started

## Install and use packages

### What you'll need...

**Apt command help page:**
[https://alex.de.net/man/8/apt](https://alex.de.net/man/8/apt)

**Apt-get help page:**
[https://manpage.linuxnet.com/manpages/sup/](https://manpage.linuxnet.com/manpages/sup/) [lucid/man/apt-get.8.html](lucid/man/apt-get.8.html)

## Install and use packages

The Raspberry Pi is great, but it's made better with the software you install onto it. On its own, the Raspberry Pi is a near-perfect mini computer. It already contains a wealth of educational software, a few games, some programming utilities and a number of system tools. But, as with most computers, this is only the tip of the proverbial iceberg. By installing more programs, you can do much more.

These programs, known as packages, are as wide and as varied as the developers who originally designed them. In Linux, if there's a need for a particular program, then someone develops one. They then put it out to the world and make the source code freely available, hence 'open source'. Once the program has been tested, it will eventually make its way onto one of the many remote servers for that particular Linux distro.

These remote servers, called repositories, or repos, contain all the elements of the package in order for it to be downloaded and installed onto your system. The process is very quick and easy once you know how it's done...

### Did you know...

If you press the **Tab** key, the command line will attempt to auto-complete your command for you – just press Enter to finish.

![](img/59caadfa348382a5c408c25137901e27_27_0.png)

## Update and upgrade

01 Getting hold of a package on the Raspberry Pi involves dropping into the command-line terminal, via the LXTerminal icon on the desktop, and entering a few commands. But before we do that, we need to make sure the system is up to date. Enter the following into the terminal:

```
sudo apt-get update
sudo apt-get upgrade
or
sudo apt-get update && sudo apt-get upgrade
```

## Search for a package

02 The apt-get command (Advanced Package Tool) is the key to downloading and installing packages on the Raspberry Pi. In the previous instance, we updated the existing packages and system, upgraded any that needed it, and updated the current package list. Now, let’s search the list of server packages for available games.

```
apt-cache search game | less
```

![](img/59caadfa348382a5c408c25137901e27_28_0.png)

## Apt searching

03 The current list you find yourself in is the name of all the packages labelled as ‘games’ from the available server. In the list, the part before the hyphen tells you the name of the package, which is what you will need to know to be able to install it. Use the arrow keys up/down to navigate, press ‘Q’ to exit.

## Installing a package

04 Using the up and down arrow keys, navigate the list. If you find something you like the look of, say *Angry Drunken Dwarves*, remember the name of the package, in this case ‘angrydd’, and press ‘Q’ to exit the list. To install the package, enter the following in the terminal:

```
sudo apt-get install angrydd
```

## Executing the package

05 The result of the previous command should be the successful download and installation of the game, *Angry Drunken Dwarves*. To execute the newly installed package, you can either run it from the LXDE Menu under Games > Angry Drunken Dwarves, or by typing in the following into the terminal:

```
angrydd
```

![](img/59caadfa348382a5c408c25137901e27_28_1.png)

## Remove a package

06 This installing of packages is perfectly fine, and you can see just how powerful a command Apt really is. But, what if you want to remove a package?

Using the Apt command again, let’s say we want to completely remove all trace of *Angry Drunken Dwarves* from the Raspberry Pi.

```
sudo apt-get --purge remove angrydd
```
Enter ‘Y’ to accept the removal.

## Apt Easter eggs

07 The Apt command is a short, non-menu-driven variant of the Aptitude command. This command has a rich history in Linux, and as a result has some rather special ‘features’, also known as Easter eggs. Purley for a little bit of fun, type in the following commands and see the results:

```
aptitude moo
aptitude -v moo
aptitude --vv moo
aptitude -vvv moo
aptitude ~vvvv moo
aptitude ~vvvvv moo
aptitude -vvvvvv moo
sudo apt-get moo
```

![](img/59caadfa348382a5c408c25137901e27_28_2.png)

## Man the Apt command

08 As you can see, there is more to the simple Apt command than what first meets the eye. There are many different sub-commands that you can run, and many different variations in which to run them.

If you want to see what else the Apt command can do, enter the following:

```
man apt
```

![](img/59caadfa348382a5c408c25137901e27_28_3.png)

## Use graphical installations

### What you'll need...

**Synaptic:**
www.cncityng.org/synaptic/

![](img/59caadfa348382a5c408c25137901e27_29_0.png)

Would you prefer a graphical interface to install new programs? If so, then read on...

If you're new to Linux, you may find using its built-in Apt package management tool a bit intimidating and confusing. The apt-get command is used for installing applications through the internet, connecting to the remote servers – called repositories – which house the programs as packages. But it is used through the terminal command prompt, which can be daunting, so we need an alternative: a desktop environment interface method of getting hold of packages.

This is where Synaptic comes in. Synaptic is a friendly-looking graphical interface to the apt-get terminal command which allows you to manage your application installations, and removals, through the already familiar desktop environment. Think of it as a kind of online shop where you can pick and choose the programs you want and have them downloaded and installed onto your Raspberry Pi without you having to drop into the terminal.

![](img/59caadfa348382a5c408c25137901e27_29_1.png)

## Update the system

01 Unfortunately, if you have an aversion to dropping into the command-line terminal, then you're going to be stuck at the first step. Before we install anything, we need to make sure that the Raspberry Pi is fully updated and any existing packages are upgraded. Simply enter the following into the LX Terminal:

```
sudo apt-get update
sudo apt-get upgrade
```

![](img/59caadfa348382a5c408c25137901e27_30_0.png)

## Installing Synaptic

02 To install Synaptic, you'll first need to enter the LX Terminal and run the command below – don't forget to type Y to any prompts asking you to accept the installation:

```
sudo apt-get install synaptic
```

![](img/59caadfa348382a5c408c25137901e27_30_1.png)

## Running Synaptic – Part 1

03 In essence, that's all you need to do. Synaptic is now installed and ready to use. However, due to its complexity, there may be some bugs that need ironing out first, so it's best to follow these steps. To test if Synaptic is working okay, first enter the following command into the terminal.

```
gksudo synaptic
```

![](img/59caadfa348382a5c408c25137901e27_30_2.png)

## Running Synaptic – Part 2

04 You should be now looking at the Synaptic program window, where you can scroll through the list of available programs and click on each to download and install. Now we need to test whether it will run from the LXDE menu. Click on the icon in the bottom left, then go to Preferences > Synaptic Package Manager.

## Running Synaptic – Part 3

05 Running Synaptic from the LXDE menu results in an error. Don't panic; however, all it's doing is asking for a password. Enter the following password into the box:

```
raspberry
```

This is the default Pi password so we're assuming you have not changed it!

## Fixing Synaptic – Option 1

06 This will temporarily fix the issue, but to permanently resolve it, do one of the following. First, right-click the Synaptic icon in the menu and left-click Properties. In the Executable text box, change the text to add the gksudo command. So instead of 'synaptic-pkexec', it will read:

```
gksudo synaptic-pkexec
```

## Fixing Synaptic – Option 2

07 The second, and best, option is to drop back into the terminal and alter the way in which the program is executed from the menu. All that is needed is to change one line so another, so that the gksudo command is again used instead of the plain synaptic-pkexec. From the terminal, type:

```
sudo nano /usr/share/applications/synaptic.desktop
```

Change Exec=synaptic-pkexec to ...

```
Exec=gksudo synaptic-pkexec
```

## Synaptic fully working

08 After you've entered those changes, exit nano via Ctrl+X, then press Enter a couple of times to get back to the command prompt. You can now launch Synaptic from the menu or by entering the following command when you're in the terminal:

```
gksudo synaptic
```

![](img/59caadfa348382a5c408c25137901e27_30_3.png)
