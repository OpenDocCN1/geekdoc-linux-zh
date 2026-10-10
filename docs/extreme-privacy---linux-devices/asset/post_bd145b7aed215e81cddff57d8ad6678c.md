
# CHAPTER ONE: WHY LINUX?

I mentioned in the introduction that Windows and macOS machines collect and store data about your usage of their products. Let's dive deeper into that. In 2019, I requested all of the data stored about me from Apple. I was preparing to record a podcast about the data which Apple collects about all of us, and I wanted to see the damage first-hand. I possessed several Apple ID accounts in alias names, so I requested the data from each of them. Since I never gave Apple my true name, I assumed the exposure was no big deal. I was wrong. The data provided by Apple confirmed they knew the following about my "anonymous" Apple accounts:

- My full alias name and email address provided during account creation
- My alias physical address provided during account creation
- The serial numbers for all devices
- The dates I first used the email addresses with Apple
- Multiple IP addresses possessed during use of the devices
- The internal computer names assigned to all devices
- The dates/times of any reformatting of the systems
- The dates/times and IP address of last access to iTunes, FaceTime, and iCloud
- My time zones during usage of the devices
- The VoIP telephone number provided during Apple account logins
- An alternative email address I once entered into Apple Mail
- Songs I had listened to through the official Apple Music application
- The moments within the songs when I paused the playback
- My IP addresses during media streaming from Apple's servers
- My preferred musical artists identified during their onboarding process
- The serial number of an iPhone which I had accessed in 2017
- All podcasts subscribed to through iOS devices
- Titles of podcast episodes which had been completed or paused (hundreds)
- Dates of podcast subscriptions and listening times
- Podcasts which possessed reviews from me, including full review text
- All app purchases, including free apps, downloaded to the device
- All IP addresses assigned during downloads
- All books downloaded through Apple Books
- Hundreds of IP addresses used during my connections
- An export of all entries from Apple Calendar
- Documents and contacts remaining in iCloud
- Auto-stored contacts from Apple Mail
- Recipient email addresses accessed within Apple Mail
- Dates and times of outgoing email
- **My real name extracted from outgoing email headers**

I remind you that this data was all monitored, collected, and stored while I assumed I was being anonymous. There simply is no anonymity with Apple devices, as the digital trail will eventually identify any user. If you have followed my digital guide *Extreme Privacy: macOS Devices*, you know we can block almost all of this telemetry, but it can be a chore to maintain. I believe we should not need to take such extreme measures to prevent companies from this invasion.

Microsoft is no better. By default, Windows 10 and 11 require a Microsoft online account in order to install the operating system. Some versions allow you to bypass account creation altogether by being offline, but Microsoft is pushing to eliminate this option in Windows 11. An active Microsoft account is not required in order to receive important software updates, but Microsoft's Telemetry service continuously collects the following data, plus numerous additional details, sending it to their corporate servers in Seattle:

- Typing diagnostic data from your keyboard
- Microphone transmissions
- Index of all media files on your computer
- Webcam data
- Browsing history
- Search history
- Location activity
- Health activity collected by HealthVault, Microsoft Band, and other trackers
- Privacy settings across the Microsoft application ecosystem

This data would make it very easy to identify you, your location, and all online activity. Microsoft claims this collection of data is only to enhance your experience, but I find this activity to be invasive and unnecessary. This is where Linux comes in. Consider the following summary of the benefits of Linux over Windows and macOS systems:

