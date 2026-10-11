
## 32 The CPU and RAM Usage Is Too High

If you're running a server, it makes sense to keep an eye on CPU and RAM usage so you know that your system is coping with the load you are putting on it. A good way to do this is using third-party services such as New Relic; however, on the box itself you can also check usage using the `top` commands. Running top on its own will sort by top processor users; however, if you hit capital M (Shift+M), sorting will be by memory usage. Remember that high CPU and particularly memory usage isn't necessarily a bad thing, especially on a server running fairly consistent processes. Unused memory is wasted memory!

## 33 PHP Isn't Working in My LAMP Stack

When configuring the LAMP (Linux, Apache, MySQL, PHP) stack on your server, there is a simple trap you can fall into. After installing the PHP packages, you may find that your scripts aren't being executed and are instead being printed to the screen, despite restarting Apache2 and doing everything you think you should be doing. The usual culprit? Forgetting to install the libapache2-mod-php package, which integrates PHP with the web server. It's a common mistake, easily done, and it's not the easiest package name to remember off the top of your head!

## 34 My Server Won't Send Outgoing Mail

> You will need to install an MTA

If you want to send email from your Linux server, you will need to install an MTA (mail transfer agent) such as Postfix in order to do so. The best way to install Postfix and associated utilities on Ubuntu is using:

```bash
$ sudo apt-get install mailutils
```

Near the end of the installation process, you will be prompted to select a 'mail server configuration that best suits your needs' – choose 'Internet site' (the default option). You'll be prompted to provide a domain name; ensure the DNS for this name matches the IP address of your server. Now the most important step – to set the server to only allow mail sending from localhost, edit /etc/postfix/main.cf and replace `inet_interfaces = all` with `inet_interfaces = localhost`. To test sending mail, use the command:

```bash
$ echo "This is a test email" | mail -s "This is a test subject" me@myemailaddress.com
```

## Just In Case...

What happens if it all goes wrong? You may have a hardware issue or your Linux problem means you need to wipe your disk

![](img/6866071e033820549b214c239744aaa0_67_0.png)

Above A comprehensive, tested backup solution will give you peace of mind – particularly as you tinker around with your Linux install!

## 35 I Need a Backup Plan

You finally have your Linux machine exactly how you like it. Well done! So do you fancy going through that process again? We suspect not. If your hard disk fails, do you have vital data you want to save? We imagine so. With this in mind, you should ensure that you have a reliable backup strategy for your machine, whether it is a desktop or a server.

Commercial solutions are available such as Crashplan which are very accomplished (with free friend backup) and of course there are excellent free equivalents such as CloudBerry Backup and open source options too, such as Bakula or Bareso.

> If you want to have ultimate control over your backups, you may wish to roll your own

There are a multitude of different backup scripts available for download across the internet, which provide an ideal starting point for your own script. How it works will depend on what you want to back up – on a desktop it is likely to be primarily file-based, but on a server you may also want to back up databases. A common approach is to prepare a backup archive locally and store it remotely on a service such as Amazon S3, automatically deleting files after a specified amount of time.

Don't forget one of the golden rules of backup: ensure that you test your backups with a restore now and again. Admittedly, this is easier to do on servers than workstations, but if you never put your solution to the test, you can't be 100 per cent sure it works!

---

## 1,500 FOOTBALL PITCHES EVERY DAY!

Did you know that European forests, which provide wood for making paper and many other products, have grown by 44,000km² over the past 10 years? That’s more than 1,500 football pitches every day†

Love magazines? You’ll love them even more knowing they’re made from natural, renewable and recyclable wood

†UNFAO, Global Forest Resources Assessment 2005-2015.
Two Sides is a global initiative promoting the responsible use of print and paper which, when sourced from certified or sustainably managed forests, is a uniquely powerful and natural communications medium.

There are some great reasons to #LovePaper Discover them now, two-sides.info

![](img/6866071e033820549b214c239744aaa0_68_0.png)

