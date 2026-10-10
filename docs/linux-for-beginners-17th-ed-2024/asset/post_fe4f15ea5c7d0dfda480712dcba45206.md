
## VPNS AND TOR

The previous steps can aid your online privacy but to really become anonymous you need a Virtual Private Network and Tor.

### STEP 1
A VPN is a remote server, or cluster of servers, that establishes a connection with your computer. The end result is that your computer’s identity on the Internet is hidden behind the VPN remote server; so you could live in the UK but have an IP address (the computer online identity) belonging to Iceland.

### How VPN works?

![](img/5019375da05cbf0090115165d80772a1_42_0.png)

### STEP 2
Most good VPNs charge a monthly or annual fee but it's worth the expense. We use CyberGhost, [www.cyberghostvpn.com](http://www.cyberghostvpn.com), which offers VPN connections for Windows, Mac, Mint (as well as other Linux distros), Android and iOS devices. Details for each OS can be found at [www.support.cyberghostvpn.com/hc/en-us/articles/213190329-Read-me-first.](http://www.support.cyberghostvpn.com/hc/en-us/articles/213190329-Read-me-first.)

![](img/5019375da05cbf0090115165d80772a1_42_1.png)

### STEP 3
Another option is to use Tor. Tor is an open network that helps you to mask activity to that hides your IP address behind countless nodes around the world. It’s available for Windows, Mac and Linux computers and is very easy to install and use. Start by navigating to [www.torproject.org/download/download-easy.html](http://www.torproject.org/download/download-easy.html) and clicking on the Download Linux 64-bit button.

![](img/5019375da05cbf0090115165d80772a1_42_2.png)

### STEP 4
When the download has finished, drop into the Terminal and enter the Downloads folder, `cd Downloads/`. Enter `ls` to check the tor.xz file is present, then enter `tar -xf tor-browser--linux-x86_64-0.4.8-en-US.tar.xz` to unpack regularly. So if your version is different press Tab to autocomplete the tor--browser--filename. When the files are unpacked, use `cd tor-browser_en-US/` to enter the new folder.

![](img/5019375da05cbf0090115165d80772a1_42_3.png)

### STEP 5
A quick `ls` reveals a couple of entries: a folder called Browser and a file called `start-tor-browser.desktop`. To start the Tor setup, type `./start-tor-browser.desktop`. This command launches the Tor setup, where you are offered two options: Connect or Configure. For most users, the Connect option will suffice. Click Connect when you’re ready.

![](img/5019375da05cbf0090115165d80772a1_42_4.png)

### STEP 6
After the connection is established, the Tor Browser launches. This is a customised version of Firefox that can help you to securely browse the Internet without fear of being viewed or tracked. Mixing both a VPN and Tor makes for an extremely secure and private connection to the online world.

![](img/5019375da05cbf0090115165d80772a1_42_5.png)

![](img/5019375da05cbf0090115165d80772a1_43_0.png)

> "Linux: the operating system with a CLUE... Command Line User Environment."
> - *Anonymous (Posted on comp.software.testing)*

![](img/5019375da05cbf0090115165d80772a1_44_0.png)

## Using the Terminal

The Linux command line, the Terminal, is an incredibly powerful environment. From it, you can bring the OS to its knees, or update it to something spectacular. You can hack into remote computers, look at an animated ASCII camp fire, install new apps and programs, watch Star Wars played out from a server in the Netherlands, and code intricate automated scripts.

In this section you will explore the intricacies of the Terminal, and how it works with Linux. You will learn how to manipulate the Linux file system from the Terminal, but you will discover some odd, but fun things you can do in the Terminal.

The Terminal rules supreme in the world of Linux. Learn how it works, and you can access all that power.

## Basics of the Terminal

Most operating systems use two kinds of interface, the GUI, which is the desktop that Windows, macOS and Linux Mint boot into and the command line. While modern operating systems shy away from the command line, Mint uses the Terminal to give the user greater control of the system.

## TAKING COMMAND

The command line, or Terminal, is an extremely powerful interface. Everything you can do on the desktop can be done within the Terminal. Let’s start by seeing how it works.

- **STEP 1** The Terminal can be accessed by either clicking on the Terminal icon on the Panel, located between the Firefox and Files icons or launched by opening the Menu and selecting it from the left-hand quick launch strip.

![](img/5019375da05cbf0090115165d80772a1_45_0.png)

![](img/5019375da05cbf0090115165d80772a1_45_1.png)

- **STEP 2** The Terminal gives you access to the Linux Mint Shell, called Bash, which gives you access to the underlying operating system. Everything in Mint, including the desktop and GUI, is a module running from the command line.

- **STEP 3** What you currently see in the Terminal is your login name followed by the name of the computer; as you named it during setup when you first installed Mint. The line then ends with the current folder name; at first this is just a tilde ~ , which means your Home folder.

![](img/5019375da05cbf0090115165d80772a1_45_2.png)

![](img/5019375da05cbf0090115165d80772a1_45_3.png)

- **STEP 4** The flashing cursor at the very end of the line is where your text-based commands are entered. You can begin to experiment with a simple command, Print Working Directory (pwd), which outputs the current folder you’re in to the screen. Type pwd and press Enter.

- **STEP 5** All the commands you enter work in the same manner: you enter the command, include any parameters to extend the use of the command and press Enter to execute the command line you've entered. Type into the Terminal: uname -a and press Enter. This displays some system information regarding Mint.

- **STEP 6** Before we get into entering commands, let's take a moment to see what menus the Terminal has to offer. The File menu option allows you to open a new Terminal, create a new profile, where you can alter the size, colours and behaviour of the Terminal, add a new tab, and close all current active Terminal sessions.

- **STEP 7** The Edit option lets you copy and paste commands to and from the Terminal and other sources; handy for when you want to copy a very long and complex command from a web page. It also allows you to edit the current profile preferences,

- **STEP 8** View and Search options let you alter the sizing of the Terminal window and of course search within the Terminal for any particular key words.

- **STEP 9** The Terminal entry extends the profile editing and sizing and allows you to alter the character encoding. Interestingly, you can also set it to a Read Only mode, which stops you from entering any commands into the Terminal; this is good for when you need to permanently display the Terminal contents.

- **STEP 10** Finally, the Help option displays the help contents and version number of the Terminal, or to be more precise, GNOME Terminal; we'll simply refer to it as Terminal in future. The Contents are worth having a quick read through, to help familiarise yourself with how the Terminal works.

## Update Mint via the Terminal

Up to now you’ve been using the shield icon to launch Mint Update Manager in order to update the system and upgrade the currently installed apps, tools and other elements. However, you can also accomplish a complete system update and upgrade from the Terminal.

## USING APT-GET

To update and upgrade via the Terminal you use the APT (Advanced Packaging Tool) command. It’s a powerful command and combines different elements depending on its use.

### STEP 1
Start by opening a new Terminal or if you already have one opened clear its contents with the clear command. This starts you off with a clean slate on which to work.

![](img/5019375da05cbf0090115165d80772a1_47_0.png)

### STEP 3
Apt-get is used to update and upgrade the software in Mint, as well as Ubuntu and other Debian-based distros. Using the Update element retrieves new package lists and updates the list of source files. Upgrade downloads and performs an upgrade to the latest versions of those files. To start the entire Upgrade and Update process, enter: `sudo apt-get update`, followed by your password.

![](img/5019375da05cbf0090115165d80772a1_47_1.png)

### STEP 2
Enter `apt-get` into the Terminal. This brings up a list of the most used apt-get commands, along with a brief description of what the command does. It’s worth having a look at, even if it doesn’t make a huge amount of sense at this time.

![](img/5019375da05cbf0090115165d80772a1_47_2.png)

### STEP 4
Notice now the addition of the sudo command. The sudo command once meant Super User Do; these days it’s more acceptable as Substitute User Do. It means that the administrative user (Super User) uses APT (Advanced Packaging Tool) to Get any Updates. Now try this: `sudo apt-get upgrade`.

![](img/5019375da05cbf0090115165d80772a1_47_3.png)
