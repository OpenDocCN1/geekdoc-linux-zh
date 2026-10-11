# # Getting connected

Now let’s tackle some connectivity and Internet hurdles.

![](bbox=[0.78, 0.01, 0.98, 0.19])

# ## Going slower

**My Internet connection seems really slow — downloading files takes forever. Do I need to fix this in Linux or change my router’s settings?** Stay away from your router settings until you have tried everything else — you could end up breaking a fully working setup. The first step is to check that it really is slow, by using a service like [http://speedtest.net](http://speedtest.net). Next, check that nothing is sucking up your bandwidth in the background. A good program for this is `nethogs`, which you may have to install from your package manager:

```
sudo nethogs eth0

```

This gives a top-like display of what’s using your bandwidth. If you’re connecting to your router by wireless, try a wired connection to rule out Wi-Fi issues. If that makes a difference, try testing in different locations.

There’s also the possibility of congestion with other wireless routers from your neighbours, which can be avoided by switching your router to a different wireless channel. You can see the wireless channels in use with this command

```
sudo iwlist wlan0 scan \| grep ‘e Address: e Channel: e ESSID:’

```

`iwlist` produces a lot of output about each access point it discovers, hence the need to filter it with `grep`. You can also use something like *Wi-Fi Analyzer* on Android, which gives a graphical display of the channel and strength of all access points in range, enabling you to map any points where the signal from your router is weak as well as identifying competition for bandwidth.

There’s also the highly scientific test of picking up the phone: if the line is noisy, you will suffer reduced speeds and you’ll need to report the problem to your line provider. If all the above checks show nothing, check with your ISP before tampering with previously working router settings.

# ## Streaming video

**When I try to watch videos on Amazon Prime or Netflix (I have accounts with both) I get a message saying my computer is unsupported. Can I fool them into thinking I am running Windows? Will that let me watch the services I have paid for?** These services use *Silverlight*, a proprietary technology from Microsoft, to render the video and apply DRM. There’s no *Silverlight* for Linux but there is a solution called *Pipelight*, which is a browser plugin that in turn uses Wine to run *Silverlight*. It requires a patched Wine but all the packages you need are available for most distros. Users of Ubuntu-based distros can add a PPA and install everything with:

```
sudo add-apt-repository ppa:pipelight/stable
sudo apt-get update
sudo apt-get install pipelight-multi

```

This adds the *Pipelight* PPA and then installs the software. Instructions for other distributions are at [http://bit.ly/PipelightInstall](http://bit.ly/PipelightInstall). Set it up with:

```
sudo pipelight-plugin --create-mozilla-plugins
pipelight-plugin --enable silverlight

```

This will download the required *Silverlight* software and set up plugins for your browser. Installing *Pipelight* isn’t enough to watch your videos; you will still be denied access because your browser tells the website you no running Linux. Install one of the *User-Agent* control extensions for your browser: such as *user-agent-overrider* or *ucontrol* on Firefox or *user-agent-switcher-for-chrome* if you use Chrome. Then use it to set your User Agent to “Firefox for Windows” and enjoy your streaming video.

![](bbox=[0.1, 0.4, 0.5, 0.7])

> **Wi-Fi Analyzer on Android shows access points in range and which channels they use, so you can set yours to avoid competition.**

# # The last but one resort

When your computer seems totally locked up and no amount of key bashing has any effect whatsoever, the last resort is to cut the power. With all the risks of data corruption this entails, but there’s one more thing you can try: the Magic *SysRq* keys. These are special key combinations that can be used to shut down a locked-up system reasonably gracefully. Their name comes from the fact that they use the *SysRq* key, sometimes marked *PrintScr*, and they are truly magic.

Even if your keyboard does nothing else, these work because the kernel sees these key presses directly with no user-space software getting in the way.

While holding down *Alt* and *SysRq*, press each of these keys in turn:
* **R** – resets keyboard.
* **E** – exits all remaining running programs with a *KILL* signal.
* **I** – interrupts all running programs with a *TERM* signal.
* **S** – syncs all filesystems.
* **U** – unmounts all filesystems and remounts them read-only.
* **B** – reboots.

There are various mnemonics to help remember this key sequence, some of them harder to remember than the *SysRq* sequence itself — there’s one to do with elephants. The one I find easiest to remember is that it’s **BUSIER** backwards, but the one I like most is “Reboot Even If System Utterly Broken”.