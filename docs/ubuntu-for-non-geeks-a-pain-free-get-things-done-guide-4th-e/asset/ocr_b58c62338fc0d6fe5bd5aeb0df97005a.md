As you can see, the oracle told me, “What we bring closer, grows to us,” which I will interpret as . . . well, I’m not sure what to interpret it as.
Hmmm.

pyWings was written in a programming language called Python, which actually creates scripts rather than true conventional programs. You will learn a little more about this distinction in later in the chapter, but one of the differences I can mention right off the bat is that you don’t actually have to install pyWings; you are simply going to put it on your hard drive in your home folder and run it from there, more or less as is.

# 9B-1: Getting Ready for pyWings (Installing Tkinter)

As I mentioned, one difference between pyWings and most of the other applications you know is that pyWings is a Python script. To create a graphical interface for itself, pyWings uses a toolbox known as Tkinter, which is the de facto standard (though not the only) GUI toolbox for Python. Tkinter, however, no longer comes bundled with Ubuntu, so you will need to download and install it yourself. Fortunately, this is quite easily done.

Although it is possible to whip open the Ubuntu Software Center and install Tkinter by the simple means learned in Chapter 6, it seems more appropriate in this command line–oriented chapter to . . . yeah, you got it, use the command line. That said, open a Terminal window, type sudo apt-get install python-tk, and then press ENTER. When asked for your password, type it, and then press ENTER. APT will search the online repositories and find your file, along with anything else it requires to function properly. Once it is ready, it will ask you whether you want to continue. You do, so type y, and then press ENTER. When your username prompt reappears, you’ll know the job is done, and you can go on to the next step.

> NOTE If you prefer, you can perform this installation using aptitude instead, using the techniques we discussed earlier in the chapter.

# 9B-2: Getting pyWings

You are just about ready to begin “installing” pyWings, but before you do, you need to get it from http://sourceforge.net/projects/pywings/. Once there, click the View all files button, and then download the file pywings-1.1.tar.gz. Then place the file in your home folder so that you can follow along easily with the rest of this project.

# 9B-3: Creating a LocalApps Folder for pyWings

As I mentioned earlier, you will be installing the pyWings program locally in your home folder. Installing a program locally means that you are installing the program and all its support and data files in your home folder. This makes things a bit easier, but it also means that the program will not be available to other users. It also means that if you’re not careful, you might inadvertently delete it.