![](cover.jpeg)

Raspberry Pi:

How To Master Raspberry Pi

![](images/00002.jpg)

By

Richard Dorsey

![](images/00001.jpg)

© Copyright 2017 by Richard Dorsey - All rights reserved.

The follow eBook is reproduced below with the goal of providing information that is as accurate and reliable as possible. Regardless, purchasing this eBook can be seen as consent to the fact that both the publisher and the author of this book are in no way experts on the topics discussed within and that any recommendations or suggestions that are made herein are for entertainment purposes only. Professionals should be consulted as needed prior to undertaking any of the action endorsed herein.

This declaration is deemed fair and valid by both the American Bar Association and the Committee of Publishers Association and is legally binding throughout the United States.

Furthermore, the transmission, duplication or reproduction of any of the following work including specific information will be considered an illegal act irrespective of if it is done electronically or in print. This extends to creating a secondary or tertiary copy of the work or a recorded copy and is only allowed with express written consent from the Publisher. All additional right reserved.

The information in the following pages is broadly considered to be a truthful and accurate account of facts and as such any inattention, use or misuse of the information in question by the reader will render any resulting actions solely under their purview. There are no scenarios in which the publisher or the original author of this work can be in any fashion deemed liable for any hardship or damages that may befall them after undertaking information described herein.

Additionally, the information in the following pages is intended only for informational purposes and should thus be thought of as universal. As befitting its nature, it is presented without assurance regarding its prolonged validity or interim quality. Trademarks that are mentioned are done without written consent and can in no way be considered an endorsement from the trademark holder.

Table of Contents

![](images/00002.jpg)

