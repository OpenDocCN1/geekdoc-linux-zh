Manually adding an .xinitrc file with the following finally let Starship bring up a usable LXQt desktop. Again, this isn't to say what occured was wrong. But based on past Linux experience, the author was expecting the installation to include all dependencies and the launch script to start everything up "automagically". But in FreeBSD, you need the "screwthat" to install X.org yourself, launch it in the /standard way, and make sure your environment it set to trigger LXQt when you do. The designation for devices are similarly different. In FreeBSD, you reference the first internal drive with /d/ad/0/. Partitions are alternately referred to as slices, so the second partition may be /d/ad/0s1/ or /d/ad/0s1/ depending on where you are looking. Likewise, the default CD-ROM is represented by /d/ev/cd0/. Is using "ada" for the hard drive "wrong"? Who knows! Just understand that you may need to do some translation of nomenclature along the way.

# FreeBSD is DIY

This speaks to the philosophy of BSD, which is to assemble the system you want with the software you want. In the course of writing this article the author frequented the FreeBSD message boards (https://forums.freebsd.org) on one occasion looking for hints on a GUI package manager. Firstly, the FreeBSD community is very active on forums, and give extremely accurate answers. But the answer to questions like "Where's the GUI package manager for FreeBSD" was a resounding, "We don't have one, we like pkg or port. Feel free to try some until you find one you like though." This wasn't intended to be dismissive, but rather to encourage the poster to build his/her platform to taste. Yet the FreeBSD developers have taken pains to make the assembly easy where it makes sense. A quick confession: this author was fully prepared to hunt down Xorg configs (or XF86Config files, as those of a certain age will remember them) and tinker with modelines. At one time this was an extremely painful part of getting a Linux system running. But the X.org installation process on FreeBSD, the graphics system was configured, and a nice-looking desktop was the result. So, you may ask, why did the issue in the last section happen? Why didn't the whole desktop stack just install? It's because FreeBSD didn't assume this author wanted to use X.org at all. Maybe Wayland was the intention. In this sense FreeBSD will often "do what you say, what you mean". So you should be sure about what you're doing before you issue commands in FreeBSD, especially if you don't understand their function (e.g. there's a command that will happily re-build your entire system from source, likely occupying it for several hours) or target devices as mentioned in the previous section. In other words, understand the FreeBSD parlance for disk partitions before you start formatting drives.

![](bbox=[0.09, 0.86, 0.46, 0.95])

Installing the nano text editor using the Ports system. It fetches the source for all dependencies, compiles, and installs them.

![](bbox=[0.49, 0.1, 0.85, 0.24])

Stated another way, think of modern Linux distributions as an office suite with easy-to-use buttons that sometimes don't get you precisely the result you want. FreeBSD, on the other hand, is LaTex. You can get exactly the end product you want, you just also need to know exactly how to go about it.

# Quickly, back to Linuxland!

This short journey into the world of FreeBSD tracked with what you'll find a lot in open source. It's easy to get started and achieve some measure of success and productivity. But as you start to dig into it, you quickly learn how far you still have to go. Mentioning a couple of key take-aways at this point is prudent if you're thinking of giving FreeBSD a spin:

+   » Measure twice, cut once. aka do your research.
+   
+   » The FreeBSD Handbook (www.freebsd.org/doc/ handbook) is your best friend.
+   
+   » Plan to do more things in the terminal than with Linux.
+   
+   » FreeBSD often defaults to MVP (minimum viable product). You may need to manually add things that just "come with" Linux.
+   
+   » All that said, for Linux users a short holiday in FreeBSD is a great learning experience. And when it comes to the open source world, isn't that the point? (0.85, 0.56)

# USING THE PORTS COLLECTION

First, navigate your way to the Ports Collection on your machine:

```
cd /usr/ports
```

A Port is basically a recipe for building the program in question. Spin through the various sub-folders and you'll start to see some old friends, such as desktops in the X11-wm folder, the Firefox browser in /www, and (huzzah!) Emacs in /editors. In order to search for applications, we first need to index all the ports in the system:

```
cd /usr/ports
make index
```

Use the following command to search for something:

```
make quicksearch name=[name_of_your_search_target]
```

This will show you the name, location and a short description for your results. If you find what you want and would like to install it, you can use the command below. Just bear in mind you'll be compiling, not just installing, the application and all its dependencies:

To build and install a program, navigate to its Port directory and issue the below command. Note the clean parameter will make sure any temporary build files are deleted once it's done.

```
make install clean
```

Sit back and watch the messages scroll by, and after a few minutes/hours/days (depending on the size of the application), your hot-off-the-press program will be ready to run. Uninstalling is just as easy (again, from the Port directory):

```
make deinstall
```

Sometimes installing binary packages is the quickest and easiest way to get the software you want. And like Linux package managers, it is dependency aware.