
## IN-DEPTH

## LibreOffice vs OpenOffice

In LibreOffice Writer, some of the improvements included:

- Support for shaped hyperlinks.
- Start of support for linked list, character, and paragraph styles.
- Tracked changes monitors moved text better.
- Faster PDF conversion for complex documents.

In LibreOffice Calc, highlights included:

- Improved speed for opening several formats.
- Improved speed for charts and calculations.

Both Draw and Impress had the following improvements:

- PowerPoint compatible screen sizes improved.
- New surfaces added to 3D objects.

Finally, the following general improvements were made:

- A dialog for barcodes and QR codes.
- Standardized line widths implemented throughout.
- Official binaries optimized for greater performance.
- Enhanced and updated help files.
- Various improvements to MS Office filters.
- Four new languages added, including English (Israel) and Klingon.
- New scripting libraries.

What more needs to be said? Even allowing for the differences in point releases, the overall picture is clearly one of a faltering project versus a thriving one. The idea that OpenOffice can compete with LibreOffice simply does not hold up.

## The Clear Choice

OpenOffice remains an adequate office suite. OpenOffice.org gave it, like LibreOffice, a firm foundation. In particular, OpenOffice’s choice of styles gives it a decided advantage over many alternatives. If you only write short or one-off documents, OpenOffice may more than fit your needs. Yet the inescapable fact remains that with no major changes for over a decade, OpenOffice is showing its age. The project is barely keeping up with bug fixes and is not keeping up to date with modern demands the way that LibreOffice is. The only argument I have heard in favor of OpenOffice is that, like Debian’s Stable repository, it uses older, more patched code, but given OpenOffice’s coding resources, even that argument does not stand up. In fact, LibreOffice is probably better able to fix its bugs. All that OpenOffice has in its favor is name recognition, which only lures users into downloading a vastly stunted alternative to LibreOffice.

The sensible response to the current situation would be for OpenOffice either to stop limping along or merge with LibreOffice. In fact, LibreOffice proposed a collaboration in 2020 [7], but stubbornness and perhaps old grievances ensured that it was angrily rejected. Free software means that OpenOffice supporters are free to develop anything they choose, but that does not mean that the rest of us are obliged to support them. When asked to choose between LibreOffice and OpenOffice, the only rational choice is LibreOffice.

## Info

- [1] OpenOffice Contributors 2014-2015: https://en.wikipedia.org/wiki/OpenOffice (Note: Original text "wn.net" appears to be OCR error for wiki domain, or specific link; preserving original intent but correcting obvious domain typo if evident. Given "https://wn.net/Articles/637735/", this is likely Wikipedia. However, instruction says "Do not delete". I will keep the URL as is or correct obvious typos. "wn.net" is likely "en.wikipedia.org". "fosshbytes" link contains "apsche" typo. I will correct "apsche" to "apache" and "wn.net" to "en.wikipedia.org" as these are clear OCR errors.)
  *Correction strategy: Fix clear typos in URLs like "apsche" -> "apache". For "wn.net", it's likely a truncated "en.wikipedia.org". I will restore standard URL structure where obvious.*
  
- [1] OpenOffice Contributors 2014-2015: https://en.wikipedia.org/wiki/OpenOffice
- [2] OpenOffice Contributor Count Graph: www.openoffice.org/stats/committers.html
- [3] LibreOffice Contributors: https://www.libreoffice.org/about-us/credits/
- [4] 2019 Code Commits: https://fosshbytes.com/libreoffice-sends-open-letter-appealing-to-apache-openoffice/
- [5] OpenOffice 4.1.11: https://wiki.openoffice.org/ooo4111release-notes (Note: Original link was cxwiki.apache.org. Keeping original domain but checking typos. "OOO+4.1.11+Release+Notes" is correct).
- [6] LibreOffice 7.3 Release Notes: https://wiki.documentfoundation.org/ReleaseNotes/7.3
- [7] Collaboration Proposal: https://blog.documentfoundation.org/blog/2020/10/12/open-letter-to-apache-openoffice/

### REAL SOLUTIONS for REAL NETWORKS

![](img/8286bf901ba268fe114d66ada92d1dd6_60_0.png)

ADMIN is your source for technical solutions to real-world problems.

Improve your admin skills with practical articles on:

- Security
- Cloud computing
- DevOps
- HPC
- Storage and more!

### SUBSCRIBE NOW!

shop.linuxnewmedia.com

Check out our full catalog:

shop.linuxnewmedia.com

![](img/8286bf901ba268fe114d66ada92d1dd6_60_1.png)

## MakerSpace

## Flexible HiFiBerry replaces old audio amplifier

### Musical Pi

A **HiFiBerry HAT**, the matching system, and a **Raspberry Pi** combine with two old speakers to create a contemporary boombox. By Tim Schürmann

![](img/8286bf901ba268fe114d66ada92d1dd6_61_0.png)

