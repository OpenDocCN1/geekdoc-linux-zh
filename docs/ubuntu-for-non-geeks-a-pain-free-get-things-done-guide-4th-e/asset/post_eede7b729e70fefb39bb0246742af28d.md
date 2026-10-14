
Internet service provider (ISP). While the router is connected to your modem via cable, the connection from the router to the computers on your local network can be wired, wireless, or both.

What does a router have to do with the defense of your computer? Well, most routers include a *firewall*, which essentially functions to keep all of the bad stuff off the Web away from your computer, much in the way that the firewall in your car keeps the heat, fumes, and noise from your engine out of the passenger compartment. This built-in firewall is one reason that even people with only one computer, who could just as easily connect their computer directly to their cable or DSL modem, use a router. Of course, just how much security the firewall in your router provides depends on which filters you select in the firewall setup software. For example, a very common and useful filter (particularly for those with a wireless network) limits Internet access to those machines specified on the firewall’s access list. This prevents your next-door neighbors from hitching a wireless ride via your ISP connection. They aren’t paying the bill, after all.

The setup software for a router is built into the router, so you don’t have to worry about software installation and system compatibility. Using your router with Linux is no different from using it with Windows. You can access the software and modify your settings via a simple web browser, as you can see in Figure 19-1. Just type the IP address of the router (usually provided in the owner’s manual) in the browser’s location bar, press ENTER, and you’ll be ready to go.

![](img/f7cef0df22f9dba5a41777808c98eece_378_0.png)

Figure 19-1: Setting up a router

## Software Firewalls

If you don’t have a router and don’t plan on getting one or if you have one but are bordering on paranoia, you might want to consider using a software firewall, in particular one of the most popular software firewalls available for Linux, Firestarter.

You can get Firestarter via the Ubuntu Software Center by searching for *firestarter* and installing it. Once it is installed, run it by selecting **System ▸ Administration ▸ Firestarter** (you might be asked for your password). Firestarter will open with a self-explanatory setup wizard the first time. Just read each screen carefully; make whatever selection you are suggested, if any; and click the **Forward** button in each of the wizard screens until you get to the last one (shown in Figure 19-2). On that screen, make sure that the box next to *Start firewall now* is checked, and then click the **Save** button. The wizard window will then close, and the main Firestarter window will appear. Assuming the correct network device was detected and selected and the correct wizard choice made, the firewall will be up and running.

![](img/f7cef0df22f9dba5a41777808c98eece_379_0.png)

*Figure 19-2: The last screen of the Firestarter setup wizard*

If the wrong network device was selected, a warning window will appear telling you so. In that case, you can do a bit of trial-and-error manipulation by selecting **Edit ▸ Preferences** in the main Firestarter window and then clicking **Network Settings** in the Preferences window that appears (Figure 19-3). In that window, select one of the other devices listed in the Detected device(s) drop-down menu, and then click the **Accept** button. Once back at the main Firestarter window, click the **Start Firewall** button (which looks like a Play button), and see what happens. If you still can’t start the firewall, repeat the process I’ve just described, this time selecting a different network device.

![](img/f7cef0df22f9dba5a41777808c98eece_380_0.png)

Figure 19-3: Selecting network devices in Firestarter

Once your firewall is up and running, there is nothing more that you really need to do. You can simply look at the Firestarter window (Figure 19-4) to see what is going on network-wise on your computer—which active connections you have, how much information has been coming and going, and whether there have been any events in which, for example, the firewall has blocked an intruder. If you click the Events tab, you can then see the details of those events, such as what connection attempts were blocked, where they came from, and when they happened.

![](img/f7cef0df22f9dba5a41777808c98eece_380_1.png)

Figure 19-4: Firestarter in action
