
## VLC

Pop!_OS does not include any powerful media player. If you will ever encounter various audio and video files, I highly recommend installing VLC from Pop!_Shop.

## Office

Pop!_OS includes the LibreOffice suite of applications for word processing, spreadsheets, and presentations. However, I prefer ONLYOFFICE for this purpose. It can safely be installed from Pop!_Shop.

## BleachBit Cleaner

After some time, your Linux device will likely become saturated with old cache files, leftover data, and other unnecessary files. I recommend executing BleachBit once weekly to keep things under control. I prefer the BleachBit (as root) option within the Pop!_Shop (Flatpak). I accept the default configuration upon first launch. I then select every option except "Free Disk Space" and click "Clean". At this point in the book, while working from a new machine, I was able to free 1.02 GB of data.

## Utilities

I prefer to add a few system utilities to any Linux distribution including GNOME Feeds for RSS, GNOME Podcasts for podcasts, and Metadata Cleaner to sanitize personal information from within files. All of these can be installed from within the Pop!_Shop with the default options. For Metadata Cleaner to function, you also need a utility called mat2, which can be installed via Terminal with the following.

```
sudo apt install mat2 -y
```

After a reboot, you can right-click on any image, video, or other file which may contain hidden metadata and clean the content. This will produce a second file next to the original with "clean" added to the file name.

## Virtual Currencies

If you need virtual currency access, I always recommend an offline software-based wallet without the need for a third-party exchange. I rely on Electrum for Bitcoin and Monero GUI Wallet for Monero. While you may find these programs within Pop!_Shop or another software repository, I would only install them directly from their original source. I obtain the AppImage file from the official Electrum site located at https://electrum.org/#download and then right-click the file to install it with AppImageLauncher. I then download the compressed Linux 64-bit file from the official site at https://web.getmonero.org/downloads, decompress it, and then right-click the Monero AppImage file to finish the installation process.

## Application Updates

You should keep your newly-installed software updated. The "Installed" tab within Pop!_Shop will allow you to patch your operating system and any Flatpak/Deb programs, but it does not update all individual applications. I keep the following commands digitally ready within my local notes application for easy copying and pasting, but a future chapter will present a custom script which will automatically execute all of these commands.

```
sudo apt update
sudo apt upgrade -y
sudo apt full-upgrade -y
pop-upgrade release upgrade
sudo apt autoremove -y
sudo apt autoclean -y
flatpak update -y
```

You should now possess a Linux computer which is stable, secure, private, updated, cleaned, and includes the basic applications for daily use. There is still much more to be done, but you have the **steps** completed. When we create our custom maintenance script later in the book, we will add even more commands to make sure we are keeping our system tidy.

While most people rely on the providers of these applications to store encrypted data, extreme privacy enthusiasts might consider self-hosting as an option. This topic exceeds the scope of this guide, but there is plentiful information available online which could assist in self-hosting Bitwarden, EteSync, Standard Notes, and others. Next, we must tackle the most important program on our system: the web browser.

## DNS Entries

This would be a good time to revisit your NextDNS portal and check your logs. I like to launch every program once and then shut it down, then see what types of connections were made within NextDNS. The damage on my machine was fairly minimal, as seen in the following image (top). Thunderbird was the worst offender because it synchronizes with their own server. This is not malicious, but you could block these requests if desired. Standard Notes connects to its own server for data synchronization, so no harm there. If you were uncomfortable with ONLYOFFICE sending any data back to its servers, you could block the entire domain within NextDNS. That would allow complete offline usage of the program. I made this change (second image) and the connection was blocked on the next launch (third image).

![](img/451a8c416cafc58e46802d06b4bc7b1a_32_0.png)

![](img/451a8c416cafc58e46802d06b4bc7b1a_33_0.png)

Next, we must consider proper web browser configuration and usage.

# CHAPTER SIX: WEB BROWSERS

Before we consider connecting to various websites in order to take full advantage of our new Linux build, we should properly configure our web browsers. I recommend the Firefox web browser for most daily browsing, with limited use of other browsers for specific tasks. Firefox is already included with most Linux distributions, and the default Pop!_OS installation of Firefox is **preferred** for our needs. Launch Firefox and consider the following modifications.