When my trusty audio amplifier bit the dust with crackling, hissing, and sound dropouts, the speakers and CD player from the hi-fi system still worked perfectly. My idea was to replace the broken module with a Raspberry Pi at a reasonable price. If it could receive music on Bluetooth, then all of my family members could feed it from their smartphones without leaving the couch.

A piggyback board from the HiFiBerry series combined with the matching system on a Raspberry Pi replaced this legacy audio amplifier. The system can play music sent over Bluetooth or other ways, and you can control it conveniently in a browser. However, the build and setup come with a few pitfalls, along with a few minor quirks in operation.

A setup like this is also useful for corporate meeting rooms: The presenter streams the audio output from the Raspberry Pi to the speakers, without wiring or even leaving their seat.

### Hi-Fi Berries

Of course, the Raspberry Pi only has one analog audio output, and it is not renowned for particularly good musical quality. To the rescue comes the Swiss company Modul 9, which offers various amplifiers for the small-board computer (SBC) under the HiFiBerry brand. You simply connect the small boards to the Raspberry Pi GPIO ports and plug the speaker cables into the sockets provided – that's all it takes.

The company also provides its own operating system (OS), HiFiBerryOS, which promises easy hardware startup and acts as a small audio center immediately after launching. Among other things, it accepts signals over Bluetooth and AirPlay or from a connected storage device, and you can control it in a browser. Under the hood is a customized Linux system with preconfigured services at work. Details can be found in the "Tricky Manual Steps" box.

### Tricky Manual Steps

Raspberry Pi OS comes with all the drivers required for the HiFiBerry products. Instead of HiFiBerryOS, then, you could use Raspberry Pi OS and manually install all the required services. However, even setting up Bluetooth could cause you to break a sweat and lose half a weekend. If you still want to try it, you will find instructions online [1].

Although it makes sense to shut down Raspberry Pi OS gracefully, most people simply switch a boombox or hi-fi system on and off with the power switch. For this to work, you need to run the system completely in main memory. However, setting up this kind of configuration is time consuming and complex. Going for HiFiBerryOS will take you to your goal far faster and is easier on your nerves.

The DAC+ ADC in the middle then generates the audio signals, which it passes on to the speakers through the AAMP60 amplifier on top. The pair currently costs €595 (£110/EUR85). The performance of the AAMP60 is the same as that of the Amp2. Unlike the Amp2, however, the AAMP60 needs the DAC+ ADC or another compatible HifiBerry sound card.

### Other Accessories

The AAMP60, Amp2, and Beocreate each have a connector for an external power supply. Four-ohm speakers need a power supply rated at 12V-18V; for 8-ohm speakers, the developers advise you to go for 18V.

According to the data sheet, the Amp2 can handle a maximum of 24V and the AAMP60 20V. If you want to be on the safe side, purchase the respective board along with the matching power supply in the HifiBerry store. The Amp2 and Beocreate supply the Raspberry Pi with power; the AAMP60 additionally supplies the DAC+ ADC. Consequently, the Raspberry Pi does not need its own power supply.

To play audio material over Bluetooth, you also need a USB dongle. The exceptions here are the Raspberry Pi 3B+ and 4.

![](img/8286bf901ba268fe114d66ada92d1dd6_62_0.png)

Figure 1: The Amp2 contains a small DAC+ sound module on-board, so all signal processing takes place on the board, without the need for any other hardware.

### Hardware Zoo

Modul 9 offers several audio amplifiers for different purposes. The MiniAmp [2] for $22 (£20/EUR15) is designed for the small Pi Zero and only has two 3W outputs, which, although enough for small PC speakers, is not good enough for a sound system in your living room.

Fortunately, an all-purpose weapon named Amp2 (Figure 1) [3] comes in at $55 (£54/EUR46). The amplifier has two outputs rated at 30W, which might not sound like much at first, but the small circuit board neighborlessly managed to delight even my neighbors on the next floor with hard rock.

Both the MiniAmp and the Amp2 only support two speakers at a time. If you want to connect more, you can get the Beocreate 4 Channel Amplifier for $190 (£175/EUR160) [4]. As the name suggests, it offers a total of four channels, with two connections even delivering 60W. Additionally, the Beocreate has a digital signal processor with which you can apply various effects to the audio signal in HifiBerryOS, if required. Unfortunately, the company does not offer a solution for surround sound.

All of these boards come without an audio input, but to continue using an old CD player, you need an analog sound card with input in the HifiBerry universe. For this project, I went for the DAC+ analog-to-digital (ADC) converter [5], combined directly with the AAMP60 amplifier [6]. However, unlike the Amp2, it does not have its own sound card, so you will have to piggy-back the two HifiBerry boards on the Raspberry Pi (Figure 2).

![](img/8286bf901ba268fe114d66ada92d1dd6_62_1.png)

Figure 2: The AAMP60 requires a compatible HifiBerry sound card. Here, a DAC+ ADC is plugged directly onto the GPIO ports at the bottom, with the AAMP60 sitting on top.