- Linux operating systems do not require an account for installation or usage. You will not be asked for a name, email address, physical address, telephone number, username, or credit card just to use the system which you purchased.
- Most flavors of Linux possess either no telemetry or minimal data collection, which can be easily disabled. Unlike macOS, there are no account requirements in order to download official software. This alone is a huge privacy benefit.
- I believe the security of Linux systems is much better than Microsoft Windows. Most malicious software targets Windows systems due to the abundance of Windows users in both personal and professional spaces, but also because of the overall ability for programs to access system resources. There are viruses and other malicious programs which target Linux and macOS, but these are fairly rare. Any time you hear about a machine becoming infected with ransomware or other computer viruses, it is almost certain to have involved a Windows system. While I believe macOS systems are more secure than Linux or Windows, the privacy invasions negate many of the benefits.
- Linux is completely free and open source. This means that all Linux operating systems are transparent and can be audited by anyone. There are many active Linux communities which pour over all of the code to make sure nothing nefarious is going on behind the scenes. Microsoft and Apple hide their code from the public view and we never truly know just how bad things might be. Open-source code also allows people to create many different versions of Linux which can accommodate specific needs and niches. We will soon discuss the many flavors of Linux and which of them might be most appropriate for your needs.
- Almost every aspect of Linux can be modified and customized. If you are a macOS user, you know that you cannot uninstall stock Apple software such as Mail, Photos, Facetime, Music, and other undesired applications. You are stuck with them. Most Linux systems begin with minimal programs and allow you to choose what should be added. You can remove anything desired and are never stuck with a default list of stock apps.
- Linux is a very lightweight operating system. It runs smoothly on modern and legacy hardware, which allows for easy testing without the purchase of new and expensive machines.
- Since Linux can be installed on practically any computer hardware, we can be very selective about each part. Most Linux machines allow you to modify all parts including batteries, RAM, drives, etc. If you purchase a MacBook Pro and later decide to upgrade any of these specifications, you are likely out of luck. You would have to buy a whole new machine.

I could provide many more additional reasons I prefer Linux over more traditional systems, but I believe the previous points suffice for most people. Instead of trying to convince you to give Linux a shot, I prefer to explain the ways in which I customize my own Linux usage, and the process for clients. I believe by the end of this guide you will be ready to build or purchase your own Linux device. Next, let’s tackle hardware choices, which can be overwhelming.

# CHAPTER TWO: HARDWARE CONFIGURATION

If you are a macOS user, you are limited to specific hardware approved and sold by Apple. If you want a laptop, you have a handful of options which can be minimally optimized. Linux is a different beast. Since it runs on practically any computer hardware, the options are endless. You likely possess an old computer which is capable of running Linux without much effort or commitment. If not, you probably have a macOS or Windows device which could host a Linux virtual machine. If you decide to purchase a new computer specifically designed for Linux, you have a new set of overwhelming choices. Let's make sense of all of these options.

### Used Equipment
One of the best ways to test Linux is to install it onto a retired machine. If your computer is capable of running Windows, it will likely also handle Linux. If you possess an Apple computer, things are not as straight forward. Older Apple computers made before 2016 should handle just about any Linux variation. If you have a newer Intel-based laptop with a touch bar, you will need a special variant of Linux available from t2linux.org. If your device was made after 2020 and has the latest Apple processor, I do not recommend attempting a Linux installation. Everything else should be possible. I keep old laptops specifically for testing new Linux builds.

### Virtual Machines
If you only have one computer, then a Linux virtual machine is ideal for experimentation. Chapter Eight goes into great detail about creating virtual machines within any Linux, macOS, or Windows platform. It also explains how to build Linux and Windows virtual machines within your Linux host. Once created, your virtual machine will behave just like a traditional installation on a host.

### New Computers
This is always my preference. If you decide to commit to a Linux lifestyle, purchasing a dedicated Linux machine with your own specifications is ideal. It also opens the flood gates with multiple manufacturers, models, and customizations. However, I will walk you through my preferred options. A new machine with Linux pre-installed is not only the easiest way to get going, it should offer the best possible integration into your daily activities. During the rest of this chapter, I will assume that you want to purchase a new computer specifically for your Linux experience. However, the next chapter explains how to install Linux within any capable device. For now, let's focus on hardware options.

There are thousands of new and used machines which could run Linux well. You might have a preference for Lenovo ThinkPad laptops, and you might want to stick with that which is familiar. Maybe you prefer Dell machines. Both Lenovo and Dell work great with Linux, but I believe we can do better. Let's start with the processor. The processor is the main chip which allows your computer to complete all of the functions and tasks which you tell it to do. It is the heart of a computer. It can also be the first vulnerability from an outside attack. Virtually every Intel processor made since 2008 possesses software known as the Intel Management Engine (Intel ME). It is a subsystem of proprietary firmware embedded directly onto the chip. It is a small operating system. Any traditional operating system installed to the computer, such as Linux, would have no control over Intel ME. The Intel ME software runs during boot, while the computer is running, and while it is asleep. As long as the chipset is supplied power, it even continues to run when the system is turned off.