[Introduction](#index_split_003.html_filepos4289)

[Chapter 1: What is Raspberry Pi?](#index_split_004.html_filepos6248)

[Chapter 2: Under the Hood](#index_split_005.html_filepos10154)

[Chapter 3: Setting Up](#index_split_006.html_filepos20270)

[Chapter 4: Programming Essentials](#index_split_007.html_filepos29788)

[Chapter 5: Project Ideas](#index_split_008.html_filepos63367)

[Chapter 6: Your First Project - A Portable Superconsole](#index_split_009.html_filepos68062)

[Conclusion](#index_split_010.html_filepos90419)

Introduction

![](images/00002.jpg)

Congratulations on downloading Raspberry Pi and thank you for doing so.

The following chapters will discuss the innumerable ways that you can work with the super versatile Raspberry Pi computing microboard - or, rather, how you can make it work for you.

If you’re reading this, I’m sure you’ve heard at least a couple things about this extremely neat gizmo. Maybe you’ve heard of people building massive arcade cabinets at home where they and a friend can play their favorite games from back in the day; maybe you’ve seen smart mirrors that show people a feed of important information as they get ready in the morning; or maybe, you just ran into an article about them online and you’re just wanting to know what they can do.

More likely, since this is a programming essentials book, you’re trying to understand how to get the most out of your Raspberry Pi by writing your own scripts or working with other people’s scripts.

Regardless of your reasoning, I can say that getting the Raspberry Pi will most certainly be one of the best decisions that you’ve made recently. You’re going to be able to do a whole host of super cool things with it and learn a lot about technology and engineering in the process.

There are plenty of books on this subject on the market, thanks again for choosing this one! Every effort was made to ensure it is full of as much useful information as possible, please enjoy!

Chapter 1

![](images/00002.jpg)

What is Raspberry Pi?

For the intents and purposes of this book, we’re going to start from nothing and assume that you know, well, nothing. So to do that, we have to start with the extremely basic questions. The most basic question of all is this: what is the Raspberry Pi?

As I said, the Raspberry Pi is featured quite prominently in a huge number of tech DIY projects all over the web. What’s more is that if you’re friends with engineers or people who love technology, you probably have a friend or two that have already worked with a Raspberry Pi and carried out a project.

So what, precisely, is the Raspberry Pi? Well, at its most basic, it’s just a bunch of parts.

The Raspberry Pi was developed in 2012 by the Raspberry Pi foundation. The original intent of the project was to develop a super small and cost-effective computer that could be used to teach basic concepts regarding programming and computer science to both schoolchildren and children in developing countries, situations where available funds otherwise are quite sparse.

One of the intents behind the Raspberry Pi is that it’s supposed to be extensible. This means that it’s supposed to be very open-ended; you should be able to buy a number of modifications and hardware options for it and use them rather easily. We’ll talk more about this in the next chapter.

The Raspberry Pi was successful far beyond its original intent. While it was meant, as I said, to solely help money-tight situations - like public schools in developing countries - be allowed to fester a knowledge of programming and computer science, it quickly became a favorite toy of tech hobbyists everywhere because it allows you to do so much with so little.

Indeed, packed in a very cost effective microboard is a fair amount of computing power. However, we’ll get to that in the next chapter, as well.

So what exactly is a Raspberry Pi? Well, it’s a gateway to possibility. When you get a Raspberry Pi, you’re actually getting a million different things that you can do with it, too. You can set up a rig to water the plants automatically. You could teach your child how to program while they play Minecraft. You could do things like retrieve automatic updates on the weather and make an alarm clock that dictates them to you in the morning. In short, the Raspberry Pi enables you to do a lot of things for very little cost. All it takes on your end is the initial money for the Raspberry Pi, the money that you have to expend for the project materials, and the ingenuity and know-how to make it happen.

So with all of that said, I think you’ve got a fair idea of what the Raspberry Pi is conceptually, but I’ll recap once more before I bring this chapter to the close: the Raspberry Pi is a microcomputer with a ton of processing power for its small size. Many models of the Raspberry Pi are little bigger than a credit card! With its processing power, you are enabled to do a lot of things that you may have only dreamed of before. The Raspberry Pi will allow you to take on a huge number of DIY projects that will spruce up your life, bring you joy, and teach you things along the way.

Chapter 2

![](images/00002.jpg)

Under the Hood

So now that we know what a Raspberry Pi is, we need to know what’s powering it. At its base, the Raspberry Pi is just a microcomputer; a collection of computer parts soldered together in a tiny, practical package.

However, despite its small size, the Raspberry Pi is generally rather powerful. Moreover, several versions are out on the market right now that you can get your hands on. In this chapter, we’re going to be discussing the hardware specifications of each Raspberry Pi model and what they mean for you. Additionally, later on in the chapter, we’re going to be talking about the software which can power Raspberry Pi.

Firstly, there are currently six different models of the Raspberry Pi available on the market. I’ll shortly go into the hardware specifications on each one, going from least to most recently released.

The first model is based off of the original version of the Raspberry Pi, with a few modifications. It’s called the Raspberry Pi 1 Model A+ and is the lowest cost version of the “full” Raspberry Pi. It has a single USB port and is very small. It also is rather low on power. Therefore, if you’re undertaking a project that doesn’t take much power and doesn’t need many USB dongles, you’ll be fine. On models before the Raspberry Pi 3, one USB port will generally be taken up by a bluetooth or wi-fi dongle, so bear that in mind as we go forward.

A slightly better version of the same series - Raspberry Pi 1 - is available, and is called the Model B+. It features 4 USB ports and is, thus, more extensible. It shares many of the same perks as the Raspberry Pi 1 in terms of efficiency in both cost and power, but is slightly more expensive. (Though you also get a bit more power in return for the extra cash)

After the first version came, naturally, the second version. Much like the first, you can very easily get ahold of the second version of the Raspberry Pi, aptly named the Raspberry Pi 2\. The only version of the Raspberry Pi 2 currently available is the Model B. The Raspberry Pi 2 Model B is just slightly more expensive than either Raspberry 1 model. However, in return for the slightly bigger chunk of change, you get a super solid ARM processor and a whole gigabyte of RAM. For the record, the ARM processor is a big deal; the fact that the Raspberry Pi 2 has an ARM processor means that you could feasibly put any sort of ARM operating system on the device. This includes, for example, Windows 10 ARM or the ARM version of Ubuntu. This means, naturally, that your device is capable of far more than it would be otherwise, since you have a larger array of operating systems to use.

The next version of the Raspberry Pi that we need to discuss is the Raspberry Pi 3\. This is the latest version of the Raspberry Pi to be released, and it adds many things to the second iteration. Among these are built-in bluetooth and wifi, so that you no longer have to get separate dongles for those and your 4 USB ports can be exclusively used for anything you wish rather than wasting one or two on little wireless dongles. The CPU has also been upgraded a fair amount. Aside from that, the specs are largely the same as the Raspberry Pi 2\. However, depending upon the complexity and specificities of your project, you may wish to opt for a Raspberry Pi 3 - and after all, its CPU is better, which means your project will run faster and more efficiently, and who doesn’t want that? There’s only one version of the Raspberry Pi 3 on the market right now - the Model B.

Lastly, it’s important that we talk about the Raspberry Pi Zero. So, what is the Raspberry Pi Zero? Well, it’s the most cost-efficient form of the Raspberry Pi that you can get. It’s rather small, and each board is only $5 a pop. That’s not bad at all, and makes a huge number of projects super approachable from a standpoint of price. The Raspberry Pi Zero shares specs with the Raspberry Pi Model A+ in a lot of ways, but is far smaller. Additionally, the Raspberry Pi Zero doesn’t have a standard USB port. Additionally, you can get the Raspberry Pi Zero W, which is largely the same as the Raspberry Pi Zero but adds built-in wifi and bluetooth connectivity. Depending upon the nature of your project, you may wish to opt for this one so that you can easily use these features without getting convoluted and bizarre dongles for these purposes. The Raspberry Pi Zero and Raspberry Pi Zero W are great when you want to prototype, because they’re extremely cheap, and also are great for projects with a rather small form factor.

So, how do you know which version of the Pi you should get? It really depends on a number of factors. For example, if you’re new to Pi, you may wish to opt for a cheaper version, like the Model A+, the Model B+, or the Raspberry Pi Zero, that way if you don’t know what you’re doing or don’t end up liking the hobbyist nature of the Raspberry Pi, you aren’t out that much money. If you’re wanting a project that will last longer and be more competitive hardware wise, you should definitely opt for the newest version of the Raspberry Pi available. Ultimately, it’s a question of budgeting. Additionally, if you find a project that you’d like to partake in, you’ll likely want to use the same exact version of the Pi that the person who created the project used, just for the simple fact that there shouldn’t be any “mistranslations” if you do so, and there shouldn’t be any hangups on code or script.

When you decide that it’s time to go all in and buy a Pi, it’s really simple. First, you go to [http://raspberrypi.org](http://www.raspberrypi.org). On the top navigational bar, right below the search icon, there’s a “tag”that says “Shop”. Click it, and you’ll be taken to the Raspberry Pi online store. Click the version of the Pi that you’d like (you can also use this opportunity to compare specs more directly, if you so desire) and then scroll down on its respective page. A little bit of the way down the page, you’ll see where it says “Buy from our distributors” and then sections divvied up by one’s country or region. Some of the links don’t carry over, but if you get a broken link from the Raspberry Pi website, just try another one until you land where you want to be.

Eventually, you’ll find yourself on a storefront with the version of the Pi that you’d like to use. You can take this opportunity to look around at all of the gadgets that are available for the Pi, if you’d like to do so. Let me give you a heads up, though; there are a lot of them. Poke around a bit and see if there is any potential fodder for project ideas that you may have. The Raspberry Pi is one of the best supported microboards out there, so I’m sure that you will be able to come up with something. Anyhow, once you’ve cemented yourself into buying a certain Raspberry Pi, then just relax. All you have to do now is wait for your new toy to come in the mail for you to start playing with it, and that won’t be too long of a wait… right?

Now that we’ve talked about the hardware and where to buy a Pi, I feel like it’s apt that we talk about the software that you can get powering the Pi.

The Pis that are model 2 and 3 can theoretically run any ARM-based operating system that will run on their architecture. This leaves a lot of options open in terms of what operating systems one can use.

Generally, most people opt to use the Raspberry Pi team sponsored operating system “Raspbian”, which is a derivative distribution of the popular Linux-based operating system Debian. Raspbian comes loaded with a ton of tools that are designed to help someone have a working operating system with next to no money down on it, as well as a bunch of tools that are intended to teach people - mainly kids - programming in fun ways. Among these are things like Minecraft Pi, which lets people play Minecraft and also use Python code in order to improve their experience with the game. Additionally included is the MIT-created Scratch, where puzzle piece commands are used to illustrate program flow and computer logic.

However, beyond all of the little knick-knacks that come with Raspbian, in the end, it’s just a very solid operating system based on a solid operating system.

There are a lot of options available, though, if you’re thus inclined. For you to truly get the Raspberry Pi experience, you should opt for Raspbian, but once you have more experience and want to start experimenting, there are things such as the ARM version of Windows 10, Arch Linux, Gentoo, Ubuntu MATE, Kali Linux, and FreeBSD. All of these have their own particular uses, depending upon what you’re wanting to do and what your goal is with a particular Raspberry Pi. But, for right now, the Raspbian operating system is actually optimized for the Raspberry Pi and has a huge number of packages just for it, so I highly recommend you work with it.

Chapter 3

![](images/00002.jpg)

Setting Up

At this point, I’m assuming that you’ve gotten your hands on your Pi. If you haven’t, you can still proceed to Chapter 4 and practice your programming chops and then just refer back to this when your Pi is in.

If your Pi is in, then perfect! You’re absolutely ready for this chapter.

This chapter is going to focus on how to get your Pi up and running. I’m focusing specifically on the Raspberry Pi 3\. However, the instructions should be relatively similar regardless of which version of the Pi that you’re using. Adapt and do your research prior.

So, here are the things that you’re going to need for this chapter:

> > > > •Raspberry Pi: This one goes without saying. You’re going to, of course, need a Raspberry Pi in order to set up a Raspberry Pi.

> > > > •Screen of some form with an HDMI input: It can be a TV or a monitor, it doesn’t particularly matter too much. What matters, ultimately, is that regardless of which one it is, it has an HDMI input. The Pi exclusively has a HDMI output, so whatever screen you’re using, it has to accept HDMI. No questions.

> > > > •USB peripherals: You’re going to need to control the Pi somehow. A USB-connected keyboard and mouse are more than optimal for what you’re needing here.

> > > > •MicroSD card: You’re going to need at least an eight gigabyte MicroSD card for your Pi. Everything is read off of an SD card on the Pi. Where on most computers, you have an external hard drive connected, like a SATA drive, the Pi runs off of the SD card. You can actually set your Pi up to read off of a USB drive or an external hard drive, but the SD card is the most direct and easy method.

> > > > •Power: The Raspberry Pi’s power source is a microUSB. This sort of connection is the same as that which powers most Android smartphones. The cord has to be good enough to supply two and a half amps of voltage, because otherwise, you’re underpowering your Pi and may fry it - it’s far easier than you would think! Play it safe and be sure that you’re using the right voltage. If you’re unsure, refer to the communities in Chapter 6 and ask around to be sure.

> > > > •NOOBS: Installling the suggested Raspberry Pi Linux distribution, Raspbian, used to be rather difficult. Recently, in relative terms at least, the Raspberry Pi team have released a utility called NOOBS (“New Out of Box Software”) that makes it dramatically easier than it was. No longer do you need to tamper with the Terminal just to get a copy of Raspbian onto your SD card; just get a copy of NOOBS and you’re good to go. You can get NOOBS at [https://www.raspberrypi.org/downloads/noobs/](https://www.raspberrypi.org/downloads/noobs/) — get the version which has an offline installation, as this one will come with the operating system alongside it.

So here’s what you do. The first thing you need to do is plug your microSD card into your computer. How you have to do this will depend upon your computer’s set-up for SD cards; it’s possible that you may need to go and buy a reader for it, or a microSD to SD adapter. Some computers - mine, for instance - support SD cards but not microSD cards, which is one example of when you would need the adapter.

Once you’ve gotten your card hooked up to your computer, you need to format the card to FAT. This is simple enough to do.

FAT format, Windows:

All you do is plug the SD card in. Then, go to Windows Explorer. Windows oldies will remember this as “My Computer”. From here, find the SD storage device in the left pane of your screen. Right click it, and then click “Format…”. Make certain that you don’t have any sensitive data on there that you need to make a backup of. If you do, copy the files to your computer right quick before you format. Afterward, carry out the formatting. You simply need to format as (MS-DOS) FAT, naming the drive whatever you’d like.

FAT format, Mac:

Open the Disk Utility and make absolutely certain that you’ve selected the right volume. If you accidentally choose the wrong volume, you could lose some very important information and format the wrong drive altogether! This is very much not desirable. Once you’ve made certain that you’ve selected the correct drive and there’s no important information on the SD card, you just click “Erase...” with the formatting type being “MS-DOS”.

FAT format, Linux:

Get gparted if you don’t already have it (you’re a Linux user - of course you do!). In gparted, select the appropriate drive, once again making sure that you’ve selected the absolutely correct drive, and then format to fat32\. Simple.

Now, once all of that is taken care of, you should have a formatted SD card that’s ready for the NOOBS files. All that you do is take the NOOBS zip file that you just downloaded, extract it to a folder, and copy all of it to your SD card. Once every file has been copied over (it may take a minute or so, depending upon the speed of your computer), you can then call this part of the installation process good.

The next thing that you have to do is plug the microSD card into your Raspberry Pi. After that, you need to start attaching all necessary cables to your Raspberry Pi. Plug in the power last, because the Raspberry Pi will turn on automatically when the power is plugged in. Plug in all other devices first, such as your monitors, keyboard, mouse, any wireless dongles, and your wired internet connection if applicable.

If everything went well, then as soon as you boot up your Raspberry Pi, you should be taken to the NOOBS installation. It should, for the most part, set itself up. The entire process is incredibly easy; after all, the Raspberry Pi itself was made so that people with pretty much no computer or tech experience at all can easily pick it up and start hacking away. The only precaution here is to make sure that you select to install Raspbian, because Raspbian is what we’ll be working with in this book, and what most Raspberry Pi projects use, actually. Technically, the Raspberry Pi can run any ARM operating system, but Raspbian is the best for people who are new to Raspberry Pi.

Spectacularly, once the set-up is done handling itself, it’ll end up restarting. At this point, you’re done with the initial set-up. Everything from here is just setting up wireless networks and bluetooth devices, if necessary.

With that, you’re essentially done with setting up your Raspberry Pi. What once seemed rather daunting has turned out to be quite easy in reality! Don’t worry - the fun is only just beginning, and there is plenty of frustration ahead! But, to match all of the frustration, sighs, and head scratching, you’ll get to experience the liberating and truly one of a kind feeling of having something work. Engineering of all forms is 90% disappointment and 10% payoff. However, the payoff is one of the best feelings that you’ll ever have.

When you’re jumping in from nothing, there is going to be quite a bit that you don’t really understand. In order to mitigate that feeling of hopeless ignorance and to help you understand some of the code snippets and scripts that you will encounter as you go forward and start working with a ton of different projects, it’s imperative that I now help you to understand how to write basic Python and what all of the underlying concepts behind programming are.

Chapter 4

![](images/00002.jpg)

Programming Essentials

At last, we’ve landed at the point for which you bought this book in the first place. In this chapter, we’re going to talk about a lot of the fundamentals and ideas behind programming that you’re going to need in order to take full advantage of the Raspberry Pi and the hardware behind it.

There’s good news and bad news; I’ll start with the bad news. The bad news is that giving extremely specific information is rather difficult, because every project is going to have its own niches, libraries, and requirements. I can’t just tell you how to write a script for one project and then have it magically apply to every single project out there. But what I can teach you is the underlying concepts that frame almost every single Raspberry Pi script, and that likewise are extremely important if you wish to be an adept programmer and hobbyist with the Raspberry Pi.

That’s where the good news comes in: you can start right now. You don’t have to wait for your Pi to come in. In fact, I wouldn’t, if I were you. Programming on your Raspberry Pi is going to inevitably be a pain and, if you have a computer, you’re actually more apt to practice your skills on there so that you can deal with a more “standard” keyboard/mouse/monitor setup than you might have on your Pi. This, of course, is subjective and relative to your experience, however.

The reason that you can do this is because almost every single Raspberry Pi script runs on Python. So what is Python? Python is a super useful programming language that was born pretty much from the phoenix ashes of languages like C++ and Java. If you don’t know what those are, they are programming languages themselves that are a fair bit more complex than Python. (I’m going somewhere with this, I promise!)

See, programming has always had one specific purpose: problem solving. Every programming language is thus tailored to solve different sorts of problems. Early on in computer history, languages were extremely esoteric. This was partly because every bit of storage and memory usage counted, and it was necessary that one had complete control over memory allocation and program size. This is where languages such as C came in. However, at the same time, there had to be a programming language that was friendly to mathematicians, who benefited greatly from making programs but weren’t adept with computers; this is where Fortran came in. Other languages, too, had their niches; Lisp was designed for stack programming. When computing power became a bit stronger, object-oriented programming came to the forefront as a dominant means of organizing projects, with the champion of object-oriented programming being Java. Shortly before Java, the ideals of C-style memory maintenance and the advent of object-oriented programming were combined into a super influential language known as C++. The list goes on and on.

Python is a scripting language, and scripting languages have a niche themselves. Scripting languages are written with two purposes in mind.

The first is that the scripts can ideally be written on one computer and then interpreted anywhere. This means that if I write a script on my Windows laptop and I send it to my friend with an iMac, they can still run the script with absolutely zero problem. This isn’t always the case, and there are some rather esoteric scripting languages, but for the most part, they run within their own special environments.

The second is that the scripts have fast deployment times. This means that the code in them can be written quicker than it could in another language. Compare this code snippet in Java:

> > > public class myFile {

> > > > > public static void main(String args[]) {

> > > > > > System.out.println(“Hello world!”);

> > > > > }

> > > }

> > > with this code snippet in Python:

> > > print “Hello world!”

The Python snippet is so much shorter. This is the intent. Scripting languages have their drawbacks - none of which, frankly, you’ll understand at this point in your learning. But for the most part, they’re extremely efficient in terms of time spent writing code, and they also have a pretty simple learning curve compared to a language like C.

So what’s the point of me saying all of this? Well, you can practice your Python programming on any computer and then transfer it to the Raspberry Pi with no issue. All you need is a copy of Python and a text editor.

The point of this chapter is to acquaint you with all the various eccentricities of programming that I think may throw you off. These lessons may not seem valuable when you look at scripts written by people who have already made projects, but when you look at those scripts closely, you’ll see that the underlying concepts - data types, arithmetic, methods, and so forth - are very prevalent. You can’t expect to do anything with a script if you don’t know what these concepts are.

Setting up Python

So let’s start from the beginning. The first thing that you need to do to start programming in Python is to, well, get Python. Many computers already have it. If you’re running Linux or Mac, then the chances are good that you do. You can test to see if you have it by opening either Terminal (in Mac or Linux) or PowerShell (in Windows) and typing python, then pressing enter. If you have Python installed, it should execute a program. If not, it should throw you an error message.

If it executes a program, look at the program text to see what it says. If it says “Python 3.x”, you need to uninstall it and get Python 2 instead. The reason for this is simple: most Python scripts are written in Python 2, because it has been the longstanding version. We are learning Python 2 in this chapter. A lot of things transfer between Python 2 and Python 3 and moving over to Python 3, if you need to, will be extremely easy. But for the most part, if a utility is written for Python 3, it will also be written for Python 2; however, more often than not, the reverse isn’t true. For this reason, it’s easiest to just teach and work with Python 2 at this point in time.

If you don’t have Python installed, or you just uninstalled Python 3 and are looking to get Python 2, you need to go to [http://python.org](http://www.python.org). This is the official Python website and is where you’ll be able to find a copy of Python for virtually any given operating system.

After this, you’ll need to get a text editor that you’d like to use. Within Raspberry Pi, you’ll be largely using the console text editor (Nano), but on your practice computer, you can use whatever you like. It really just needs to be something that you understand and are either comfortable using or are content to learn to use. Personally, I love the text editor Atom, which you can get at [http://atom.io](http://www.atom.io) for Windows, Mac, and Linux alike. There are a lot of reasons to love Atom, but the biggest are that it’s free and there are a ton of plug-ins intended to make your life easier.

Once you have your specific text editor, spend a bit getting to know it. Try making a new file, saving it, creating a project path (if applicable), and so forth. Essentially, learn the functions that you’re going to want to use. At this point, you should have your Raspberry Pi set up, too - you would benefit from going to the console, starting up Nano, and learning how to create, save, open, and edit files with it. It’s relatively straightforward and fun to use, believe it or not.

Anyway, back on your practice computer, we’re going to get to the basics of Python that will enable you to work with other people’s scripts and, eventually, write your own. Before we do that, though, there’s one last thing we need to do.

Start up Python via either Terminal or PowerShell. If everything so far has gone according to plan, you should see something that says:

> > > >>> Python 2.7.12

and then some more text afterward. If you don’t see this and you’re running Windows, ensure that you have a PATH variable set up for Python.

Once Python is running, type the following:

> > > print “hello world”

The console should print out hello world back to you. If it does, then congrats! You just wrote your first line of Python code; I hope you feel accomplished! Once you’ve written that line of code, go ahead and type exit(). This will terminate the Python interpreter in the console.

I encourage you throughout the rest of the lesson to make your own files and experiment with these concepts.

Working with variables and data

So, we’re trying to cover a fair amount of ground in a relatively short amount of space. This means that some of these explanations may seem a bit sparse, but I’m not trying to make them so - I’m just trying to not drag on about the little things and to cover the bigger things so I don’t waste your time.

In programs, there are things called data types. These data types all represent different forms of different information. Computers, they read everything as bits and bytes; 1s and 0s. We humans aren’t so fortunate as to think in such as a black and white binary sort of way so we really have to separate things and parse them up. Well, this means that different types of data are interpreted differently, both by us and by computers.

For example, if I gave you the word “oyster” and the number 472, you would say they were unrelated. Yes? That’s because they are. One is a number and the other is a word. Data types are similar. If I were to give you two words or two numbers, and you knew what I was getting at, you’d see quite plainly the bridge that I was drawing between the two.

So let’s say you have a value and you want to store it. How do you do so? The answer is simple: variables. Variables are much like they were in algebra. X can be anything that we want it to be, so long as it meets the requirements of the equations, yes? X can take on any value. Variables are similar. We can set the “equation” which defines the value of the variable.

Back in the olden days of programming, you had to define the “type” of the variable. If you had a number, you had to say that “the number x is an integer”, or if you had to store somebody’s name, you had to say that “the word name is a string.” Well, scripting languages are both a blessing and a curse because this sort of thing simply isn’t necessary anymore. Scripting languages have mitigated that sort of type definition. This is called implicit typing.

Let’s say we wanted to store somebody’s name, and the name was Jerry. We’d just create a new value, like so:

> > > name = “Jerry”

And let’s say we wanted to store our friend Jerry’s age - he’s 42.

> > > age = 42

Well, thanks to the fact that we stored this pertinent information in variables, we can recall it later. If we typed:

> > > print “My friend %s is %d years old.” % (name, age)

It’d print whatever value was stored in name and age. So in this instance, it would print “My friend Jerry is 42 years old.” Super easy stuff.

In Python, there are a few types -

| float | decimal numbers | 3.14 |
| integer | whole numbers | 7 |
| string | character sequences | “Skate park” |
| boolean | true/false | True |

There are more, but these are the biggest ones.

Python Math

Guess what computers do? They compute. And they’re very, very, very good at it. It’s no wonder, then, that programming languages are literally made to do math. There’s not much to show here, I’ll be brief:

| numberOfCats = 4 + 3 | # numberOfCats would be 7 |
| numberOfDogs = 8 / 2 | # numberOfDogs would be 4 |
| numberOfHamsters = 3^2 | # numberOfHamsters would be 9 |

For the record, the thing with the hash mark is a comment. These are ignored by the code. When you enter a hash (#), you are telling the compiler - the thing which reads and runs your code - to ignore anything that comes after the hash mark on that line. Simple concept, sure, but worth covering.

To be, or not to be? Booleans and Comparators

This will make a lot more sense here in a moment when we deal with if/else statements, but for right now, just focus on the idea of True or False. Something can be, or it can not be.

If I were to say “3 is less than 7”, it would be true. If I were to say “7 is less than 6”, it would be false. We’re allowed to make these kind of evaluations within Python. In fact, it’s encouraged.

> > > number1 = 4
> > > number2 = 5

> > > print number1 < number2

This would print out “True”, because it’s true - 5 is greater than 4\. That should go without saying, right? Python sees that you made a comparison, and it looks to determine whether the comparison is accurate or not. If it is, it feeds back True. If it isn’t, it feeds back False.

You can store these evaluations to a variable.

> > > number1 = 4
> > > number2 = 5
> > > eval = number1 < number2

> > > print eval

This would print out “True”, because Python evaluated whether “number1 < number2” was true or not, then saved that evaluation to the variable eval. Just like shy kids in high school, there are a lot of ways for things to compare themselves in Python. Here are the basic ones:

| < | Less than |
| > | Greater than |
| <= | Less than or equal to |
| >= | Greater than or equal to |
| != | Not equal to |
| == | Equal to |

While we’re on the topic, be super wary of the difference between == and =. The latter is an assignment operator - it’s used to give variables to something. The former is a comparison operator - it’s used to compare two values.

If and else

We’re moving rather quickly through all of this, I know.

There comes a time in every program’s life where they have to make big decisions, it’s just a part of growing up. You can facilitate this sort of decision making by taking advantage of the conditional statements. Let’s start with one.

> > > bananas = 3

> > > if bananas == 3:

> > > > > print “I have three bananas!”

What this program does is assign the number 3 to bananas. It then runs a check to see if bananas is equal to 3\. If it is, it prints “I have three bananas.” Great. If it’s not, it prints… nothing at all. Well, that’s a toughy. Alright. How do we fix this? We can use else statements as a catch-all in case the if condition isn’t met.

> > > if bananas == 3:

> > > > > print “I have three bananas!”

else:

print “Huh, well, I don’t seem to have three bananas.”

In this case, if bananas is 3, then the program will print that it has 3 bananas. If not, it will be puzzled and express this quite clearly. But what if it has zero bananas and is sad and wants to express that? We’ve already checked to see if there are three, we can’t check to see if there are 0, too. Right?

Wrong. This is where if else statements come into play.

Let’s just sandwich an if else statement for zero bananas in there. Observe:

> > > if bananas == 3:

> > > > > print “I have three bananas!”

> > > elif bananas == 0:

> > > > > print “I have no bananas, and this is a problem.”

> > > else:

> > > > > > print “Huh, well, I don’t seem to have three bananas.”

In this case, it checks to see if bananas is 3\. If not, it goes to the next condition and checks it. If bananas isn’t 0, then it finally moves on to the else statement. The if/else block will check every condition before resolving itself to the else statement.

Lists

Sometimes you need to store connected values together. This is super easy in Python. Let’s say you needed to store a student’s grades.

> > > student1Grades = [95, 94, 83, 87, 79, 91]

Perfect. You now have a list of 6 grades. You can access any of these. Remember, though, that computers start counting from 0, not from 1. So if you wanted to print the first item in the list, you’d use:

|  
> > > > print student1Grades[0]

 | # would print 95 |

You can add items to a list super easily.

> > > student1Grades.append(86)

And you can delete them just by using the del keyword and giving their index position.

del student1Grades[3] # would delete the value at index “3”, so the fourth list element - 87

This would delete 87 and push everything in front of 87 back by one index position.

Loops? Loops.

Loops are another way of handling the flow of a program. There are two sorts of loops in Python: for loops and while loops. We’ll start with while loops, because they’re easier.

While loops will repeat themselves for as long as a condition is met:

> > > x = 1

> > > while x < 10:

> > > > > print x

> > > > > x += 1 #adds 1 to x - is same as “x = x + 1”

This loop would print 1 through 10.

For loops serve a bit of a different purpose, especially in Python; for loops are meant specifically to iterate through a list. Let’s take the student1Grades example before. If we wanted to print out every grade in that list, we’d do like so:

> > > student1Grades = [95, 94, 83, 87, 79, 91]

> > > for i in student1Grades:

> > > > > print i         # would print 95, then 94, then 83, etc…

However, you can also do the same type of iteration that you can do with while loops with for loops; it’s not exclusively for list iteration. To count from 1 to 10, you’d do the following:

> > > for num in range(1,10):

> > > > > print num

Note that you can name the iterator variable in a for loop anything. Notice how this time, it was num, while last time, it was i. Crucial little details that will save you confusion later.

Methods

This is the last absolutely critical thing to cover in this chapter. Methods are the foundation of every good program. They let you break up your code in a very modular way and separate the program into logical sequences. They also keep you from having to copy and paste code over and over, making your code far prettier than it would be otherwise.

The basic setup of a method is like so:

> > > def methodname(arguments, if any):

> > > > > # code here

Arguments are things that you can pass into the method as values to be worked with.

Let’s take a method that computes the area of a square, for example:

> > > def computeArea(length, width):

> > > > > print length * width

What this would do is allow somebody to “call” the method, like so:

> > > computeArea(3, 4)

and then take the arguments given and do something with them. Arguments are not necessary, but they are helpful in many cases. Not every function will take arguments; some methods will simply serve a standalone purpose.

The method prior would have printed length * width, or, as we just called it, 3 * 4. So it would have printed 12.

What if we didn’t want it to just print something, though? Once we print the value, it’s gone, it’s not being stored. How can we keep the value? That’s where returning comes into play.

> > > def computeArea(length, width):

> > > > > return length * width

This won’t print the value of length * width; rather, it will give it back. Since it’s giving the value back, that means we can store it. So let’s say we had the following code:

> > > def computeArea(length, width):

> > > > > return length * width

> > > l = 3
> > > w = 6
> > > area = computeArea(l, w)

The variable area would take the value of 3 * 6, or 18, because we passed the variables l and w to the method, and it returned us the value of those arguments multiplied by one another.

Methods are immensely useful in keeping your code clean and automating processes that you would otherwise have to be extremely messy about. For this reason, it’s a good idea to practice them and build up as much skill as you can with them.

Closing

We managed to hit a lot of the big fundamentals of programming. You aren’t ready to write a massive 15,000 line program - nobody would be after a simple crash course. However, you know what you’re looking at now. It’s through time and exposure that you’ll be able to build up the necessary skills to be an expert programmer. The point of this chapter was to teach you the essentials of programming as they pertain to a Raspberry Pi and the projects that you’ll be doing. It’s going to be incredibly frustrating trying to get up to speed when a lot of the projects that you’ll be working with have been developed by people who seem light years ahead of you in terms of both software development and hardware know-how. The key thing that you’ve got to remember is that everybody had to start from nothing - nobody starts out knowing something. Eventually, you’ll get to a point where you feel comfortable with any project. Perhaps, if you stick with it, you’ll even get to a point where you feel like you’re light years ahead of others. Anyhow, speaking of other people’s projects, I’m going to now move on to how you can find project ideas that you’ll absolutely love.

Chapter 5

![](images/00002.jpg)

Project Ideas

I’m sure that at this point, you’re anxious to actually start working with some neat Raspberry Pi projects. Well, let me tell you that I’m more than excited to get you started on that path.

The first thing that we’re going to focus on in this chapter is learning where you can actually go to find all sorts of cool projects you might not have thought about before. Afterward, we’re going to talk about a super cool project that you can do super easily at home - the magic mirror! I mentioned it at the beginning, but it truly is an incredibly fun and wow-worthy project that will make your mornings brighter and leave visitors speechless.

So first thing’s first: where can you actually go to find projects?

Well, there are a lot of resources that you’ve got access to as somebody who is interested in Raspberry Pi projects. Really, if you’re just looking for inspiration, it’s as simple as Googling “cool raspberry pi projects” - you’ll get a ton of hits on really awesome projects! There’ll surely be something that can spark some sort of interest for you.

However, the three best ones that I’ve found in terms of actual tutorials are, in no particular order, Instructables, Hackster, and Hackaday. All of them have their own strengths and weaknesses.

Let’s take these one at a time.

Instructables is an excellent resource. The link that I’m referring to in particular is audreyobscure’s “Raspberry Pi projects” page at [http://www.instructables.com/id/Raspberry-Pi-Projects/](http://www.instructables.com/id/Raspberry-Pi-Projects/). A lot of these have very in-depth tutorials. The only problem is that some of them are rather deprecated and/or esoteric.

Hackster is by far my favorite. This is primarily because it’s very active. There are constantly people posting new projects, ideas, and concepts. Generally, these will have tutorials. Unlike Instructables, though, many of the projects are just for “show and tell” purposes, or a manner of documenting what the person did without documenting how they did it. Regardless, it’s still an excellent resource for inspiration, and there’s actually quite a bit that you can learn from it as well. The relevant link can be found by going to [http://hackster.io](http://hackster.io) and typing “Raspberry Pi” in the search bar, or simply going to [https://www.hackster.io/raspberry-pi](https://www.hackster.io/raspberry-pi).

Hackaday is the last one that I mentioned. This community is a little tighter than the one on Hackster. The posts are thus a little bit more tightly regulated, too. Because the posts are automatically sorted by number of likes rather than age or time last updated (you can sort them by those, don’t worry), it’s easy to get duped into looking at a super cool project and then have the files be deprecated, so be wary of how up to date a project actually is, what version of the Raspberry Pi it uses, and so forth. This site is actually worse about “show and tell” type projects, miraculously, but that’s alright - people make beautiful and amazing things and they want to show them off! No problem. It’s an excellent source for tutorials and inspiration alike. To access the Hackaday Raspberry Pi projects, simply follow this link. [https://hackaday.io/projects/tag/raspberry%20pi](https://hackaday.io/projects/tag/raspberry%20pi)

Those are my three favorite resources for inspiration and project ideas. I’ve made quite a few things with Raspberry Pis at this point, largely driven by the ideas that I’ve gotten from these sites. It’s not all looking at other people’s stuff, though; remember that the best things you’ll ever make are the things you’re passionate about. Find a way to loop your own passions into your next project.

Chapter 6

![](images/00002.jpg)

Your First Project - A Portable Superconsole

This is a relatively ambitious first project, but if you stick it out and follow the instructions carefully, then you’ll find yourself with a really seriously cool end product. This is an especially great project for video game enthusiasts.

I’ve pointed out several times in this book how the Raspberry Pi has been used by people to build things like custom arcade cabinets and portable handheld consoles. Well, now you’re going to follow in those footsteps by making your own portable handheld console.

So, you may be wondering what makes this different from every other project like this one? Well, the biggest factor which sets this one in particular apart is the fact that it is far more covert. What you get with this project is essentially a self-contained emulation station. What’s more is that if you have a child who likes gaming, they very well may enjoy taking this project on with you.

What’s even cooler is that the console may seem self-contained, but you can use any USB controller you like and play games from literally all throughout the history of gaming. The only point at which the Raspberry Pi has issues is the PS2 and GameCube era - up until then is fair game.

The optimal target console for this project is one which is broken and is sitting around. Bigger is better, and the more smooth/balance of a design, the better. For example, on the original project, I used an NES that had been sitting around forever. I’m sure that, if you’re an avid enough gamer to take this on, you’ll have an apt console sitting somewhere. The NES is the perfect console for it. However, if there isn’t an NES, anything that can be unscrewed and opened and shut easily is great.

If you don’t have an old and broken console sitting around, you can go on eBay and find gutted/broken consoles for extremely cheap.

In taking on this project, these are the things you’ll need:

> > > > •A broken console

> > > > •Hinges (to open and close the console “lid’)

> > > > •Permanent marker

> > > > •Drill with bits that are made to drill through plastic

> > > > •Raspberry Pi 3

> > > > •Screen, for this I recommend that you grab a smaller display. This 5”one should be apt: [https://www.amazon.com/Resistive-interface-compatible-Raspberry-Pi/dp/B00U21UA16](https://www.amazon.com/Resistive-interface-compatible-Raspberry-Pi/dp/B00U21UA16). The key objective is that it’s able to fit in the top half of the system after gutting and sanding - speaking of which..

> > > > •Numerous grits of either sandpaper or a sanding block

> > > > •USB controller - you can use an Xbox 360 controller or even get a USB NES/SNES controller on Amazon. Be sure to check the reviews on whatever you get, as some of the controllers on Amazon are absolutely terrible. It’s worth a few dollars more for quality - trust me.

> > > > •Headphones or speakers that will fit in ordinary 3.5 mm headphone jacks. If you’re using speakers, then a flat design is far preferable because it can balance out the heaviness from the screen.

> > > > •Very weighty linen, like old curtains

> > > > •Screwdriver

Alright, now that we’ve got all the necessary materials out of the way, let’s get cracking with this. The system that I’m going to use as an example is an NES, because it’s what I know and it’s what I’ve done the project on before. However, if you aren’t using an NES, the basic concepts are rather similar.

Anyway, back to the NES. You need to open it up. This is extremely easy. There is a set of screws fastening the bottom half of the NES to the top half. All that you do is unscrew those. Then, your NES should be open.

Now you need to take all of the NES components out. By this, I mean the motherboard and all of the wires. You can leave in the buttons and the controller ports, though, if you’d like - they add a nice sort of aesthetic to the whole thing and are rather nice to look at. Other than what you decide to leave in, you’re gutting it entirely. Gut more, not less - you need space to work with when it comes to the important components.

I’ve already told you how to install Raspbian, so I’d rather not do so all over again. It’d, frankly, be a waste of both your time and mine. Instead, I’m just going to assume that you can do all of the Raspbian setup yourself. The important part is this guide is actually RetroPie. What RetroPie does is act as a shell to Raspbian. It makes it so that when you boot into Raspbian, you automatically load the emulator packages that are necessary and are basically shot into your game station instantly.

There’s a legal obligation, really, to denote that emulator usage is illegal unless you actually own the game that you are playing. It’s literally illegal to have ROMs of games of which you don’t have a tangible copy. The chances of anybody coming after you are incredibly, incredibly low, but they are there. This is me copping out and saying “don’t say I didn’t warn you” if you play illegal ROMs.

So, going on to RetroPie’s installation. First, you should have Raspbian set up, of course, and your Raspberry Pi should be connected to the display that I mentioned you needed earlier. Once Raspbian is set up and we’re connected to either a wired or wireless internet connection, you need to open Terminal.

In Terminal, we need to update our packages. If you’re not terribly Linux savvy then this is simple enough. All that you have to do is type this:

> > > sudo apt-get update

> > > and press Enter. Then you just type this:

> > > sudo apt-get upgrade

and press Enter again. After all of that is done, your package list will be completely updated and you’ll be ready to install RetroPie.

Well, almost. RetroPie has a set of dependencies that it has to have, first. You can grab these dependencies by going to Terminal and installing lsb-release from the git repository, like so:

> > > sudo apt-get install git lsb-release

When that’s finished, we just need to get the RetroPie installation scripts. This is pretty simple, too.

> > > Just type the following:

> > > cd

and press Enter. This will make you go to the root of your C drive. Next, what you do is grab the RetroPie script from the repository, like so:

> > > git clone —depth=1 [https://github.com/RetroPie/RetroPie-Setup.git](https://github.com/RetroPie/RetroPie-Setup.git)

Once you have the script download, you have to make it so that a person is able to execute the script. This is pretty easy, as well! First, you go to the RetroPie folder:

> > > cd RetroPie-Setup
> > > (caps are important! Pay attention to that!)

Then you change the permissions:

> > > chmod +x retropie_setup.sh

Then you give the folder admin permissions:

> > > sudo ./retropie_setup.sh

If any of this doesn’t work, try throwing the keyword “sudo” before it, which elevates you to root privileges.

Afterward, you need to double check that your system locale is correct. This is because the things which are needed for all of the RetroPie emulators to run take specific files which will vary depending upon the location of the user. In order to check this, all you have to do is run locale from the Terminal.

Make sure that everything is set. If something isn’t, then it needs to be. There’s a really simple way to do this. First, make sure you understand what your locale is. For example, yours could be en_US.UTF-6. Then place that locale in the following command in place of the italicized “userLocale”:

> > > sudo update-locale LC_ALL=“userLocale”

Including quotes, of course. From here, we just need to install RetroPie itself.

There are two different ways that you can install RetroPie. You can either do a full or a partial install. If you’re only wanting certain systems to be playable, then you should definitely do the partial install. However, if that is not the case, then the full install is much easier and much more full-featured.

Full Installation

All that you do here is execute the RetroPie-Setup script. When it starts to execute, you’ll eventually land on a screen where it says “manage packages”. From here, you’ll simply toggle “Quick Install” and then comfirm by pressing Enter. Definitely one of the easiest things in this whole book, no? When you do a full installation, it also creates the exact folders that you’ll need to store your ROMs in. If you’ve followed this book relatively to the letter, they’re going to be under ~/RetroPie/roms.

Partial Installation

This solution is much lighter on your SD card if you’re wary of how much storage you have (or want) to use. Using this option, you’re able to use your own discretion at which emulators you do and don’t want installed. Remember that there are a few packages that you have to have in order for RetroPie to even run:

> > > > •RetroArch, the UI for RetroPie

> > > > •Emulation Station, the backbone of the system which starts and sorts the ROMs that you’ve got tucked away in your little folders.

> > > > •RetroPie Menu, rather self-explanatory

> > > > •Runcommand, honestly not certain what this one does but it sounds important and it doesn’t work without it

So you need to install all of those packages. Once they’re install, you can seek through the list of packages that are available and determine which emulators you do (and don’t) want.

Next, all that we’ve got to do is make it so Emulation Station will run first thing when the Pi starts up. Toggling this setting is actually extremely easy. From within RetroPie, all that you do is go to Setup Script. From here, you’re going to head to the Configuration and Tools menu, wherein there will be an Autostart submenu. Numerous different boot conditions for the Pi are listed, but all you’re going to do is toggle the first, which reads “Start Emulation Station at boot”.

You can try restarting your Pi now, just to be certain that everything is in working order. Unplug and restart your Pi. If it boots into Emulation Station first thing, then you know you did everything right. If it doesn’t, then something went awry and you need to retrace your steps and figure out what went wrong.

If everything is working then we need to talk about how to put ROMs on your Raspberry Pi. The easiest way to put ROMs on your Pi, by far, is to simply use a USB drive. Thus, this is the method that I’m going to go over for you.

So, the first thing that you need to do is format your USB drive to FAT32\. We talked about how to do this earlier, but with SD cards. The process, however, is exactly the same. Simply follow those same steps that we did earlier to format the SD card, but relative to the USB drive.

Then, once it’s formatted, what you do is open the drive and then create a folder called “retropie”, exactly like that. Then take your USB drive out of your primary computer and insert it into your Pi. The drive will start blinking, this signifies that active file system changes are happening. This is what you want. When the blinking stops, you just take the drive out.

Put it back in your original PC. You’ll see a whole lot of new folders that weren’t there before. These are where you put your ROMs. You just drag the ROM to the correct system/emulator’s ROM folder, and then you’re good to go. You can add as many as your drive will hold. It may take a bit for the transfer to complete, but it’ll happen.

When the transfer has completed, put the USB drive back in the Pi. It’s going to start blinking again; wait it out. When it’s all done, all you need to do is refresh Emulation Station. You do so by pressing the F4 key. Hopefully, you’ll see all of the new games that you loaded onto the USB right there for you to play.

So now we’re in the final stretch of all of this business: taking our console and making this project truly ours. We’ve got our Raspberry Pi working, RetroPie is taking care of all of the heavy lifting for us. Now all that we’ve got to do is seal the deal on the project.

At this point, we’ve already gutted the console. If you followed my recommendations for finding an ideal console (cough cough the NES), then it should be pretty much perfect for a hinge layout. This is actually why I’m pushing for the NES on this project: its design is so stupidly easy. The NES is two parts, with everything important in the pit thereof. So it’s actually pretty much perfect for everything we’re wanting to do here, because if we set it up with hinges, it will open/close with no issue at all, and will actually look quite good doing it.

That brings us to our next part of this project: putting the hinges on the console. In your mind, visualize where you want the hinges to be and how you want the console to open up. Take your Sharpie and try to leave as accurate of marks as possible for what you’re wanting. Then take the drill and bore holes there, very slowly, using the plastic bits. Once the holes are in place, simply put the hinges on and then test them out.

Now, we just have to start carving our way out within the system for our electronics. Figure out how much room that you need for your screen. Is it big enough? What will you have to sand down to get it to fit? Figure out what dimensions you’re going after and then start sanding out a place for your display/Pi duo. Take it very slowly and very carefully, because plastic sands off very quickly and you may take far more than you’re intending.

Once all of that is done, look at the screw holes of the Raspberry pi and determine where in the lid of the console you need to bore holes for the display to fit and be fastened. The way that I would do this is with a simple nut/screw setup. Bore the holes, put the screws through the top and then fasten a bolt so that the Pi is secure. This is extremely noticeable, but most people won’t actually realize the screws are there at all unless you point the system out. The system, thus, maintains its cool and conspicuous edge. There are different ways to do this, but honestly, I’m not so sure that they’d be anywhere near as secure as this method. If you decide to do something else and your Pi falls in the case and your display cracks, it’s not my fault.

At this point, your Raspberry Pi should be secured, and should move with the lid of the console when you open and close it. Before you test, though, put the cloth that I told you to have in the bottom half of the console. This is a great idea for two reasons specifically:

> > > > 1\. It’s a form of insurance in case your Pi isn’t secure - your screen and Pi will be buffered against the linen rather than the hard plastic.

> > > > 2\. It’ll balance out the heavy screen and Pi fastened to the lid.

Detach everything - even the screen from the Pi, if you haven’t already - and plug in all of your peripherals that you’ve got, such as speakers, power, joypads, and so forth. If your power cable won’t fit through the case of the console, you can just bore a bigger hole to poke it through. However, the microUSB connection should fit with no problem. Then put the Pi in position and fasten the screen, which will in turn fasten through the whole on the lid, which you’ll secure with a nut. Be super careful here, it’s really easy to mess this step up.

Try it out to be sure that everything is in working order. If it is, then congratulations! You’ve now got a self-contained superconsole capable of playing nearly 30 years worth of video games. That’s pretty beautiful.

To take this all one step further, if you chose wisely when selecting your display, the display will be able to directly output everything to another screen by HDMI. You could theoretically play this system on massive projectors or huge flat-screen TVs so long as you have an HDMI cable, the right display, and the raw dedication.

So there you go. That’s a pretty ambitious project for somebody to start out with, and I’m really proud of you for making it to the end of this. It’s certainly not the end of your adventures with the Raspberry Pi, and I’m hoping that I’ve given you more than enough ways to come up with inspiration in a flash.

Conclusion

![](images/00002.jpg)

Thank you for making it through to the end of this book, let’s hope it was informative and able to provide you with all of the tools you need to achieve your goals whatever it may be. Where to Go From Here - Communities and Insight - Hacking is a community.

The next step is to just jump in. Find projects that appeal to you and start working on them, or dream up some of your own and start looking into them.

Before I bring this book to a close, I’d like to say a few words: hacking. When a lot of people hear the word hacking, they don’t think of the best dudes. They think of email scandals or LulzSec or notorious people in dark rooms behind green terminals. But that’s not what hacking is. There’s a lot more to hacking than that. Hacking is an entire frame of mind. Hacking is about tinkering and learning, experiencing, breaking things apart, making new things from old things, creating, problem solving, having the ingenuity to do something really, really incredible even though the means aren’t exactly obvious.

By working with Raspberry Pi projects, you are a hacker. Maybe not a hacker, breaching people’s security or whatever, but you’d fit right in among the hacker subculture that’s existed for going on 40 years now. And the reason for this is because it takes a certain amount of curiosity, ingenuity, and drive to truly try to make something fantastic out of nothing. So, when I say that you’re a hacker, I mean it rather sincerely. By picking up this book, you are showing that you’re a hacker.

Hackers are brilliant people, and the work they do deserves credit. Whether they’re finding security holes in important networks, whether they’re phreaking phone lines, whether they’re soldering circuit boards in their garage, or whether they’re just trying to get the LED screen connected to the Raspberry Pi to display the text they’re wanting, they are the people who ultimately will push the world forward. Because they not only see the boundaries, but they see where the boundaries break, and they push them back. My point is that you, friend, are in good company.

Going forward, if you have any questions, there are a number of fantastic online communities that are well treated to answering all sorts of questions about Raspberry Pis and other related projects you may be interested in (Intel Edison, Arduino, etc.). There are a huge number of veterans out there, tinkerers and professionals alike, who are more than happy to answer any questions that you might have.

Two that I recommend are the official Raspberry Pi forums at [https://www.raspberrypi.org/forums](https://www.raspberrypi.org/forums)  and the subreddit for Raspberry Pi (with over 150,000 subscribers!) at [https://www.reddit.com/r/raspberry_pi/](https://www.reddit.com/r/raspberry_pi/). Both of these are fantastic and active boards for you to get answers and to generally engage in the Pi hacking community at large.

Also keep an eye out for other beginners having questions, or - better yet - trying and failing. Anybody can follow a tutorial, but mistakes are where the learning happens. Keep watch for the mistakes that others make, as well as the mistakes that you yourself make. Understand why they’re mistakes, and how things could have been done otherwise in order to make things go smoother. All in all, when you’re working with Raspberry Pi, just try to make every day fun, enjoyable, and a learning experience.

In the end, I’d just like to say thank you for making it to the end of this book, I hope I’ve been able to impart some valuable help and insight. I know that getting started with Raspberry Pi - especially trying to jump in and start programming right away - can be quite a daunting task in and of itself. I genuinely hope that as you go forward with any and all of your projects that you experience the best of luck and that you look back at your time reading this book fondly.

If that was the case, then I’d love for you to leave a review on Amazon. And even if you didn’t like it, leave a review. It’s people like you who help me produce quality content.

Thank you so much for reading, and I wish you the best.

Table of Contents

[Title](#index_split_000.html_filepos167)

[Copyright](#index_split_001.html_filepos736)

[Contents](#index_split_002.html_filepos3017)

[Introduction](#index_split_003.html_filepos4289)

[Chapter 1: What is Raspberry Pi?](#index_split_004.html_filepos6248)

[Chapter 2: Under the Hood](#index_split_005.html_filepos10154)

[Chapter 3: Setting Up](#index_split_006.html_filepos20270)

[Chapter 4: Programming Essentials](#index_split_007.html_filepos29788)

[Chapter 5: Project Ideas](#index_split_008.html_filepos63367)

[Chapter 6: Your First Project - A Portable Superconsole](#index_split_009.html_filepos68062)

[Conclusion](#index_split_010.html_filepos90419)