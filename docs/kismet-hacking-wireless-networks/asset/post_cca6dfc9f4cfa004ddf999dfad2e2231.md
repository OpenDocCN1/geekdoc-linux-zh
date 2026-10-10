
## Operating Kismet

Solutions in this chapter:

- Introduction
- The Kismet User Interface
- Additional RF Equipment: Antennas and Cables
- Using a Global Position System receiver with Kismet
- Putting It All Together: The Complete Kismet Setup
- Summary

### Introduction

In Chapter 2, our focus was to get Kismet installed and running in a minimal configuration. So far we have discussed the very basics needed to get it to operate on a laptop. Now, we are going to expand on that basic installation, and take the first steps to turning the Kismet laptop into a true wireless analysis tool.

Kismet has several configuration files that control its functions, most notably the `kismet_ui.conf` and `kismet.conf` files contained in the `/etc/kismet` directory. We briefly mentioned editing the `kismet.conf` file in Chapter 2. In order to make Kismet more functional, this time we’ll be performing editing to both the `kismet_ui.conf` and `kismet.conf` files to get Kismet running for everyday use.

The `kismet_ui.conf` and `kismet.conf` files are fully detailed in Chapters 5 and 6, but the changes noted in this chapter are those that are likely to be the most useful for those who are new to Kismet.

In addition to editing those files to make Kismet more functional and useful, we’ll also discuss adding several pieces of equipment that will help you get the most out of the computer that you are using to run Kismet. Many users have an expectation that they can immediately use Kismet with little more than a laptop and a wireless network card. However, to obtain the best possible results, most users quickly find that they must add some extra Radio Frequency (RF) equipment in the form of external antennas and associated cables, and a Global Positioning Satellite (GPS) receiver.

In addition to the GPS receiver, the `gpsd` software package will need to be added to the basic Kismet installation so that Kismet will work with the GPS receiver.

### The Kismet User Interface

The first thing we should do is edit the `kismet_ui.conf` file, which controls how the user interface presents itself to the user. The user interface is the client portion of Kismet that the user sees when running the application.

The `kismet_ui.conf` file is a simple text file that can be edited by any text editor. Two common text editors under Linux are `vi` and `nano`, which are used on the command-line interface (CLI). Most window managers that run under Linux, such as KDE and Gnome, also have graphic text editors that are suitable for editing `kismet_ui.conf`.

To use a text-based editor such as `vi`, you would enter the editor name followed by the file name that you want to edit on the CLI.

```
vi /etc/kismet_ui.conf
```

#### The Introductory Splash Screen

When Kismet is first run, a small splash screen opens up over the main window. The splash screen, entitled “Welcome to Kismet” tells you what Kismet client you're running, including the version and build number. It welcomes you to the Kismet panel's front end and advises you that you can press **h** at any time to get help information. It also tells you that you can turn off of the message by editing the `kismet_ui.conf` file. Pressing the space bar will get rid of the splash screen. This splash screen is shown in Figure 3.1.

![](img/d6ac176c353d2b7687c1186a140180a1_73_0.png)

![](img/d6ac176c353d2b7687c1186a140180a1_73_1.png)

Now we want to get rid of the splash screen, so that it doesn't open whenever Kismet is run. To do this, edit the line *showintro=true* and change it to *showintro=false*.

Save the file and restart Kismet. Kismet will now start up without the splash screen. Remember, press the h key to open a Help screen. The Help screen is further discussed in Chapter 4.

#### Play Sounds

Kismet, by default, plays sounds when certain events happen or are detected. Those events are when:

- A new network is detected
- Traffic is seen on a detected network
- Junk traffic is seen on a detected network
- Alarm conditions are triggered

Four sound files for these functions are installed in the /usr/share/kismet/wav directory when Kismet is installed. Playing sounds can be turned on or off by setting the sound value to true or false. By default, the sound is on, and can be found on this line: `sound=true`

