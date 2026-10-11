# Simplifying NVIDIA driver installation on Ubuntu

**NVIDIA Drivers Made Easy**

A terminal-based solution helps ease the frustration of installing NVIDIA drivers.

BY ADAM DIX

P
roprietary NVIDIA [1] drivers on Linux are an evli so necessary that even the staunchest of open source advocates will find a use case for them from time to time. Whether for gaming, mining, or some other hardware-accelerated task, the green giant is here to stay, for better or for worse, and sadly seems to be wholeheartedly opposed to going all in with open source. Unlike AMD [2] driver support – which is simply fantastic on Linux, as I am sure most of you know already – NVIDIA doesn’t seem to be willing to play nicely. One has to wonder if they feel that they simply don’t need to, that their sway over the market sets them apart from others and absolves them of the responsibility that the other players feel to their customers. Who knows. What I do know is that NVIDIA Linux driver support is worse for the wear despite the hard work of many folks in the community. The worst part about this is the effect that it has on beginners to Linux who have heard all of the wonderful things about it and give it a try, only to have their system either hobbled with Nouveau drivers or who have to go through what I am about to discuss below. It is a sad state with a clear and obvious solution that I am afraid we won’t see come to fruition any time soon.

All may not be well, but not all is bad either. At least we have some kind of (albeit proprietary) solution to rely on.

I will focus on Ubuntu [3] here as that is what I typically use nowadays as a simple, Linux-based install for whatever I need to do, but also because this is statistically likely to be what a beginner would first try out. While I started with Red Hat [4] (pre-Fedora [5]), today most folks tend towards Ubuntu, a derivative of it, or perhaps another Debian derivative their first time out.

While Ubuntu itself has a driver’s install section, not all Ubuntu derivatives necessarily do, and in some cases, even if your distribution does have an advanced driver install section, it may be difficult to find, especially for a beginner. Furthermore, there may be confusion about which group of packages to install and which version of the NVIDIA proprietary driver you want to use. I have personally also found that often after choosing a driver and clicking on Apply, the window becomes unresponsive, or at least appears that way. While the basic open source Nouveau [6] Linux driver is adequate for most tasks, hard-core users will often find a need for proprietary drivers. While I can’t fix the terribly dated control panel interface that NVIDIA offers in their proprietary driver package installation, I can help you get it installed and walk you through how to deal with it when that install inevitably breaks.

In this article I’ll show you how to figure out which graphics drivers to use on Ubuntu Linux and derivatives with a simple, built-in command which I find quicker and easier than opening up the GUI equivalent. I will also show you how to deal with the near certainty of the black screen that you’ll encounter afterwards. You see, much like a YouTuber trying to install Steam [7] on Pop\_OS [8] for the first time, I too have had struggles with using the GUI for installing NVIDIA drivers. However, unlike the typical YouTuber [9], I have not had any issues doing the same task in the terminal.

It should be noted that more than one package may exist for NVIDIA proprietary drivers, and you may need to test a few different driver packages before you figure out which one works best for you. Furthermore, devices with Optimus [10] capability may or may not work properly in terms of Optimus switching. For those who don’t know, don’t recall, or weren’t around in those days, Optimus is an NVIDIA and Intel [11] software scheme intended to allow the user to choose between NVIDIA or Intel graphics at will within the OS itself. While packages from the likes of system76 and others do make Optimus more capable than it was when it was first introduced, and in many cases fully functional, there still

![](bbox=[0.42, 0.79, 0.55, 0.89])

> **The Author**
> 
> Adam Dix is a mechanical engineer and Linux enthusiast posing as an English teacher after playing around a bit in sales and marketing. You can check out some of his Linux work at the EdUbudge Linux website, https://www.edubudgie.com.