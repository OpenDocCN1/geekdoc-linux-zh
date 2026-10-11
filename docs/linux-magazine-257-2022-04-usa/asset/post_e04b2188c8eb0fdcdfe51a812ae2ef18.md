
![](img/8286bf901ba268fe114d66ada92d1dd6_48_0.png)

Open the link to your Checkmk site in your browser. You can open the link shown on your terminal. Log in with ckadmin and the password you copied from the terminal. You will see an empty dashboard. Go to User in the sidebar on the left and, under Profile, click on *Change password* to change your password (recommended).

After that you can start adding hosts to your monitoring (Figure 4). In my case, I will add my router. Go to *Setup | Hosts* and click on *Add host*.

In my example, I only have to add the hostname *tplinkmodem.net*, because TP-Link set up the DNS for their devices and, thus, Checkmk can resolve the IP address for your hostname automatically. I recommend using this option, if available. If that is not the case, you will also need to add your device’s IP address by activating the checkbox next to *IPv4 address* and entering the IP address.

For my router, I want to work with SNMP, but by default, Checkmk assumes that you use the Checkmk agents to monitor systems. The Checkmk agents are great for monitoring servers, but on most network devices, you cannot install additional software. Thus, go to *Monitoring agents*, check the box *Checkmk agent/API integrations*, and choose *no agent*.

Next, check the box labeled SNMP (Figure 5). Choose your SNMP version—*SNMP v2 or v3* works in most cases. Because I did not change the SNMP community, I can leave the SNMP credentials box unchecked—by default, Checkmk assumes that the password is *public*. If that is not the case, you have to set the community string under *SNMP credentials*. Leave the other items unchanged.

Next, click on *Save & go to service configuration*. Checkmk will now automatically discover any relevant monitoring services on that host, and you should then see a list of *Undecided services*. Click on *Fix all* to monitor all of these relevant services (Figure 6). That will add all of the detected services to the monitoring and will also remove services that have vanished. You can manage the services manually, of course, but the `Fix all` function makes it a lot easier.

In this case, Checkmk simply detected all of my router's ports that are currently online, plus the uptime and the SNMP info check – 10 services in total for me. If there is an official check plugin available for your device, Checkmk will detect relevant information automatically. The 2,000 official check plugins cover the equipment from most common professional network vendors. This collection of plugins makes Checkmk a great tool for network monitoring and saves you a lot of time.

I recommend the blog post “Network Monitoring with Checkmk” [5] for further information on monitoring with SNMP. But before you start with outside reading, follow the last step to complete this tutorial.

## Activating Changes

Finally, you need to activate the changes by clicking on the highlighted field with the yellow `↑` at the top right corner that counts the number of changes. After that, click on `Activate on selected sites`, and you will have successfully added the first host to your monitoring.

The activation of changes is a safety mechanism. All changes made will be listed under `Pending changes` (Figure 7). You can review any listed changes before they affect your monitoring. Checkmk differentiates between the Setup menu as a configuration environment, in which you manage the hosts, services and settings, and the Monitor menu, in which the actual operational monitoring takes place. New hosts and other changes in the configuration initially have no effect on the monitoring. You need to activate these before they can go into production.

You find your host now under `Monitor | Overview | All hosts`. Click on a host, and you will see an overview of all the monitoring services of that host. Figure 8 shows the overview of my router. You can click on each service to see more details.

You will find the agents for various operating systems, such as Windows and a number of Linux distributions, via the sidebar by clicking on **Setup | Agents | Linux**.

### IN-DEPTH Checkmk

The Checkmk documentation [7], as well as in the official Checkmk forum [8], will provide answers for all your Checkmk questions. ■■■

### Conclusion

This article is intended as a proof of concept. I used the SNMP monitoring agent in the example because SNMP is supported on most home routers. However, be aware that there are some security concerns with SNMP. The US government Cybersecurity and Infrastructure Security Agency recommends that you only use SNMPv3 and has outlined additional precautions [6].

This tutorial ends here, but your real experience with monitoring has only just begun. If you want to continue, you should add your host server to the monitoring as well. Checkmk provides some lightweight, but powerful monitoring agents for server monitoring.

