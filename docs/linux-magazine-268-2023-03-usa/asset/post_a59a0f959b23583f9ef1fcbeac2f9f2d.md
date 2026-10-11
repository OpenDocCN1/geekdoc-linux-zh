
## Go In-Depth with Rocky Linux

Download this free focus guide, and learn why Rocky Linux is gaining a wide audience with users around the world.

### ADMIN

Network & Security

Focus Guide

### INSIDE ROCKY LINUX

- **The New Kid**
  Find out why Rocky is emerging as a leading enterprise Linux
- **Rocky in HPC**
  Explore the tools for high-performance environments
- **Migration Stories**
  Moving from CentOS with migrate2rocky

We interview Rocky founder Greg Kurtzer

WWW.ADMIN-MAGAZINE.COM

US$ 7.95

### Download free!

https://bit.ly/Inside-Rocky-Linux

## INTRODUCTION

### LINUX VOICE

In the old days, if you wanted to switch between Linux systems, you needed to set up your computer to dual boot. Then virtual machines entered the picture, which made it easier to switch temporarily. But virtual machines were still more trouble than many users want to take, especially if you just needed to change temporarily to run a test or check a program. This month we show you an alternative option for switching Linux systems in a Linux session. You’ll learn how to set up Ubuntu (or another Linux) to run in a Docker container. Also in this issue of Linux Voice, view television on Linux with IPTVnator and visualize your LEGO projects with LDraw and LeoCAD.

![](img/e3f454b04d121b3b3750fddfda8dd21e_70_0.png)

### LINUX VOICE

- **Doghouse – Software Freedom** Jon "maddog" Hall Restricting uses for FOSS may seem appealing, but it also might not be the solution some imagine. 72
- **Docker** Hans-Georg Eber Do you work with Ubuntu but need to test something on openSUSE? You don’t need a second PC or a virtual machine – a single container is quite enough. 73
- **IPTVnator** Erik Bärnwaldt The IPTV standard lets you view your favorite channels on Linux. 80
- **FOSSPicks** Grahm Morrison This month Grahm looks at LosslessCut, Webcamoid, Sniffnet, and more! 84
- **Tutorial – LDraw and LeoCAD** Daniel Tibi LDraw and LeoCAD help you become a virtual LEGO architect. 90

![](img/e3f454b04d121b3b3750fddfda8dd21e_70_1.png)

## MADDOG'S DOGHOUSE

![](img/e3f454b04d121b3b3750fddfda8dd21e_71_0.png)

> Jon "maddog" Hall is an author, educator, computer scientist, and free software pioneer who has been a passionate advocate for Linux since 1994 and facilitated the port of Linux to a 64-bit system. He serves as president of Linux International®.

Restricting uses for FOSS may seem appealing, but it also might not be the solution some imagine.
BY JON "MADDOG" HALL

### The tool isn't the problem

Recently the question of whether free software (or even open source) should have some clause put into the license to keep the software from being used for "bad" purposes came up again. I believe that most of this was inspired by the war between Ukraine and Russia, and people not wanting their software used for purposes of war. Some of this is probably also inspired by various governments using computer vision software to spy on their citizens or open AI software to establish surveillance. One person even brought up the concept of using "his" free software in nuclear weapons.

I am a pacifist. I do not believe in war as a solution. However, this does not mean that I would just throw up my hands if a warmongering power attacked my country and started harming people. Therefore I can understand the feelings of these people.

However, there are many other things that some people do not like, and such people would object to others using "their" software for doing these things.

Some people do not like the government, so they do not want the government to use their software. Some people do not like the military, so they do not want the military to use their software, even if it is not for killing purposes. Some people do not like the police. Some people do not like religious organizations, and some do not like atheists. The list goes on and on, and if you draw a circle around each of these groups, eventually the Venn diagram shows the null set of people able to use the software. And if no one uses the software, what is the reason for writing it?

Another issue is the concept of software ownership. A particular person, perhaps the founder of the project or the team leader, may try to limit the use of the software, but are they the only person who wrote it? Do all of the contributors agree with this limitation? One of the reasons why the Linux kernel project is still back on the 2.x license of the GPL is that there are thousands of contributors and thousands of copyright holders, who would all have to agree to the change in the license. Some of these contributors have left the project, or died, making it really difficult to get their permission to change the license.

