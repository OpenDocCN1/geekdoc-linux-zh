
It’s got good future proof qualities, with support for new DDR4 RAM and a powerful integrated Intel HD Graphics 530 GPU. Without a dedicated graphics card, the Intel Core i7-6700K reached an average of 79 frames per second (fps), with a minimum fps of 5.6 in the Heaven benchmark. In comparison with a GTX 950 GPU installed, the Heaven reached an average of 39fps and a minimum of 20.4fps.

We also benchmarked the GTX 950 in Metro Last Light, a graphically demanding first person shooting game that was the first AAA game to be available for Linux. At full 1080p resolution the GTX 950 hovered around the 50 frames per second mark for most of the run, offering a smooth gameplay experience. However, we found there were sudden drops to 36fps when things got busy – though the graphics settings were set to maximum.

If you want a more consistent framerate then you can lower some of the graphical details, and it will still look lovely. It’s certainly better than the integrated graphics that is on the Intel Core i7-6700K, which only managed 21fps in Metro Last Light – and that was while running the game at the lowest graphical settings, too.

## Installing a GPU
It’s clear, then, that if you want to play graphically demanding big budget games, a dedicated graphics card is a must-have on your shopping list. Graphics cards are relatively straightforward to install. All you need to do is turn off your machine and pop off the side to get to your motherboard. The graphics card slots into the primary PCIe slot - check your motherboard’s manual (or run a quick online search if you’re not sure, though most motherboards are clearly labelled up).

Allianware is just one of the big names to get into the Steam Box business.

One of the best things about putting together a PC is that it’s pretty hard to plug something into the wrong port or slot – they simply won’t fit. The PCIe slots have a little lever at one end of them, and pressing these down helps to eject the graphics card if you want to remove or replace it, so when installing you might have to angle the card so that the small cut out in the card fits under the lever. You’ll also have to make sure that there’s a gap in the chassis of your PC to allow you to reach the ports of the graphics card when it’s installed. To create a gap most chassis allow you to unscrew a thin metal grille to give access to the card’s ports. Find the grille that aligns with the PCIe slot you’re going to be installing the card in, and use a screwdriver to unscrew the screws holding it in place – but make sure you keep hold of the screws. Remove the grille cover and then insert your graphics card into the PCIe slot. Now use the screws that you kept hold of and use them to secure the graphics card in place. Many graphics cards – especially the more powerful ones – require that they are plugged in to your computer’s PSU (power supply unit), so check to see if the card has one or even two of these PCIe six- and eight-pin sockets. Your PSU should have a cable running from it with matching connectors. If not, Molex adaptors should be provided with the card, however any good 500W PSU should provide at least one of these and we’d recommend upgrading if yours does not. You can now close up your PC and attach your monitor to your graphics card and power it on. All going well, your PC should boot and you’ll see the desktop environment of the distro that you are running. Steam, which has the biggest collection of Linux games runs on Debian-based systems, though only Ubuntu with Unity, GNOME or the KDE desktop are officially supported. We have run Steam on other Debian-based distros, Mageia and Arch with success, but for the ease of this feature we are running the latest version of Ubuntu.

Because of the growing number of Linux gamers both Canonical and Nvidia have worked together to make installing graphics drivers a lot easier. When Ubuntu is loaded you should see a message pop up saying that ‘Restricted drivers are available’. Click this message and a window will open up listing a range of drivers that you can install. A recommended driver for your system will be highlighted, but it’s worth checking some of the drivers as there will be information regarding whether the drivers are proprietary or open source. You can also install drivers from the terminal. Open it up and type `sudo ubuntu-drivers devices`.

This gives you a list of possible drivers, eg for an Nvidia graphics card it could list:
- `driver : xserver-xorg-video-nouveau - distro free builtin`
- `driver : nvidia-304 - distro non-free`
- `driver : nvidia-331 - distro non-free recommended`

If we wanted to install the latest official proprietary driver from Nvidia – which Ubuntu recommends – then we would then type: `sudo apt-get install nvidia-331` to install. You may notice this isn’t the bleeding edge proprietary driver from Nvidia, but it will likely run most indie games. For more graphically demanding games, such as *Middle-earth: Shadow of Mordor*, you’ll need a more recent driver. In the past, this has meant either downloading and installing a driver manually from the Nvidia – which is probably too much *Terminal* exposure for most newcomers – or adding and enabling extra repositories (repos) to stay up to date. The latter option used to mean relying on third-party repos (eg ppa:pasabuntu-x-swat/x-updates for the latest stable), but in an exciting and recent development Ubuntu has set up an official PPA especially for Linux gamers wanting the latest drivers. To fetch them, add and enable the PPA using:
`$ sudo add-apt-repository ppa:graphics-drivers/ppa`
`sudo apt-get update`

