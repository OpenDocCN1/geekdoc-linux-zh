# Linux kernel

Now let’s move on to the best part of building a kernel: customising it for your particular system. Inside the main /usr/src/linux-3.17.1 directory, enter:
make xconfig
If you have the Qt4 development files installed (for example, libqt4-dev in Debian/Ubuntu), this command will build and run a graphical configuration tool. For a GTK-based alternative try:
make gconfig
and if you can’t get either of the graphical versions to work, there’s a perfectly decent text-based fallback available with this command (Ncurses required):
make menuconfig
Even though the interfaces are different, all of these configuration tools show the same options. And there are a lot of options – thousands of them, in fact. If you’re reading this tutorial on a dark winter evening and you’ve got some spare time, make yourself a cuppa and go through some of the categories.
Admittedly, much of the information is ultra technical and only actually applies to very specific hardware or system setups, but just by browsing around, you can see how incredibly feature-rich and versatile the Linux kernel is. And you can see why it’s used on everything from mobile phones to supercomputers.

separate file that can be loaded on demand. If you compiled all of the features you needed directly into the kernel, the resulting file would be huge and may not even work with your bootloader. What this means is that it’s best to only compile critical features and drivers into the kernel image, and enable everything else you need (for example, features that can be enabled after the system’s booted) as modules.
So, click on the checkboxes to change their state between enabled (blank), built into the kernel (tick) or built as a module (circle). Note that some features can’t be built as modules, though, and are either enabled or not. You’re probably wondering why some options are already enabled and some not. Who made all of these decisions? Well, if you look in the terminal window where you ran make xconfig, you’ll see a line like this:
# using defaults found in /boot/config-3.8.0-21-generic
Your currently running kernel has an associated configuration file in the /boot directory, and the xconfig/gconfig/menuconfig tools find this and use it as the basis for the new configuration. This is great, because it means that your new kernel will have a similar feature set to your existing kernel – reducing the chance of experiencing spectacular boot failures. When you click on the ‘Save’ button in the configuration program, it stores the options in .config, and any future use of xconfig/gconfig and so on will use this .config file from here onwards.

# Pimp your kernel

We’ll focus on the Xconfig tool in this tutorial because it has the best layout, and it’s the easiest to navigate. Down the left-hand side of the UI you’ll see a tree view of options and categories – if you click on a category, its sub-options will be displayed in the top-right panel. And then, clicking on one of these sub-options brings up its help in the bottom-right panel. Most options in the kernel are well documented, so click around and enjoy exploring.
The enabled options are marked by familiar-looking checkboxes; you’ll also see many boxes with circles inside. This means that the selected option will be built as a module – that is, not included in the main kernel file itself, but as a

# Enabling extra goodies

Now, at the start of this tutorial we talked about customising your kernel for better performance and using experimental features. For the former, have a look inside the Processor type and features category. The chances are that your currently running kernel was tuned for the Pentium Pro or a similarly old processor – that’s not inherently a bad thing, because it means that the kernel will run on a wide range of chips, but you’ll probably want to choose something much newer. If you have a Core i3/i5/i7 processor, for instance, you will want to choose the Core 2/newer Xeon option. Don’t expect to be blown away by a massive increase in system speed, but at

# A day in the life of a kernel

If you’re fairly new to the world of Linux, or you’ve just never spent much time looking at the technical underpinnings of your operating system, you’re probably aware that the kernel is the core part of an installation and does all of the important work – but what exactly is this work? For clarity, let’s examine the kernel’s key jobs in a little more detail:
Running programs The kernel is effectively the boss of all running programs. You can’t have one program hogging the entire processor, and if that program happens to lock up, you don’t want everything else to be inaccessible. So the kernel gives programs their own slots of CPU time, ensuring that they all get on together and that one program can’t take over the machine. The kernel can also kill running programs and free up their resources.
Accessing hardware Very few end-user programs interact directly with hardware. You don’t want two programs trying to access, for example, the same USB port at the same time, leading to all sorts of horrible clashes. So the kernel deals with your hardware, providing drivers to access specific devices, and also providing abstraction layers so that higher-level software doesn’t have to know the exact details of every device.
Managing memory Just imagine if every program had free rein over your RAM. Programs wouldn’t know who owns what, so they’d end up trampling over each other, and then, suddenly, that word processor document you had open could suddenly be full of sound data. The kernel allocates chunks of RAM to programs and makes sure that they are all kept separately from one another, so if one program goes wonky, its mess-up can’t infect the RAM area of another program.