- Click on the Firefox menu in the upper right and select "Settings".
- In the "General" options, uncheck "Recommend extensions as you browse" and "Recommend features as you browse". This prevents some internet usage information from being sent to Firefox.
- In the "Home" options, change "Homepage and new windows" and "New tabs" to "Blank page". This prevents Firefox from loading their default page.
- Disable all "Firefox Home Content" options.
- In the Search options, change the default search engine to DuckDuckGo and uncheck all options under "Provide search suggestions". This prevents queries from going directly to Google, and blocks the Google API from offering search suggestions.
- Click the "Privacy & Security" menu option and select "Strict" protection.
- Check the box titled "Delete cookies and site data when Firefox is closed".
- Uncheck the box titled "Show alerts about passwords for breached websites".
- Uncheck the box titled "Suggest and generate strong passwords".
- Uncheck the box titled "Autofill logins and passwords".
- Uncheck the box titled "Ask to save logins and passwords for websites".
- Uncheck the box titled "Autofill addresses".
- Uncheck the box titled "Autofill credit cards".
- Change the History setting to "Firefox will use custom settings for history".
- Uncheck "Remember browsing and download history" and "Remember search and form history".
- Check the box titled "Clear history when Firefox closes". Do not check the box titled "Always use private browsing mode", as this will break Firefox Containers.
- Uncheck "Browsing history" from the "Address Bar" menu.
- In the Permissions menu, click "Settings" next to Location, Camera, Notifications, and Virtual Reality. Check the box titled "Block new requests..." on each of these options. If you will never need audio communications within this browser, you could do the same for Microphone.
- Uncheck all options under "Firefox Data Collection and Use".
- Uncheck all options under "Deceptive Content and Dangerous Software Protection". This will prevent Firefox from sharing potential malicious site visits with third-party services.
- Select "Enable HTTPS-Only Mode in all windows".

These settings are what I refer to as the basics, and may be enough for most readers. This is where I want to deviate from previous writings. Prior to this publication, I always presented several settings which could be modified within the Firefox "about:config" menu. I no longer recommend this, which may upset some privacy fanatics. Please consider my reasons before abandoning this chapter. The purpose of my previous recommendations was mostly to prevent browser fingerprinting or canvasing. This activity is often abused by online sites which try to track you as you navigate the internet. If I own a clothing website and I can collect numerous identifiers from your browser, you are unique from everyone else who has ever visited my site. When you come back a week later, I know you are the same user, and I can continue to track your activity within my site.

Previously, I had recommended readers change various settings, such as the ability for a website to know your current battery level, in order to make you appear less unique to the malicious systems snooping on your connection. Today, thanks to advancements in fingerprinting technology, I believe those settings could do more harm than good. If you are the only visitor on that site which disabled this setting, you now appear even more unique than if you had done nothing.

At the risk of offending some readers, I firmly believe the following statement. We can no longer defeat modern browser fingerprinting by making modifications to our browsers. Anything we change, or any extension we add, almost always makes us a unique visitor in the eyes of sophisticated fingerprinting systems. The more actions you take to blend into the crowd likely makes you stick out more. There are exceptions to this, but for general usage, sites will continue to track us. They will also collect our IP addresses, installed fonts, video characteristics, location metrics, and browser specifications at all times. That will never change.

Furthermore, many of the current recommended about:config Firefox privacy tweaks break other desired functions. If you try to block all possible IP address leakage via WebRTC, you will likely also break the ability to use voice and video conferencing within your browser. There must be a balance of protections versus functionality.

Using a VPN, as explained later, and the previous Firefox settings stop most invasions. Since Firefox does not share cookies from one domain with another, we have strong privacy by default. If you want pure anonymity, stay off the internet. If you need the most protection possible, consider the Tor Browser, as explained later.

Next, I will discuss the abundance of helpful browser extensions called add-ons.

The first vital add-on I install on every computer is uBlock Origin. It blocks many ads and tracking scripts by default, but it also can block any other type of script that is attempting to run on a page. This helps prevent tracking, malicious code execution, location sharing, and a number of other processes that could undermine your privacy and security.

This add-on is completely free and open source. It is highly customizable, while remaining relatively easy to work with. uBlock Origin works from blacklists which block trackers specified in the list(s). The add-on comes with several lists enabled, but there are several more that can be added through simple checkboxes in the preferences. Keep in mind that the more blacklists you enable, it may be more difficult to work within the browser. This section may seem a bit overwhelming at first, but experimenting with the advanced settings should help you understand the functionality.

I have previously recommended NoScript, Adblock Plus, Privacy Badger, and Disconnect as privacy add-ons that would help stop unwanted ads, tracking, and analytics. These are no longer present on any of my systems. I now only use uBlock Origin, as it replaces all of these options. Let's start with the basics.