![](img/6866071e033820549b214c239744aaa0_68_1.png)

---

## Special Offer for Readers in North America

### 7 issues FREE

*When you subscribe*

![](img/6866071e033820549b214c239744aaa0_69_0.png)

![](img/6866071e033820549b214c239744aaa0_69_1.png)

**The open source authority for professionals and developers**

Order hotline **+44 (0)1795 418661**
Online at **www.imaginesubs.co.uk/lud**

This is a US subscription offer. You will actually be charged $97 sterling for an annual subscription. This is equivalent to $100 at the time of writing, exchange rate may vary. 7 free issues refers to the USA newstand price of $16 for 13 issues being $220.87, compared with $109 for a subscription. Your subscription starts from the next available issue and will run for 13 issues. This offer expires May 31 2017.

**Quote USA for this exclusive offer!**

---

## The Essential Guide for Coders & Makers

# PRACTICAL Raspberry Pi

72 “In a few simple steps you can configure your Pi to generate its own wireless Access Point and keep it permanently connected to a VPN”

### Contents

- 72 Automate your indoor garden
- 74 Get hands-on with the Pimoroni Blink!
- 76 Make a Raspberry Pi VPN Access Point
- 80 Anaconda for the Raspberry Pi

---

### OLED Display

All the monitoring of the Smart Plant is done centrally through the OLED display located at the top of the unit. It can be used for monitoring watering progress and all relevant sensor data which is automatically fed to it

### Sensor Package

It’s important to make sure all watering and monitoring is as precise as possible. To do this, the Smart Plant is equipped with an array of high-quality sensors which carefully pinpoint every part of the watering process, optimising it at every level

### Rotary Button

Controlling the watering levels in the Smart Plant is done through the rotary dial and push button. Values are switched through by rotating the knob in a clockwise direction and can be monitored using the OLED display above

### Measuring Air Quality

While the air quality sensor makes sure that the air being absorbed into the Smart Plant is of the best quality, it’s so powerful that it can actually pick up and locate pockets of substandard air throughout a much larger area

### Components List

- Pi2Grove board
- OLED display
- 4-channel ADC
- Rotary dial and switch
- Sensor pack
- Plastic piping and coating
- Cabling
- USB power control
- USB controlled pump

![](img/6866071e033820549b214c239744aaa0_71_0.png)

Above Amazon Echo owners can connect their unit to the Smart Plant and monitor progress using just their voice. A full setup tutorial will be available from switchDoc.com soon

Right The Grove push button is used as the central control for the SmartPlant. It works in tandem with the Pi for all core features and functions

![](img/6866071e033820549b214c239744aaa0_71_1.png)

---

## My Pi Project

### Automate Your Indoor Garden

John Shovic's indoor garden monitoring system is the perfect project for new and seasoned Pi makers alike

![](img/6866071e033820549b214c239744aaa0_72_0.png)

**We’ve seen some pretty unique projects using the Pi, but the Smart Plant is entirely different. How did the concept come about?**

The original SmartPlantPi idea came from a discussion in a local pub. We were brainstorming about what we could build with the amazing amount of environmental sensors out there (while staring at my beer) and I suggested that we build an automated plant-watering system for the Raspberry Pi. What made me think of that? I had been teaching a class at the local university, CS270 Systems Programming, in which I had Raspberry Pi computers for each student to take home and build projects.

Linux can be an intimidating study when you are down in the command line studying the kernel and the multitasking system. I decided to have the students do what I call “Physical Computing”, which is where we build sensor-based projects, like a sunlight analyser, and then use LEDs and other devices for the Raspberry Pi to interact with the environment.

**How long did it take you to go from concept to a fully made product? Did you encounter any issues during the build process?**

