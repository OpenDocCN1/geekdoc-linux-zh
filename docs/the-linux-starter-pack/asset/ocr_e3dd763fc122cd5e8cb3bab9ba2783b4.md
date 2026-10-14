# Answers

# Get gaming!

Q I'm bored with playing Same Gnome, Mines and Chess. Are there any other decent games available for Ubuntu?

A Yes! Ubuntu includes a handful of simple games with the default installation, but these are by no means the limit. Other games that you can access through Ubuntu include Battle for Wesnoth, a turn-based strategy game set in a fantasy world, SuperTuxKart, a game similar to Super Mario Kart, Vega Strike, a space trading game, and our personal favourite: Crack Attack. You can add these by going to Applications > Add Remove and choosing to see all available applications. Then click on the Games group on the left-hand side and you'll see a big long list of games that you can choose from. Simply select one or more and click on the Apply Changes button to be prompted for your password prior to Ubuntu downloading and installing the games. Be aware that some games, such as Vega Strike and Open Arena have some very large downloads, so be patient while they're downloading; Ubuntu will keep you up to date with how it's doing and give you an ETA for finishing the download.

that is commonly supplied with every camera. Ubuntu will automatically acknowledge the presence of a camera and attempt to import the pictures into GThumb, which is a picture-handling utility within Ubuntu. However, there is a better option called F-Spot (found under Applications > Graphics) that allows you to import pictures into a library ordered by time. You'll need to disable GThumb's automatic import though, by going to System > Preferences > Removable Drives And Media and unticking the option under the Cameras tab. F-Spot is pretty easy to use, and you'll be able to perform some minor editing with it. You can even export your photographs to Picasa Web or Flickr.

![](bbox=[0.43, 0.27, 0.89, 0.49])

F-Spot takes the pain out of organising your photos.

# Photography

Q I've just bought a digital camera. Will Ubuntu allow me to import my photographs and help me manage my photo collection?

A It depends on whether your camera supports mass storage or not. Mass storage is when a computer treats a camera or USB key like just another disk, which is automatically mounted and made available for Ubuntu. If your camera does support this, then you can simply link it up using the USB interface

# Using the terminal

Hang around any number of Linux geeks and it won't be long before they descend into a weird world of uttering words without meaning. Things like cd or ls, or even the more exotic-sounding grep may mean nothing to you now, but take the time to learn about the terminal and you too can harness the power of the command line.

At its most basic, the command line is a way to enter one or more commands that will interact in a low level with the Linux operating system. You can access the terminal (or command line) by one of two ways; you can go to Applications > Accessories > Terminal to open up a terminal as part of your desktop, or you can press Ctrl+Alt plus any key from F1 to F6 to access one of six different terminal windows. If you do it the Ctrl+Alt way then you'll need to login with your username and password, and if you need to return to your desktop just press Alt+F7. Don't worry about logging in multiple times; Ubuntu allows this, and it can come in handy if you need to run a command in the background while you're working on something else.

The first command you'll learn is ls, which lists the contents of the current directory. If you want to see more information, you can use the command like so:

ls -al

which will give you a more detailed listing of all the files and directories, including the hidden ones, that are located in the current directory. But how do you know which directory you're currently in? Look at the following example:

andrew@teletrain:~/Documents$

The first part (before the @ sign) tells me that I am logged on as the user andrew. The name of the machine is teletrain (the part after the @ sign) and I am currently working in the Documents directory which is a sub-directory of my home directory (denoted by the tilde (~) character). As you move through the file system using the terminal, the bit after the colon in the prompt will tell you exactly where you are.

directory. It's not inconceivable that you might one day enter a command like this one:

cd ../../..

that would move you up four levels in your directory hierarchy.

# Putting it together

One of the strengths of the command line is the ability to string several commands together in order to accomplish multiple tasks. Here at LXF Towers, we like to use the command line as it can be quicker, and a good example of this is when we update our Ubuntu installation. To do this, we enter the command:

sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get dist-upgrade -y

which will update the software repository information, install any upgrades and also install any more complicated upgrades. All we will have to do is enter our password once, as we have chained the commands together using the two && signs.

An alternative to this, using the ls command, might look like this:

ls -al | less

Instead of simply running the commands in order, this actually sends the output of the ls -al command to the less command, allowing you to easily scroll up and down using the cursor keys to see your directory contents. When you're finished, tap the Q key to return to the command line.

# Wading around

Moving to and fro within your filesystem is pretty easy to do and relies on the cd (change directory) command. Just typing it by itself and pressing the Enter key will automatically move you back to your home directory (~). The same effect can be had by entering the command:

cd -

The cd command is relatively simple to use and relies on you entering the details of the directory that you want to move into. For example:

cd ~/Music

would move me into the Music directory under my home directory. If you wanted to move up a directory, then you could enter the command:

cd ..

and Ubuntu would understand this. A single period (.) stands for the current directory, while a double period (..) stands for the immediate parent