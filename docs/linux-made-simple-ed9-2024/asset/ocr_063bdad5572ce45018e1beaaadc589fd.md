# Packages:
Installing new software

Getting fresh programs onto your Linux system is, despite what you may have heard, utterly straightforward and foolproof.

![](bbox=[0.09, 0.39, 0.15, 0.46])

+   **Quick tip**
+   
+   You can also install software from Ubuntu's dashboard. Click the search button at the top of the left hand bar, the apps icon at the bottom, and search for what you want.

Y our Linux system comes pre-installed with a whole host of useful applications and software, but there will come a time – there always does – that you want something new. There are various complex ways of getting hold of new things, and perhaps they'll be routes you explore later on in your Linux life. For now, there's a much easier way to find new programs for your computer: a package manager.

Package managers deal with everything for you. They retrieve the very latest versions of your desired software from the internet. They sort out any dependencies – items your computer might be missing – that are required for you to be able to run that software. They install everything automatically. And, once your software is firmly ensconced in your PC, they deal with the process of upgrading or removing it later on. You never have to get your hands dirty. And, all being well, everything will work perfectly first time.

You might have come across something similar on your smartphone. Apple's App Store and the Android Play Store are each examples of package managers – it's unlikely you've ever had to manually download and install any apps on a modern phone. The whole process is seamless. Apple has brought the system to macOS, and Windows converts may know that Microsoft has been trying a similar scheme since Windows 8: the Microsoft App Store. Cynically its might look at that as a way for Microsoft to control its software ecosystem, and you'd probably be right to be cynical, but it's also a way to get hold of (some) programs without the hassle – and potential danger – of downloading random things from the internet. It makes sense. It hasn't really worked, but the theory is sound.

Ubuntu's desktop package manager is called *Software Centre*. It accesses a number of sources – known as *repositories* – to grab the right version of your chosen program for your computer. Or at least it does for now – Ubuntu will soon be replacing it with an alternative, *GNOME Software*, in the 16.4 release of Ubuntu. But for now, let's look at how you might use *Software Centre* to download, install and remove software – *GNOME Software*'s interface and philosophy barely differ, so this will stand you in good stead.

# Central reservation

As you can see from the annotation above right, there's not really an awful lot to *Ubuntu Software Centre*'s core interface. A big categorised list of software, buttons so you can see what's available, installed, what you've done and how downloads and installations are getting on. The key element for us is the search box at the top right of the window. It doesn't only search by software names – handy, considering the baffling monikers of most Linux packages – but by descriptions, too. So, for example, if we wanted to find a game, we might search, yes, '*game*'. And everything with '*game*' in its title, short description, and long description will pop up. Obviously that's a very broad example, but imagine you're looking for a new email client: it makes a lot more sense to type '*email*' and find what you're looking for than it does to type *MBXMailcomper*.

Teeth-grindingly annoying nomenclature aside, then, let's install something. And why don't we get a bit meta? Before *Software Centre*, Ubuntu featured a program called *Synaptic Package Manager*, which wed wagger will still be available after the move to *GNOME Software*. It does the same things (searching for packages, fixing dependencies, upgrading and

![](bbox=[0.09, 0.68, 0.49, 0.89])

> Installing software requires that you have admin rights to your system – It's a good way of stopping other users from installing software you don't want!