![](Image00029.jpg)

![](Image00029.jpg)

LINUX:

Linux Terminal, basic functionalities and CLI (Kali Linux 2016)

Gary Mitnick

© 2016

© Copyright 2016\. All rights reserved.

First Edition: November 2016

No part of this book may be reproduced or transmitted in any form or by any means, electronic or mechanical, including photocopying, recording, or by any information storage or retrieval system without prior written permission from the author or copyright holder except in the case of brief quotations embodied in reviews.

Although the author has exhaustively researched all sources to ensure the accuracy and completeness of the information contained in this book, we assume no responsibility for errors, inaccuracies, omissions, or any inconsistency herein. Any slights of people or organizations are unintentional. Reader should use their own judgment and/or consult a programming expert for specific applications to their individual needs.

Table of Contents

[Introduction](#text00000.html__Toc467082192)

[Course Books](XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX)

[Intro to Linux terminal](#text00000.html__Toc467082194)

[Linux Command - Line Interface (CLI) Basics](#text00000.html__Toc467082195)

[Conclusion](#text00000.html__Toc467082196)

[Course Books](#text00000.html__Toc467082197)

# Introduction

Hello and welcome to this Linux Terminal tutorial this is the 2 nd installment to the hacking series.  This booklet is best served in a follow along manner.

# YOUR GIFT

Click Below for Your FREE Malware Protection Gift

[>>CLICK HERE<<](https://forms.aweber.com/form/28/192431228.htm)

[](https://forms.aweber.com/form/28/192431228.htm)

# Course Books

[![C:\Users\Garci\OneDrive\Kindle\Book Library\Non-Fiction Books\Gary Mitnick\Hacking - Gary Mitnick\KDP\HACKING - Book Cover.jpg](Image00000.jpg)](https://www.amazon.com/dp/B013JB35IK/)

[https://www.amazon.com/dp/B013JB35IK/](https://www.amazon.com/dp/B013JB35IK/)

[![C:\Users\Garci\AppData\Local\Microsoft\Windows\INetCacheContent.Word\Tor---Book-Cover-red.png](Image00001.jpg)](https://www.amazon.com/dp/B01M15T2GG/)

[https://www.amazon.com/dp/B01M15T2GG/](https://www.amazon.com/dp/B01M15T2GG/)

[![C:\Users\Garci\AppData\Local\Microsoft\Windows\INetCacheContent.Word\HACKING v2.jpg](Image00002.jpg)](https://www.amazon.com/dp/B01MXFX3BM/)

[https://www.amazon.com/dp/B01MXFX3BM/](https://www.amazon.com/dp/B01MXFX3BM/)

# Introduction to the Linux terminal

In this section I am going to introduce you to the Linux Terminal and show you some of its basic functionalities. To start off in Kali Linux, the terminal Icon is in the upper left corner, if you currently have it open it would be best to follow along with this course, you will have a much better understanding and be more familiarize with Linux at a quicker rate. If not, you can still follow along this course no problem. If you are following along with your device, you can go ahead and click on the terminal button. (The terminal button is circled in red in the next image)

![](Image00003.jpg)

This will open the terminal:

![](Image00004.jpg)

By default, it opens a root terminal in Kali. So, if you want to configure it for customization or personalization reasons we will go over how to do it. If you do not want to configure it, this is perfectly fine – you do not have to.  You don’t actually need to do anything else to the terminal beyond what you see above, it works just fine with its default looks and settings. However, 99% of the time people are interested in configuring the terminal to suit their own needs and purposes. For example, I for one will almost always increase the font size, so that it is clear and visible and so that I have a better overview of what I am doing at the moment and it also reduces eye strain according to some articles.

To configure the terminal, you can go ahead and right click anywhere in the terminal and click on “show menu bar”. (see images below)

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (24).png](Image00005.jpg)

![C:\Users\Garci\AppData\Local\Microsoft\Windows\INetCacheContent.Word\Screenshot (25).png](Image00006.jpg)

Now that the menu bar is visible, go ahead and click on “edit” and then “profiles preferences”. This next menu will then show up:

![C:\Users\Garci\AppData\Local\Microsoft\Windows\INetCacheContent.Word\Screenshot (27).png](Image00007.jpg)

From here you are given a great deal of options. One of the first you will see is that you can use a System Fix Width Font, if you click on “Monospace|20” you can change the font and the size here to your preference. You can also change the cursor shape, title of a command (tab), color change (tab), and the background (tab). On the background tab, you have 3 features, you can have a loid change of color, download any image from the internet to paste as your back ground, and you can even configure the level of transparency for your terminal. Something really cool here, is that you also have the option to have a fully transparent back ground. In the scrolling tab, there is another important feature, it is called “Scrollback” which is best kept checked “unlimited” unless you are severely limited in terms of Ram. All in all, you have the power to fully customize the terminal to any extreme liking.

Now that we have covered how to modify your terminal with various options per your liking and preferences. We can move on to the next very helpful tip: Open tabs in your terminal (same window) as opposed to having various terminal windows opened simultaneously. To open a new tab, you can go ahead and click on “File” and then “Open Tab” you can have various tabs of your terminal listed here (refer to image below) instead of having terminal windows open all at once. It is very easy to get confused trying to figure out which window is which or what you were doing on which one.

With tabs:

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (28).png](Image00008.jpg)

Without tabs:

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (30).png](Image00009.jpg)

If you don’t have the taps it is not actually very manageable to work on. Primarily because as previously mentioned there is a high risk of confusion between having many terminals opened at once. Having these tabs available at your disposal is going to help you out a lot as you progress through this course series and as you get into more complicated stuff.

Anyway, I just wanted to introduce you to the Linux Terminal. We have done some work with it before during the installation of Virtual Box and Virtual Box Guest Additions in [“Hacking: How to Create Your Own Penetration Testing Lab Using Kali Linux 2016”](https://www.amazon.com/dp/B01MXFX3BM/) but in there I mainly just gave you the commands and you basically just rewrote them or copy and pasted them and that was the end of it, but here in the next section I will start explaining the fundamental Linux Terminal Commands starting from the most common and basic ones and from there you will be able to see the logic of things and how this Linux Terminal works along with its functions. Once you learn these commands they will give you a HUGE amount of power.

All the power of your operating system rests on its terminal because it is a direct interface to the kernel of the system and it’s a lot faster than the graphical interface.

As a final keynote, once you learn how to use the Linux Terminal and get into the habit of typing in commands you will be able to use them for a wide variety of purposes including but not limited to penetration testing.  You will be able to use these commands beyond pen testing, for such things such as network administration, system troubleshooting, etc. so you are actually learning code for a wide spectrum of options and career opportunities as opposed to just learning this for penetration testing only.

# Linux Command - Line Interface (CLI) Basics

In this section, we will go over the basic commands which you will need in order to progress through this course. There are 4 basic commands – these 4 basic commands are used to navigate within the terminal, to go through the file system, to figure out where you are at the moment, to copy things, move things, to get listings of files, folders, to see the contents, remove them, change the ownership of files or change the modes of files. You will shortly see what I mean.

The following is a complete list of the commands:

Cd

Ls

Pwd

Cp

Mv

Cat

Less

Grep

Echo

Touch

Mkdir

Chown

Chmod

Rm

Man + help

Cd

First off we have “cd” which stands for Change Directories. If you just type in “cd /home/” and then hit ENTER you are going to navigate over to your home directory. So, you are literally changing your work directory by using “cd”.

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (31).png](Image00010.jpg)

Note: If you type in “cd ..” you will always go one step back. So “..” means previous folder. It’s a shortcut you will use often.

Ls 

Next up we have “ls”. “ls” shows you the listing off the current folder contents. You can also use, for example, “ls /home/” and you get the listing of a specified folder as well. Typing “ls” in and of its own will give you the listing of the current folder, as opposed to typing “ls” and then a path to a folder, which will give you a listing for a specified folder. In addition to that, you also have “ls – l” which will give you a long listing which will tell you who the owners are, the size, the date, the type, the permissions and so on and so forth. However, one of the more common usages of “ls” is “ls – la” to show the inner hidden files as well.

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (32).png](Image00011.jpg)

Pwd

The third function is “pwd” which stands for print working directory. You may find this a bit confusing, but if you notice in the images they all have a forward slash. The forward slash symbol “/” in all Linux-like systems simply refers to the root directory from where all the files are located from where everything begins. So, print working directory does exactly what the name itself says, it prints your current working directory.

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (33).png](Image00012.jpg)

Cp

Next up you have your “cp” command, which we have previously used to copy Virtual Box Guest Additions from one place to another in [“Hacking: How to Create Your Own Penetration Testing Lab Using Kali Linux 2016”](https://www.amazon.com/dp/B01MXFX3BM/) . It’s fairly simple. You type in “cp / path ”. So, if I for example, go ahead and type in “cp VBOCLinuxAdditions.run” and if I want to copy it to “/var/”. I will enter it as “cp -v VBOXLinuxAdditions.run /var/”

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (34).png](Image00013.jpg)

Note: the “-v” is very useful to have, it tells you what the machine is currently doing (you won’t get confused or think that it has lagged or crashed because you will have a status update. You don’t need it, but it is very beneficial to have especially for large files with a longer wait time.  The -v tells you what the machine is doing, but you can enter it as “cp VBOXLinuxAdditions.run /var/” if you do not want a live status update.

You may have noticed that all the commands above up to now and the rest we will be going over have their own arguments which can be passed to them to modify what the command does. You can view a listing of these arguments in the terminal as opposed to memorizing them all. So, let’s take an example of “cp --help” it is a universal way of getting help on a subject within a terminal. You type in the command, a space, then “--help”, press ENTER and you will get a listing of possibilities. It will look a bit messy and a bit difficult to see, but if you scroll upwards you can see all the arguments. They are all listed clearly here. You have the argument on the left (red) and then you have an explanation on what that argument does on the right ((yellow)refer to image blow)). It is best to memorize these as you go and as you progress through the course with the practice of these commands, as opposed to trying to memorize these all at once. The more you use these commands the more you will be remembering them more and more without wishing it, you will be caching the information, so to say (haha)

![C:\Users\Garci\AppData\Local\Microsoft\Windows\INetCacheContent.Word\Screenshot (48).png](Image00014.jpg)

If you scroll higher on this help menu you will come across “Usage”. In Usage, you get the format or the syntax of the command. So basically, “cp [option]… ([-T] specify your source and destination) Very simple. (see image below)

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (49).png](Image00015.jpg)

This is universal for all the commands; you can always use the help menu. However, in addition to the help menu, you also have “man pages”. So, if you type in “man cp” the man pages on “cp” will give you a ton of information - It gives you the name (it’s called synopsis here) but basically the syntax of the command, the full description of what the command does, full description of the argument, you even get the author who wrote in some notes, as well as the copyright info and some references to other things as well.

Mv

Next on the list is “mv” which stands for move and will cause a folder to move. This is also how you rename folders and files too. To rename a file you must type it in as “mv file.ext filerename.ext ” as an example if I want to rename VBoxLinuxAdditions.run I will enter it as “mv VBoxLinuzAdditions.run filerename.ext or new name.ext ” so it will look like this: “mv VBoxLinuzAdditions.run RandomIsNotSoRandom.run” since I want to rename this file to RandomIsNotSoRandom.run . If I want to move this file to my home directory I will enter it as “mv RandomeIsNotSoRandom.run /home/”

Note: When you delete something with “mv”, or when you move something over something else, it is very difficult to recover, if not impossible. Also, be very careful with deleting files in Linux - once you delete them from the terminal you will not be able to recover them. There are some complex procedures that might be able to give you a fraction of what you wanted to recover, but if you remove it from the terminal it is very difficult to recover. It’s not like windows or something of a kind when you delete something in windows, you can always recover, you basically didn’t even delete it. You just don’t see it anymore. But here, when you delete something its gone permanently. So, take great caution, take care but don’t be afraid. Over a period of time, these things become second nature to you. You will take it into consideration without even thinking about it.

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (36).png](Image00016.jpg)

Cat

Next up we have “cat”. “cat” shows you the entire contents of the file (whatever that might be) it is very good for files that you do not wish to make any accidental changes to but you want to quickly see what is located within a file.

Note: Terminal text editor Nano is a good text editor from the terminal. You will need to learn how to use the terminal’s text editors because you don’t want to be switching back and forth between GUI text editor’s and working on something on a terminal. It’s extremely time consuming plus, here on Kali Linux, you can edit things in root. However, if you are using some other distribution or something of a kind, most of the GUI text editors will not be able to run as root. You will get an error message. So, that can be a bit problematic. That’s why you should always learn how to use text editors that are from the terminal.

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (37).png](Image00017.jpg)

Less

“less” is very similar to “cat” it shows you the content but it creates a new workspace within the terminal itself and when you press “q” in your keyboard it is going to exit and nothing will be displayed. so, it is very nice in terms of being neat and organized.

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (38).png](Image00018.jpg)

Grep 

Next on the list is “grep” which is how you pull something (grep) from something else. Linux is case sensitive so when you are grepping, it is going to check whether you are searching lower case or uppercase. Grep is very important; it is a huge part of the Linux Terminal alongside with “cat” and “less” for filtering through text files. If you continue down this course, you will at some point be doing large network scans and you will need to create files from where you can pull useful information from which you will later pass on to other tools to move forward. OKAY!

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (40).png](Image00019.jpg)

Echo

Next is “echo” – type in echo “I am alive” and it will echo these words – it literally is an echo. When you type something into it will echo the words you have typed back to you. 

Note: by using the up and down arrow keys in your keyboard you can scroll between past commands. Echo is a very nice command to have, you can change variable names and values with it. We will use this a bit more as we progress through the course where we will have clear examples that directly relate to what we are doing, which is basically pen testing then you will see more advance usage of these commands – especially “grep”.

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (41).png](Image00020.jpg)

Touch

“Touch” is a quick way to create files. So, for example, I can type “touch file1 file2 file3” and press ENTER followed by “ls”. You see it has immediately created 3 files. This is a very quick method to create any number of files that you wish. You can also specify folder paths. You can create file1 in home, file2 in var, file3 in varlog and so on and so forth.

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (42).png](Image00021.jpg)

Mkdir

Next you have “mkdir” it stands for Make directory. So, if you type this in, you are making some sort of a directory. “mkdir name of directory” then hit ENTER and “ls” it will state this file is a directory, which is “ name of directory” above . I can even navigate to it – there is nothing in it, but you get the idea. You can make directories in such a fashion.

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (43).png](Image00022.jpg)

