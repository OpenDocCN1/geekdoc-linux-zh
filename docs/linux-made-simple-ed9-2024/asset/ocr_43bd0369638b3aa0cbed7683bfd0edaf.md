# # Install apps in Mint
How to find and add new programs to your distro.

Now that you're up and running in Mint, you'll be wanting to start making productive use of it. That naturally involves running applications and utilities. Start by taking an inventory of the programs you use in Windows and checking the website for each to see if a Linux build is available. If there isn't one, don't panic — you'll find the vast majority of Windows applications have an equivalent version for Linux. Better still, many of these are both free and open source, so you won't need to splash out to use them, but do of course donate to them.

The most obvious place to start is your office suite. When it comes to replacing your word processor, spreadsheet, database and presentation tool, you'll find everything you need is already built into Mint via the free LibreOffice software, which can be found under Menu > Office.

If you're looking for a specific open-source alternative to your original proprietary program, start your search at **http://bit.ly/SoftwareEquivalents** where you'll find links to other useful resources such as **www.osalt.com**. If you still can't find anything suitable, try **http://alternativeto.net**.

The simplest way to obtain and install software in Mint is through the *Software Manager*. It offers a neat, user-friendly front-end for finding and installing programs. Programs are organised into 'repositories' (or repos) and if your target program isn't in the repos supported by the *Software Manager* you'll have to find alternative ways of getting them.

First, visit the program's home page – here you may be offered a convenient downloadable installer in the form of a

![](bbox=[0.55, 0.17, 0.92, 0.36])

> Manage all your repositories through the Software & Updates tool, which you'll find in System Settings.

Deb package – choose the 32-bit or 64-bit download (if offered) to match the version of Ubuntu you installed. Once downloaded, navigate to your Downloads folder, double-click the file and follow the prompts to install it.

Other programs may require you to install them through the Terminal. This usually involves first adding the program's repo using the following command:

`sudo add-apt-repository ppa:user/ppa-name`

The *ppa* stands for Personal Package Archive, which is a special software repo – generally focused on Ubuntu – that anyone, usually a software team, can establish for uploading source packages for anyone to download. Replace *ppauser/ppa-name* with the PPA provided by the software producer.

Once done, you can then install packages from that repo, either through *Software Manager* or – seeing as you're already in the Terminal – with the following command:

`sudo apt-get update 6.5 sudo apt-get install <program>`

Replace `<program>` with the name of your target program and it'll be downloaded and installed. Once added, you can view and manage all repos via System Settings > Software Sources.

# ## “You’ll find the vast majority of Windows applications have an equivalent version for Linux”

# ### Popular alternative applications

| **Windows app** | **Alternative** | **Where to get it** |
| :--- | :--- | :--- |
| Word, Excel, PowerPoint, Access | LibreOffice | Pre-installed |
| Publisher | Scrivbus | Software Manager (SM) |
| Photoshop | The GIMP | Pre-installed |
| Windows Movie Maker | OpenShot | Software Manager |
| Adobe Reader | Document Viewer | Pre-installed |
| iTunes | Amarok | Software Manager |
| Windows Media Player | VLC Media Player | Software Manager |
| Internet Explorer | Firefox, Chromium | Pre-installed or SM |
| Outlook/Windows Live Mail | Thunderbird, Evolution | Pre-installed or SM |
| Skype | Pidgin | Software Manager |

# ## Stay up to date

Programs you install through repos – either via the Terminal or *Software Manager* – are checked for updates on a regular basis, namely within 10 minutes of first booting up and then every two hours thereafter. That should be frequent enough for the vast majority of people, but you can check manually too using one of two methods. The first is done via Cinnamon: open Menu > Administration > Update Manager and click ‘Refresh’ to manually check here, and choose Edit > Preferences > Auto-Refresh to change the time between update checks (days, hours and minutes are supported).

To check for updates via the Terminal, type `sudo apt-get update` and hit Enter. You may find the application versions in the Software Center aren't as up to date as those provided on the program's website – by adding the relevant repos, you can ensure the latest version of the program is installed, and gain access to beta and other pre-release builds.