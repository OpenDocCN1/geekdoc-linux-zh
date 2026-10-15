# CHAPTER 34

# Advanced APT

# IN THIS CHAPTER

+   ► Using Aptitude
+   ► The dpkg Back-End
+   ► Configuring APT
+   ► Reference

In Chapter 7, “Managing Software,” we already looked at the standard desktop tools that Ubuntu provides for software installation. But the APT system is capable of a lot more than you can see by just using Add/Remove Applications: it has the powerful Aptitude command-line front-end, it has the dpkg package installer that does a lot of the hard work, and it also has a configuration file that is very easy to edit by hand. We will be looking at each of these topics in this chapter, giving you the necessary APT experience to be able to use it at any level.

# Using Aptitude

Aptitude is a command-line front end to APT, roughly equivalent to Synaptic. You can launch Aptitude simply by running sudo aptitude from your terminal. Each time it starts, Aptitude needs to load the APT cache and convert it into a tree that you can browse through. This usually only takes a couple of seconds, and you will see status bars on the bottom of the screen so you can see what is happening.

Once the cache is loaded, you can start using the program. If you have mouse support enabled on the command-line, or if you’re running Aptitude from inside an X session, you can use your mouse to click on things, including the menu bar. Without the mouse, you are left using the cursor keys and Return to find your way around the interface.

To get started, use the cursors (or your mouse) to expand the Not Installed Packages list, and look in devel > main. A list of packages in that group will appear; I have things such as CVS and build-essential. To install CVS, use the cursor keys to select it then press + on your keyboard. To show that it’s selected, Aptitude will highlight it green on