People may have heard of open source projects that change the licensing. Normally this is done with a fork of the project where the original license is maintained for the code released before the license change, and the modified license is applied to the forked code after. Another way of changing a license is to have all the contributors assign their copyrights to an entity (either a person or a corporation) so that person or corporation has the ability to change the license. This is why the GNU project could go from the GPL 2.x licenses to the GPL 3.x licenses without having to get permission from thousands of people.

But trying to get thousands of people to agree on changing the license to include sanctions against some group of people or a country would probably be close to impossible, and a very dangerous precedent.

Even the discussion of such a path would create horrible ripples. In the early days of Free and Open Source Software (FOSS), intellectual property lawyers would read over the many licenses of FOSS software just to make sure they was not some "gotcha" that might affect the companies they represented and prevent those companies from using the software. This inspection by these lawyers is one of the reasons given for a limited set of open source licenses to be generated and used. Once a lawyer has inspected a particular type of license for its terms and conditions, they do not have to inspect it again. If now there were new restrictions superimposed on end uses, you would open this inspection again and many companies would give up using and contributing to open source.

Finally, open source software will find its way to people who want to use it for bad purposes no matter what you do. Just as locks only keep honest people honest, licenses will not prevent evil people from using software for evil purposes.

The solution to this is not to blame the tool, but the user. A hammer can be used to build a house or it can be used to kill a person … used for good or for evil. It is the end developer who is helping to build the weapon or wage the war that we need to stop, not the FOSS in the pipeline.

## Use Ubuntu and other distributions as Docker containers

### Cleanly Docked

Do you work with Ubuntu but want to test something quickly on an openSUSE system? You don’t need a second PC or a virtual machine to do it – a single container is quite enough.

BY **HANS-GEORG EBER**

A virtual machine (VM) lets you use software intended for a different Linux distribution or even a different operating system. But setting up a VM can be time consuming. If you use VirtualBox, VMware [1], or Gnome Boxes [2], you can configure and start a virtual PC in the program interface before proceeding with the regular operating system install. After completing this procedure, the window will contain a full graphical desktop, such as KDE or Gnome, and you can boot and shut down the VM like a real PC. In many cases, a full install is exactly the solution you need, but sometimes you may just want to quickly test a program. Then the overhead for a VM install of a complete system is disproportionate to the results. The reasons why you cannot always run programs directly on your Linux system are revealed in the "Library Dependencies" box.

If you develop your own software, you may want to test whether the program files you generate will run on all distribution versions you support. Can the RPM or Debian package you generated be imported? Are all dependencies on libraries met so that the program actually launches? Finally, does it work as expected? Again, using a VM is a little excessive for these software tests. Containers offer an alternative to VMs or real hardware: They do not virtualize a complete computer and are therefore not suitable for all purposes, but in many cases they are perfect for the use case at hand. The advantage they have is that of resource efficiency (lower RAM and disk space requirements), and they can be set up far faster than a VM. You can deploy a new container in seconds, while a fresh installation in a VM will take around 15 minutes. Even when cloning an existing VM, you can

### Library Dependencies

The reason why you cannot run arbitrary Linux applications on just any system is that the program files usually contain only parts of the binary code that the computer executes. Much of the functionality is found in library files that Linux additionally loads at program startup time. For example, if an interactive program in text mode wants to read a line of text, it does not use its own routine for this, but instead resorts to the `read1` line function from the library of the same name. Figure 1 shows a small sample program that reads a line of text and outputs it unchanged with a hint. The code for the input and output comes from the `read`1 line library function for the input and from `pr`1`int` for the output. When compiling with GCC, the `-`read`1` line option ensures that the compiler notes the dependency on the readline library in the generated program file. The last command in Figure 1 shows all the libraries that the test program needs, including `libread`line`.so`.8. The file extension `.so.8` indicates that the program expects a specific version of the library, version 8. If you try to run the program on a machine with the older readline version 6 or 7, the program loader will fail to find the library and will complain (Listing 1). Missing libraries can be installed later on: Linux is quite flexible and lets you install different versions of the same library at the same time. Whether you will find a missing version for a particular Linux distribution is another question. There is so much dynamism in Linux and the applications available for it that each distribution update also updates a few library packages. Programs that require libraries that are too new or too old will no longer run. Switching to a different distribution, such as from Ubuntu to openSUSE, becomes even more difficult because distributors often decide for themselves to keep certain software packages at a version below the latest available one. A program compiled for openSUSE might then need libraries from two different releases on Ubuntu.