The sound application that comes as part of most Linux installations is play, and by default, Kismet uses play to present those sounds to the user. This can be seen from this line: `soundplay=/usr/bin/play`

However, some Linux distributions come with different sound applications. If play is not the sound application on your laptop, then you will have to change the soundplay=/usr/bin/play line to reflect the sound player that is installed. For example, aplay is the sound player application that comes with Ubuntu Linux version 8.04. If you are using Ubuntu v8.04, you have to change the line to soundplay=/usr/bin/aplay, so that the play application is used to play the sound files.

### Additional RF Equipment: Antennas and Cables

Most people using Kismet for the first time will use it for the activity known as “war driving,” or locating Wireless Local Area Networks (WLANs) while driving through a given area. The steel and aluminum body panels in most auto bodies block radio signals very effectively, and because of this, an antenna is usually one of the first accessories purchased to be added to the Kismet laptop. An external antenna for WLAN uses functions in the same way as the AM/FM radio antenna on your car. It allows a weak signal, which otherwise might not penetrate the car body, to be brought in where the receiver—or in the case of Kismet, the wireless networking card—is located.

To help you understand antennas and how they work, here are some basic terms you should know when determining what type of antenna you want to use while running Kismet:

- **Gain** Gain describes how well an antenna performs. The units used to describe gain are the *decibels*.
- **Decibel (dB)** A decibel is the unit of measure for power ratios describing loss or increase of apparent radio frequency power, normally expressed in watts. A decibel is not an absolute value—it is the measurement of power gained or lost between two communicating devices. These units are usually given in terms of the logarithm to Base 10 of a ratio.
- **dBi value.** This is the ratio of the gain of an antenna as compared to an *isotropic antenna*. The greater the dBi value, the higher the gain. If the gain is high, the angle of coverage will be more acute.
- **Isotropic Antenna** An isotropic antenna is a theoretical antenna that radiates its signal to cover the area in a perfect sphere. It is used as the starting point to describe the performance and gain of a real antenna.

Generally, an antenna capable of transmitting and receiving the signal equally in all directions is preferred. These antennas are known as “omni-directional” or “omni” for short. Most war drivers use an omni antenna in the 3 dBi to 8 dBi range, as these give the best compromise on signal gain and pattern. Commonly, this type of omni-directional antenna has a magnetic base that sticks readily to a steel car body roof. Such “mag mount” antennas allow the antenna to be transferred between different vehicles without a complicated installation. Two small omni-directional antennas along with a wireless card can be seen in Figure 3.2. The antenna on the left is approximately 6 inches in height and has a magnetic base that allows it to be easily mounted on a car body. The antenna on the right is made for use on tabletop. Both have a gain of approximately 5 dBi.

#### Figure 3.2 3dBi Omni-Directional Antenna with Magnetic Mount Base

![](img/d6ac176c353d2b7687c1186a140180a1_76_0.png)

One common misconception is that the higher the gain of the antenna, the better your results will be when using Kismet. This is not true. The important thing to understand from the preceding definition of dBi value is the last sentence: “If the gain is high, the angle of coverage will be more acute.”

The signal coverage area of an omni-directional antenna is shaped roughly like a donut. The higher (or larger) the gain, the “shorter” the donut. The opposite is true as well. A smaller gain antenna has a “taller” donut. Figure 3.3 shows the signal donut of a 5 dBi gain omni-directional antenna compared to that of an 8 dBi gain omni-directional antenna. The signal donut of the 5 dBi is taller than the signal donut of an 8 dBi gain omni-directional antenna. This is illustrated in the side view. What this means is that although it has a “weaker” signal, as indicated in the overhead view, a 5 dBi gain omni-directional antenna is likely to provide better results in a neighborhood with tall buildings, such as an urban downtown area. Also, because these antennas rely on line-of-sight communication, a 5 dBi gain antenna works well in residential areas where homes and other buildings provide obstructions between your antenna and any wireless access points (APs).