Chown

“Chown” stands for change ownership. It allows you to change the ownership of a file. Now since we only have a single user here, which is root, there isn’t any point in doing so. Unless we create some other new users – however we do not need them. But just to show you how this would work for example, if the owner of the file was not root and you want to change it to root, you would need to do the following.

Type, “chown”, then you would type the username “:” – colon and the user group. So, the user group and the username are usually the same, unless you have some bigger servers or something like that. Then just specify the name of the file. You can type “test” – there it will effectively change the ownership of the file test to the username root, who is from the user group root. If I do “ls la” it stats who the owners are and which groups owned the files.

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (44).png](Image00023.jpg)

Chmod

“chmod” is another more used command. This command allows you to change file permissions. This is something that you will need to use daily and quite often. We will deal with it in greater depth as we proceed through the tutorial. You will also need to be acquainted with bash scripting. Bash scripting like the terminal itself – so pretty much all the commands used in the terminal can be used by scripting as well.

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (45).png](Image00024.jpg)

Rm

There is one more command that I would like to show you, and this can be a very dangerous command, indeed, it can mess you up in ways you can’t even begin to imagine yet – that is the command “rm” . “rm” is basically remove. Once you remove things with this commands it is next to impossible to recover anything from it. So, if I type in “rm test.sh” it is going to remove it and it is no longer going to be there. If you try to remove a directory using “rm” you will not be able to do it because it also serves as a failsafe. So, you wouldn’t delete a full directory because you wouldn’t be able to recover it and that would be bad. When you are using “rm” you always want to be asked questions.

