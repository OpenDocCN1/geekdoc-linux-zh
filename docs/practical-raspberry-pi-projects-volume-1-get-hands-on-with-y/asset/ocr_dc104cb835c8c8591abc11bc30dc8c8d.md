# 13  Test the connection

The easiest way to test the Wi-Fi connection is to shut down the Raspberry Pi using **sudo shutdown -h now** and then remove the wired network connection and reboot the Raspberry Pi by removing and reattaching the micro USB power connector. If the Wi-Fi connection has worked, you should now see the splash screen with IP address again.

![](bbox=[0.07, 0.09, 0.93, 0.55])

Above Once fully configured, load your pictures and video to complete your digital photo frame!

# 15  Test with video and more

Pictures are great, but Screenly also allows you to display videos (with audio if you wish) and web pages, which really is a huge benefit. This is perfect if you want to enhance your digital photo frame even further or perhaps display the local weather and news to keep yourself informed. Plug in your speaker – we would recommend The Pi Hut portable mini speaker (available from bit.ly/1xEpBNZ) or anything similar.

# 16  Place in situ and enjoy!

Once you have got Screenly all set up and loaded all of your favourite pictures and videos onto it via the web interface, it is now time to enjoy the fruits of your labour! Mould the spider stand if you have one into shape by taking the middle two legs at the top and bending them downwards and backwards. Then spread the front-middle legs a bit wider to give a good base and shape the outer legs at the top and bottom to support the screen. You are then ready to give it its permanent home – our expert’s is on the mantel piece over the fireplace!

# 17  Other project ideas

In this tutorial we have looked at just one fairly basic application of Screenly and the HDMILI. You could use this powerful open source software to run your digital signage empire, share screens in schools and clubs, or as a personal dashboard using a suitable web page. Whatever you make, please don’t forget to take pictures and send them to us!

# 14  Upload pictures to Screenly

Once again, you will need to visit the Screenly OSE web interface by entering the IP address into another computer. Since you are now using a wireless connection, the IP address may be different to the previous one. You need to select the ‘Add Asset’ option on the top right-hand side, which should launch a pop-up options screen. Select Image from the drop-down box and you then have the option of either uploading the image or grabbing it from a URL, using the corresponding tabs. Enter the start date and end date of when this image should appear, and how long it should appear on screen for, then press Save. Repeat this step for each of the pictures.

![](bbox=[0.12, 0.58, 0.43, 0.76])

# Access Screenly from afar

The default Screenly image is essentially some additional software running on top of Raspbian OS. This means that SSH is enabled by default (it’s why we changed the default password in Step 11) so it’s now possible to access the command line, as well as the Screenly dashboard, from outside of your LAN. We recommend setting a static IP for your Screenly-powered Rasp Pi from your router setting up SSH with keys on your Pi, and port forwarding on your router for ports 22 and 8080. The Screenly dashboard has no login so anyone can access it, but an authentication feature is imminent.