The development of the SmartPlantPi kit took about three months from (the) start to the finish of the project and kit documentation. The big choice we made in the hardware design was the decision to go with the Grove connector system. The Grove system is a standard plug used to connect a variety of small computer devices together. All told, there are about 200 different Grove sensors out there, from a number of different manufacturers. All of the Grove connectors are the same size and have four wires but come in four flavours: FC, Digital, Analog and Serial. Going with an all-Grove design means there is absolutely no soldering required for SmartPlantPi, which makes the project much more accessible for all levels of makers.

**For those who may be unaware of the SmartPlantPi, could you give them an overview of what the project is?**

SmartPlantPi (or Smart Plant for short) is an introductory, easy-to-build Raspberry Pi-based environmental monitoring and plant watering system using advanced sensors to monitor the soil moisture, monitor the sunlight, watch the air quality and monitor temperature and humidity. It is designed to be easy and simply put together and tested with no soldering required. Smart Plant also comes with a USB-controlled pump, water flow sensor, plastic tubing for the water, and buttons for control.

**Would you say the focus of this project is on education? Can adults benefit from it as well?**

Well, everything we build for the maker market is designed for education and learning. Making is education. Making is learning. Building your own projects allows you to innovate around a framework and do wonderful things that we have never thought of.

> “Making is learning. Building your own projects allows you to innovate”

The educational goals for Smart Plant are:

- Learn about the Raspberry Pi and installing software on the Pi
- Connecting up sensors to the Raspberry Pi
- Learning about feedback loops and regulating water to plants
- Understand your indoor environment and what affects it
- Learn about the new technology called the Internet of Things

**What sort of role does the Raspberry Pi play here?**

The Raspberry Pi is the key component of the system. It is the brain. We could have designed this using a much simpler computer, such as an Arduino, but we wanted to provide the power of the Pi and Linux to allow the Smart Plant to be connected up to the Internet of Things and Alexa. To do that, we needed computing power, and the Raspberry Pi provides all of that in a single inexpensive project.

**We’ve seen mentions of multiple sensors being bundled in with the Smart Plant Pi, what do they bring to this project?**

The sensor package provides a whole indoor environmental monitoring system. Temperature, Humidity, Sunlight, UV Index, and one very cool sensor: the Air Quality Sensor. We were amazed at how sensitive this inexpensive sensor was. We could detect all sorts of events in the entire house. One thing to point out is that virtually all of the time the sensor was under 3200 (rated fresh air) and the average was 2727 across the entire period.

**Are people able to track the progress of their plant at all?**

Absolutely, there are a couple of ways. The first is with the built-in OLED display. It displays status and also flashes alarms when detected. Secondly, we can monitor your plant on the internet by using PubNub and Freeboard.io (a tutorial on how to do that is part of the SmartPlantPi documentation). Here is a live link to our demo plant: freeboard.io/board/BhKt4Y

**How have you found working with the Raspberry Pi in this project? Would you use it for other projects in the future?**

The Raspberry Pi in this project is the best and most capable platform for designing projects and prototyping products. We can build projects that can do amazing things and make use of the thousands of software packages and sensors available for the Raspberry Pi.

**What is our next Raspberry Pi Kickstarter? We are building a board that will allow the maker to experiment with artificial intelligence on the Raspberry Pi with some neural network hardware assists. Can you just imagine what we can build with that? Technology doesn't just have to be the domain of the technologists. We all can be part of this future. Learn. Make. Repeat.**

![](img/6866071e033820549b214c239744aaa0_72_1.png)

**John Shovic**
has spent over 30 years in hardware engineering, and is a proud author of over 50 papers, including coverage of Arduino and the Raspberry Pi.

**Like it?**
You can boost a pretty incredible portfolio of work, much of which he goes into detail in over on his site at switchdoc.com. Make sure you take a look at the site's tutorial section, which is packed with tips and tricks for beginner and advanced Pi projects alike.

**Further reading**
The entire process of the SmartPlantPi is fairly complex, and if our brief overview here hasn't enough, then make sure you head across to the switchdoc.com website where a full rundown is available.