![C:\Users\Garci\OneDrive\Pictures\Screenshots\Screenshot (46).png](Image00025.jpg)

Man + help

If you get stuck don’t worry about it, I get stuck all the time. But if you get stuck and you don’t know what to type in or what argument to pass, just type in “—help” and look at what you can type, read a little bit and then use the options. Try it out, sometimes it will work, sometimes it won’t, often, you will be able to figure it out from the help menu. If you can’t figure it out from the home menu just type in “man rm” and you can read pretty much everything there is to know about a command here. And if you can’t perform the task, if you can’t find anything useful here, forums are your next best bet. Trust me you will succeed in doing it.

Cd

Ls

Pwd

Cp

Mv

Cat

Less

Grep

Echo

Touch

Mkdir

Chown

Chmod

Rm

Man + help

# Conclusion

In any case this was a brief introduction to the basic commands of Kali Linux that we will use to do and learn more about ethical and unethical hacking– please make sure that you know the functions of each of these commands, then later we will get in depth, and do more advanced stuff and use more advanced commands by combing them and so on. In any case I bid you all farewell and I hope to see you in the next course book installment. Stay tuned for future updates!

Ps. This series will be compiled into 1 book when it is completed. You will receive your copy for free, via email.

# YOUR GIFT

Click Below for Your FREE Malware Protection Gift

[>>CLICK HERE<<](https://forms.aweber.com/form/28/192431228.htm)

# [](https://forms.aweber.com/form/28/192431228.htm)

# Course Books

[![C:\Users\Garci\OneDrive\Kindle\Book Library\Non-Fiction Books\Gary Mitnick\Hacking - Gary Mitnick\KDP\HACKING - Book Cover.jpg](Image00026.jpg)](https://www.amazon.com/dp/B013JB35IK/)

[https://www.amazon.com/dp/B013JB35IK/](https://www.amazon.com/dp/B013JB35IK/)

[![](Image00027.jpg)](https://www.amazon.com/dp/B01M15T2GG/)

[https://www.amazon.com/dp/B01M15T2GG/](https://www.amazon.com/dp/B01M15T2GG/)

[![C:\Users\Garci\AppData\Local\Microsoft\Windows\INetCacheContent.Word\HACKING v2.jpg](Image00028.jpg)](https://www.amazon.com/dp/B01MXFX3BM/)

[https://www.amazon.com/dp/B01MXFX3BM/](https://www.amazon.com/dp/B01MXFX3BM/)