
# Bodhi Linux in 24 Hours

Patrick Valtin

**EX-LIBRIS**

![](img/aa479e16c3ea23572f6197ce6302aaf6_1_0.png)

RONALD A. JAVITCH
RARE BOOK COLLECTION.

Copyright 2014 IT Researches
Amazon.com
Bought From Internet
June 2014

## Table of Contents

- **1 Introduction**
  - 1.1 About this guide
  - 1.2 What is Bodhi Linux?
  - 1.3 What you need to know about Bodhi Linux before you begin
  - 1.4 Installing Bodhi Linux
- **2 First steps with Bodhi**
  - 2.1 Preliminary housekeeping tasks
  - 2.2 Some initial tweaks
  - 2.3 Installing some applications: Firefox and Flash
  - 2.4 Installing Nautilus and Gnome Terminal
  - 2.5 Application Launchers
  - 2.6 Using Nautilus and Gnome Terminal
  - 2.7 Running Nautilus as Superuser
  - 2.8 Customizing the Nautilus Icon
  - 2.9 Hidden files
- **3 Turbocharge your Desktop**
  - 3.1 A first look at shelves and iBars
  - 3.2 Hiding desktop launchers
  - 3.3 A second shelf
  - 3.4 A popup shelf
  - 3.5 The Places gadget
  - 3.6 Run Everything
  - 3.7 Edge bindings
  - 3.8 Key bindings
- **4 Beef up your System**
  - 4.1 Office applications
  - 4.2 Media players
  - 4.3 Photo applications
  - 4.4 Dropbox
  - 4.5 Osmo personal organizer
  - 4.6 Skype
  - 4.7 Osmo Audio Recorder
  - 4.8 elDeb and Chrome
  - 4.9 Get-iPlayer
  - 4.10 Other applications
  - 4.11 Uninstalling applications
- **5 More power to your desktop**
  - 5.1 Update your iBar
  - 5.2 An iBar on the desktop
  - 5.3 The Favorites menu
  - 5.4 Applications name display
  - 5.5 Startup applications
  - 5.6 Virtual desktops
  - 5.7 Different shelves for different desktops
  - 5.8 GTK Themes
  - 5.9 Profiles
  - 5.10 E17 themes
  - 5.11 Starting afresh
- **6 Maintain and replicate your system**
  - 6.1 Aliases
  - 6.2 Updating your system
  - 6.3 Cleaning your system
  - 6.4 Backing up with Remastersys
  - 6.5 Unetbootin
  - 6.6 Running Bodhi Linux from a USB drive
  - 6.7 Future versions of Bodhi Linux
  - 6.8 Conclusion
- Quick Start Guide to this Bodhi Linux installation

# 1 Introduction

## 1.1 About this guide

This guide describes how to install the Bodhi Linux operating system on your computer, how to customize it, and how to install the software applications you will want to use (web browser, email client, office applications, photo software, media player, etc). It is a practical step-by-step guide rather than an academic description of the Bodhi system, but at relevant points it will give links to explanatory material on the web.

It grew out of notes prepared for a University of the Third Age (U3A) computer group in the UK, some of whose members wished to migrate to Linux from Windows following Microsoft’s decision to cease supporting Windows XP. I hope, though, that it will prove useful to a wider audience, including existing Linux users who are coming to Bodhi for the first time.

Bodhi Linux is highly customizable and can be tweaked in numerous ways. However, a step-by-step guide such as this is necessarily prescriptive, so that by following it you end up with a very specific desktop profile. Don’t worry about that. The point is that having learnt how to create and save that profile, you are then in a position to set up your own profile, either by playing around with what you’ve already produced or by starting a fresh. And if you mess things up you can easily restore your saved profile. And as for the various applications that you will be installing as you work through this guide, they can be easily removed and replaced with alternatives.

I should emphasize that this is not an official Bodhi Linux publication, and that I have no connection of any kind with the Bodhi Linux developers. Like Bodhi itself (and indeed most Linux products), it is given away free of charge. However, if you find it helpful and, more importantly, if you like Bodhi and continue to use it, I would encourage you to make a donation to Bodhi Linux to support its further development. The donate link is on the Bodhi Linux home page at www.bodhilinux.com.

## 1.2 What is Bodhi Linux?

Bodhi (rhymes with Jodie) is what’s known as a Linux distribution or ‘distro’, meaning a variant of Linux packaged with a window manager or desktop. All variants of Linux are built on the same essential Linux ‘kernel’, so they all share a common core. Probably the most popular variant is Ubuntu, and it is from this that Bodhi Linux is derived. There are a number of different desktops (i.e. window managers with added extras) that are available for Linux, and the one that is packaged with the standard Ubuntu distro is called Unity. Bodhi Linux, however, uses instead the Enlightenment window manager, or E17 for short (17 being its current version number).

Enlightenment can be used with other distros, and it has become a firm favourite with many Linux users (including, obviously, me), as it is agile, elegant, and very customizable.

However, it is only Bodhi Linux that puts Enlightenment at the heart of its design philosophy. Enlightenment's disadvantage is that it is so customizable that the user is faced with quite a learning curve, but Bodhi's Help system - 'Tibodhi Guide to Enlightenment' - provides excellent guidance. And hopefully this step-by-step guide will enable you get to grips with it.

Although Bodhi is based on and is very close to Ubuntu, it is not Ubuntu. In particular, it does not have the same software repository. Again, its repository is based on the Ubuntu repository, but it is kept more up-to-date, meaning that the Bodhi developers try to provide the latest releases of the various software applications that you are going to want to install.

Bodhi Linux is currently at version 2, the latest release being 2.4.

**Further reading:** If you want to read a little more about Bodhi and its Enlightenment window manager, go to the introductory section of the Bodhi Guide. You can find it at the Bodhi website (www.bodhilinux.com) - at the home page, move the mouse pointer over 'Documentation', choose 'Enlightenment Guide', then 'Introduction'.

## 1.3 What you need to know about Bodhi Linux before you begin

Fortunately, you don't need to know much about Linux itself in order to use Bodhi and its Enlightenment desktop, and what you do need to know can be picked up along the way. However, there are a couple of concepts used by Enlightenment that I need to introduce you to right now. These are 'E17 Themes' and 'Profiles'. I mention them here because you will meet them while you are installing Bodhi on your computer.

- **E17 Themes:** These control the appearance of the desktop, including the background, the fonts, and the various gadgets such as the clock. For examples of some of the themes that are available, go to the Bodhi website (http://www.bodhilinux.com/), mouse over 'Resources', choose 'Art Wiki', then choose 'Enlightenment'.

- **Profiles:** These control everything about the desktop, including the theme you have chosen, the positioning of its elements, what modules are loaded, and any key bindings and mouse bindings that you may have set. Profiles are very powerful because they store all your customizations, it means that you can try different profiles, with different themes and customizations, secure in the knowledge that you can at any time return to your original saved profile. Bodhi comes with a number of standard profiles from which you can choose, to suit your particular hardware and preferences.

- **GTK Themes:** Also called 'themes', these are not part of Enlightenment, but I mention them here so that you don't confuse them later with E17 themes. GTK themes control the appearance of the windows within applications run, i.e. their colour schemes and the look of common elements such as scroll bars. For examples, go to the Art Wiki on the Bodhi website and choose GTK themes.

**Note:** I won't be cluttering up this guide with explanations of terms such as GTK. If you would like to know what they mean, search the web, if necessary including 'linux' or 'ubuntu' in your search phrase.
