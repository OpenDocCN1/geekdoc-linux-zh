The problem with `make config` is that it is just downright tedious. Typically, you will only be changing a very few options and leaving the rest in their default state. But `make config` forces you to step through each and every one, and contemporary kernels have well over 2000 options. Personally, I've never used `make config` and I honestly wonder why it is still in the kernel package.

`make menuconfig`, based on the `ncurses` library, brings up the pseudo-graphical screen shown in **Fig. 12.6**. Here, the configuration options are grouped into categories and you only need to visit the categories of options you need to change. The interface is well explained and reasonably intuitive. But since it is not a true graphical program, the mouse does not work. The same help text is available as with `make config`. When you exit the main menu, you are given the option of saving the new configuration.

![](bbox=[0.15, 0.35, 0.85, 0.71])

# Figure 12.6
Make menuconfig.

While most true Linux hackers seem to prefer `menuconfig`, my choice for overall ease of use is `make xconfig`. This brings up an X Windows-based menu, as shown in **Fig. 12.7**. Now you can see all the option categories at once, and navigate with the mouse. Of course you must be running X Windows to use this option, and you must have the `g++`, Qt graphics library, and Qt development tools packages installed.