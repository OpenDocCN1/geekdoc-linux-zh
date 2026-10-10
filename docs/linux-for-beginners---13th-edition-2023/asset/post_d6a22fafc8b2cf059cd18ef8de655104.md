
## Linux Tips and Tricks

As you’ve seen, the Linux Terminal is quite an exceptional environment. With a few extra apps installed, and a smidgeon of command knowledge, incredible, and often quite strange, things can be accomplished.

### TAKING COMMAND

There are countless Linux tips, secrets, hacks and tricks out there. Some are very old, originating from Linux’s Unix heritage, while others are recent additions to Linux lore. Here’s our favourite ten tips and tricks.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_63_0.png)

```bash
sudo apt-get install emacs25
emacs -batch -l dunnet
```

Dunnet is a text adventure written by Ron Schnell in 1982, and hidden in Emacs since 1994.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_63_1.png)

![](img/7801ba6bee6a3a08f7f02897cdbcd867_63_2.png)

```bash
sudo apt-get install elinks
elinks
```

Enter the website you want to visit.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_63_3.png)

![](img/7801ba6bee6a3a08f7f02897cdbcd867_63_4.png)

```bash
sudo apt-get install moon-buggy
moon-buggy
```

Then:

Enjoy.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_63_5.png)

![](img/7801ba6bee6a3a08f7f02897cdbcd867_63_6.png)

```bash
wget https://gist.githubusercontent.com/sontek/1505483/raw/7d042716ea57e69fb52632fee09f42753361c4a2/snowjob.sh
chmod +x snowjob.sh
./snowjob.sh
```

![](img/7801ba6bee6a3a08f7f02897cdbcd867_63_7.png)

### MEMORY HOGS

If you need to see what apps are consuming the most memory on Linux, simply enter:

```bash
ps aux | sort -rnk 4
```

This sorts the output by system memory use.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_64_0.png)

### SHREDDER

When you delete a file, there’s a chance of someone with the right software being able to retrieve it. However, to securely and permanently delete a file, use Shred:

```bash
shred -zvu NAMEOFFILE.txt
```

Replace **NAMEOFFILE** with the name of the file to delete.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_64_1.png)

### ASCII ART

ASCII art can be quite striking when applied to some images. However, it’s often difficult to get just right. You can create some great ASCII art from the images you have by using img2txt:

```bash
img2txt NAMEOFIMAGEFILE.png
```

Replace **NAMEOFIMAGEFILE** with the actual name of the image file on your system. If img2txt install installed, use:

```bash
sudo apt-get install caca-utils
```

![](img/7801ba6bee6a3a08f7f02897cdbcd867_64_2.png)

### BBS

Back in the days of dial-up connections, the online world was made up of Bulletin Board Systems. These remote servers provided hang-outs for users to chat, swap code, play games and more. Using telnet in Linux, we can still connect to some active BBSes:

```bash
telnet battles.tarbbs.dyndns.org
```

There are countless operational BBSes available, check out **https://www.telnetbbsguide.com/bbs/list/detail/** for more.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_64_3.png)

### DIRECTORY TREES

If you want to create an entire directory (or folder) tree with a single command, you can use:

```bash
mkdir -p New-Dir/{subfolder1, subfolder2, subfolder3, subfolder4}
```

This creates a New-Dir with four sub folders within.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_64_4.png)

### FORGOTTEN COMMANDS

It’s not easy trying to remember all the available Linux commands. Thankfully, we can use apropos to help us. Simply use it, along with a description of the command:

```bash
apropos "copy files"
apropos "rename files"
```

![](img/7801ba6bee6a3a08f7f02897cdbcd867_64_5.png)

## Linux and the Big Bang

Linux is colliding particles, so we can understand how the universe works.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_65_0.png)

![](img/7801ba6bee6a3a08f7f02897cdbcd867_66_0.png)

### DID YOU KNOW...

that Linux is at the heart of the science behind the Large Hadron Collider? Using a combination of Red Hat Linux and CentOS (an ultra-stable distro built from the Red Hat core) as the base distributions of choice, scientists, developers and engineers have created SL – Scientific Linux.

Using SL as the base, the clever people at CERN have developed several different versions of their own custom Linux distro to help with all aspects of the LHC. Most notable is SLC, or Scientific Linux CERN, also known as CERN6. According to reports, there are over 36,000 systems running SL, and over 15,000 running SLC.

## Using the Terminal

### Creating Bash Scripts – Part 1

Eventually, as you advance with Linux Mint, you'll want to start creating your own automated tasks and programs. These are essentially scripts, Bash Shell scripts to be exact, and they work in the same way as a DOS Batch file does, or any other programming language.

#### GET SCRIPTING

A Bash script is simply a series of commands that Mint will run through to complete a certain task. They can be simple or remarkably complex, it all depends on the situation.

- **STEP 1** You'll be working within the Terminal and with a text editor throughout the coming pages. There are alternatives to the text editor, which we'll look at in a moment but for the sake of ease, we'll be doing our examples in Xed. Before you begin, however, run through the customary update check: `sudo apt-get update && sudo apt-get upgrade`.

- **STEP 3** To begin with, and before you start to write any scripts, you need to create a folder where you can put all our scripts into. Start with `mkdir scripts/`, and enter the folder `cd scripts/`. This will be our working folder and from here you can create sub-folders if you want of each script you create.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_67_0.png)

![](img/7801ba6bee6a3a08f7f02897cdbcd867_67_1.png)

- **STEP 2** There are several text editors we can use to create a Bash script: Xed, Vi, Nano, Vim, GNU Emacs and so on. In the end it all comes down to personal preference. Our use of Xed is purely due to making it easier to read the script in the screenshots you see below.

- **STEP 4** Windows users will be aware that in order for a batch file to work, as in be executed and follow the programming within it, it needs to have a .BAT file extension. Linux is an extension-less operating system but the convention is to give scripts a .sh extension.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_67_2.png)

![](img/7801ba6bee6a3a08f7f02897cdbcd867_67_3.png)

**STEP 5** Let’s start with a simple script to output something to the Terminal. Enter `xed` `helloworld.sh`. This will launch Xed and create a file called helloworld.sh. In Xed, enter the following: `#!/bin/bash`, then on a new line: `echo` `Hello World!`.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_68_0.png)

**STEP 6** The `#!/bin/bash` line tells the system what Shell you’re going to be using, in this case Bash. The hash (#) denotes a comment line, one that is ignored by the system, the exclamation mark (!) means that the comment is bypassed and will force the script to execute the line as a command. This is also known as a Hash-Bang.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_68_1.png)

**STEP 7** You can save this file, clicking File > Save, and exit back to the Terminal. Entering `ls`, will reveal the script in the folder. To make any script executable, and able to run, you need to modify its permissions. Do this with `chmod +x helloworld.sh`. You need to do this with every script you create.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_68_2.png)

**STEP 8** When you enter `ls` again, you can see that the helloworld.sh script has now turned from being white to green, meaning that it’s now an executable file. To run the script, in other words make it do the things you’ve typed into it, enter: `./helloworld.sh`.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_68_3.png)

**STEP 9** Although it’s not terribly exciting, the words ‘Hello World!’ should now be displayed in the Terminal. The `echo` command is responsible for outputting the words after it in the Terminal, as we move on you can make the `echo` command output to other sources.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_68_4.png)

**STEP 10** Think of `echo` as the old BASIC Print command. It displays either text, numbers or any variables that are stored in the system, such as the current system date. Try this example: `echo` `Hello World!` `Today` `is` `$(date +%A)`. The `$(date +%A)` is calling the system variable that stores the current day of the week.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_68_5.png)
