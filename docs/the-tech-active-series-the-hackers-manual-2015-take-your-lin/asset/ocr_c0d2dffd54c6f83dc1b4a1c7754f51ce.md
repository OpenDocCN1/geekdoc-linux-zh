might seem like a limitation but it really isn’t, thanks to the brilliant SoX sound exchange audio editor. We’ll use the nifty little tool to process any MP3 file irrespective of its encoding and convert it into the correct WAV file on-the-fly.

Begin by installing the audio editor and its dependencies with sudo apt-get install sox libsox-fmt-all. When it’s done, type in the following command, substituting "SomeSong.mp3" with the name of the MP3 file you wish to play:
sox -t mp3 SomeSong.mp3 -t wav -r 22050 -c 1 - | sudo /pfm - 101.2.
The first part of the command converts the MP3 file into a WAV file, changes its audio sampling rate to 22050 Hz and down-mixes the track to mono. The converted track is then sent to the standard output, denoted by the hyphen, and is then piped (|) into the standard input of the pfm command.
The only difference in the pfm command in the above example is that instead of specifying the name of the file to broadcast, we are asking the script to instead broadcast the standard input. If you’ve still got your FM receiver tuned to the 101.2 frequency, you should now hear your MP3.
You can do some wonderful things with SoX. You can, for example, use it to broadcast your favourite streams live from the Internet. The command sox -t mp3 http://www.tuxradar.com/files/podcast/tuxradar_506e02.mp3 -t wav -r 22050 -c 1 | sudo /pfm - 101.2 will broadcast the TuxRadar podcast. The only difference between this command and the previous example is that instead of pointing to a local MP3, you are now pointing to one that resides online.

script will download missing dependencies and then present a menu with a couple of options.

The first option downloads and installs precompiled binaries of all the popular supported platforms. The second grabs the newest source code for each app and compiles them on the Pi. If you choose this option, be prepared to wait as it might take almost an entire day. In case you aren’t this patient, you might as well grab the image file and transfer it on to a blank SD card with dd.

RetroPie uses a graphical front-end called EmulationStation, which allows you to manage the various installed emulators. The RetroPie image automatically starts this frontend, but if you’ve setup RetroPie on top of an existing Raspbian install, you’ll have to launch it manually with the emulationstation command.

Once it’s up you should see the controller setup screen, from where you can configure your USB gaming controller. In order to play the games, of course, you must first own them. ROMs can be made from your own copies of these old games, or you can find abandonware online. Some companies, such as id Software, have made the original Doom open source and public domain. Once obtained, you’ll need to copy them to their appropriate emulator sub-folder inside the roms/ folder on the SD card.

# Hack #7: Emulate vintage gaming

Games weren’t always graphical masterpieces. Their developers had fewer resources to play with and instead of graphical excellence the developers relied on gameplay to keep the players hooked. This is why the vintage games even with their rudimentary graphics are still quite popular with gamers of all ages even today – there’s nothing quite like A classic gaming challenge, even on Steam or Live.

The easiest way to start playing vintage games on the Raspberry Pi is to install RetroPie which packs a bundle of emulators. You can install RetroPie on an existing Raspbian install or run it as a standalone distro. Before you fetch the installation script, grab its dependencies with sudo apt-get install git dialog. Then you can download the latest RetroPie setup script with:
git clone git://github.com/petrockblog/RetroPie-Setup.git
Now change into the cloned directory and run the script with cd RetroPie-Setup && sudo ./retropie_setup.sh

> “In order to play emulated games, of course, you must first own them…”

![](bbox=[0.52, 0.55, 0.92, 0.72])

EmulationStation will only display the emulators that have ROMs added.

# Donate excess resources

If you aren’t always using your Pi, you can donate the idle processing power for a worthy cause. BOINC is a computing volunteering service and it uses the donated power for a variety of projects, from protein folding for medical sciences to the search for alien intelligence.

Before installing BOINC, tweak the Raspberry Pi to cut down its own resources utilisation by calling sudo raspi-config. Head to Advanced Options > Memory Split and earmark the least possible memory for the GPU which you should find is 16MB. Then install BOINC with sudo apt-get install boinc-manager boinc-client

When it’s done, launch the BOINC Manager from the Others menu. You’ll be asked to add from one of over 30 supported projects. Some projects might warn you that they might not have work suitable for the Pi. While you can still add them, it’s best to add projects that can make use of the Pi such as the Collatz project, which is attempting to disprove the Collatz Conjecture.

![](bbox=[0.62, 0.78, 0.92, 0.9])

To configure how BOINC uses the Pi’s resources, first enable the Advance View and then head to Tools > Computing preferences.