After you install, the procedure is similar. Add the host that you want to monitor, but you can leave the box **Checkmk agent/API integrations** unchecked and should not switch that to SNMP. By default, Checkmk assumes you are using Checkmk agents to monitor systems.

The Checkmk documentation [7], as well as in the official Checkmk forum [8], will provide answers for all your Checkmk questions. ■■■

### Author

**Martin Hirschvogel**, Director of Product, joined tribe29 in 2018 and since then focuses on improving Checkmk. Martin heads the product marketing team and leads development around modern DevOps technologies such as Kubernetes. Before joining tribe29, he worked as Chief of Staff at Team-Viewer and was a consultant at Boston Consulting Group.

### Info

1.  Checkmk: [https://checkmk.com](https://checkmk.com)
2.  Nagios: [https://www.nagios.org/](https://www.nagios.org/)
3.  Checkmk download: [https://checkmk.com/download?edition=cre&version=stable&dist=ubuntu&os=focal](https://checkmk.com/download?edition=cre&version=stable&dist=ubuntu&os=focal)
4.  OMD: [https://omdistro.org/](https://omdistro.org/)
5.  "Network Monitoring with Checkmk": [https://checkmk.com/blog/network-monitoring-with-checkmk-2-0](https://checkmk.com/blog/network-monitoring-with-checkmk-2-0)
6.  Reducing the Risk of SNMP Abuse: [https://www.cisa.gov/uscert/ncas/alerts/TA17-156A](https://www.cisa.gov/uscert/ncas/alerts/TA17-156A)
7.  Checkmk documentation: [https://docs.checkmk.com/latest/en/](https://docs.checkmk.com/latest/en/)
8.  Checkmk user forum: [https://forum.checkmk.com/](https://forum.checkmk.com/)

![](img/8286bf901ba268fe114d66ada92d1dd6_50_0.png)

Figure 8: Viewing all the monitoring services on a host.

## Adjusting Cell Phone Photo Orientation with Go
**Sunny Side Up**

![](img/8286bf901ba268fe114d66ada92d1dd6_51_0.png)

Cell phones often store photos upside down or sideways for efficiency reasons and record the fact in the Exif metadata. However, not all apps can handle this. **Mike Schilli** turns to Go to make the process foolproof. By *Mike Schilli*

**S**omehow, I seem to hold my cell phone wrong when taking pictures. It often happens that a picture that looks right in the phone’s photo gallery is suddenly upside down or on its side when I want to send it to friends on WhatsApp. A quick look at the metadata of the photo in question reveals what’s going wrong (Listing 1) [1].

It appears that my phone is saving images with the wrong orientation, but it is also storing the correction value, which shows up in the JPEG format’s Exif header to tell you how the photo actually should be rotated. I don’t know who came up with this idea, but assuming that any app looks in the Exif header first and then aligns the image correctly seems like a fundamental flaw to me. There’s no doubt in my mind that the original camera app should perform the rotation when the picture is taken, rather than having the work done downstream time and time again by an unmanageable number of photo apps.

**Listing 1: Photo Metadata**
```bash
$ exiftool pic.jpg | grep Rotate
Orientation: Rotate 180
```

**Author**
**Mike Schilli** works as a software engineer in the San Francisco Bay Area, California. Each month in his column, which has been running since 1997, he researches practical applications of various programming languages. If you email him at mschilli@permeister.com he will gladly answer any questions.

![](img/8286bf901ba268fe114d66ada92d1dd6_51_1.png)

## Upside Down World

Figure 1 illustrates that the cell phone still displays the image the right way around in its photo app, even though it was stored incorrectly. The desktop version of the WhatsApp client in the browser, however, obviously ignores the associated Exif header and sends the picture upside down (Figure 2). Imagine the recipient’s reaction to receiving a message about my surf trip to Ocean Beach in San Francisco with a photo on its head! High time to write a Go program that correctly orients a photo retrieved from a phone and then deletes the Exif header entirely, so that any downstream application will process the image as-is – very much like GIMP (Figure 3) does when it sees a rotated photo. While I’m at it, I’ll throw in some algorithms for rotating images 90 or 180 degrees: After all, someone might ask about them in your next job interview.

![](img/8286bf901ba268fe114d66ada92d1dd6_51_2.png)

**Figure 1: My smartphone shows the image the right way round …**
Photo by Gurt with hat on: Unsplash