To upgrade to or install the latest driver use `sudo apt-get install nvidia-current`. If you’re concerned about these drivers making your system bled – most newly released Nvidia drivers can tend to have their teething problems – then we’d advise sticking to the x-swat PPA. To roll back changes made by the PPA use `sudo ppa-purge ppa_name`.

If you have an AMD graphics card and want to install the latest official drivers then you can download and install the AMD Catalyst program which gives an easy-to-use graphical interface for installing the latest drivers. If you have previously installed an AMD card you’ll need to remove the old drivers by opening up the terminal and type in `sudo aticonfig --uninstall`. Now enter `sudo /amd-driver-installer-x86.x86.x86_64.run` in the Terminal. Where it says ‘amd-driver-installer-x86.x86.x86_64.run’ you’ll want to double check that it’s the most recent driver for your card on AMD’s website ([http://support.amd.com](http://support.amd.com)). A window will open allowing you to complete the installation. A word of warning, before updating the kernel down the line, remember to remove the proprietary driver.

## Game services
Now that your Linux machine is ready to play games the big question is where can you get games to play? Steam is the obvious choice as it has a huge collection with a decent mix of genres and game types. It also features some fairly features such cross play, so you can buy a Linux game, and if it’s compatible with Windows or Mac, you can play it on those OSes as well without having to pay for another copy. Many games on Steam also support cloud saves for you saving your progress on one machine and switching to another and carry on playing where you left off.

To install Steam in Ubuntu you can either search for it in the Software Center or open up the terminal and type `sudo apt-get update` and then `sudo apt-get install steam` to install Steam. Once installed you will need to sign in with – or sign up for – a Steam account. After that buying, downloading and installing games through Steam is a piece of cake.

Good Old Games is another great service that’s now supporting Linux. Although it’s not quite as straightforward as buying through Steam, its GoG Galaxy application takes plenty of cues from the Steam client (but isn’t currently available for Linux, you have to use the launcher), but it does come with its own pros, such as it only sells DRM-free games and it guarantees games to run on supported platforms or your money back. Also, as you can probably guess from the name, it started out specialising in old games, repackaging them so that they work on new hardware and OSes. Of course, it can also features new games as well, and you can view and download games from [www.gog.com](http://www.gog.com).

We’d normally recommend taking a look at Desura, too ([www.desura.com](http://www.desura.com)), which has a host of Linux indie games – both free and paid-for – but Desura’s parent company filed for bankruptcy in June, and aside from Humble Bundle offering its assistance ([www.humblebundle.com](http://www.humblebundle.com)), and another great source of Linux games, there’s been no official word on its future yet. The site is still up so the choice to buy is your own. Regardless of the game service you decide to use, you should now have a Linux machine that’s fully ready to play the latest and greatest games.

## Fun Gaming

![](img/420a7272a6efa239082a35eeadd9bc1d_76_0.png)

The **Additional Drivers** system in Ubuntu makes it straightforward to install new open source or proprietary graphics drivers.

![](img/420a7272a6efa239082a35eeadd9bc1d_76_1.png)

The Nvidia **GTX 950** is a very good graphics card for its price, though if you want a bit more oomph you’ll need to spend a little extra.

![](img/420a7272a6efa239082a35eeadd9bc1d_76_2.png)

You need to sign up for a free Steam account to log into the service.

> If you want to play big budget games, a dedicated graphics card is a must-buy.

### Steam machines

Valve, the company behind the Steam platform, has been promising to disrupt the way we play games in our living rooms with Steam Machines. These are compact gaming PCs designed to replace gaming consoles, such as Xbox One and PlayStation 4. Running SteamOS, Valve’s Debian-based distro, the first commercially available boxes should go on sale in November – hopefully by the time you read this magazine. Steam Machines are being made by a variety of manufacturers, such as Asus and Alienware, and come in all different shapes and sizes. This means that if you don’t want to build a gaming machine yourself, you should be able to find one that suits your needs – and budget. Prices start from $449 (around £292 – roughly the cost of a PlayStation 4 but with a heck of a lot more power) to a wallet numbering $4,999 (around £3,256) for Falcon Northwest’s Tiki with its granite base. You can find out more about Steam Machines and purchase them from Valve’s own Steam website at http://store.steampowered.com/ sale/steam_machines. If you’d prefer to play your games with a controller rather than a keyboard and mouse, then many USB controllers will work plug-and-play with Linux and SteamOS, even Microsoft’s Xbox 360 controller. Valve has also created its own Steam Controller ($40), with the unique device supposedly making it easy to control games that usually use mouse and keyboard controls with the gamepad.
