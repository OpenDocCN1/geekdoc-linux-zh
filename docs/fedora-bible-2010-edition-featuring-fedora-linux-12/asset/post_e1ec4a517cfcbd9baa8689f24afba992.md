
account on WordPress.com or you can use that software to set up your own blogging site. Install the wordpress package in Fedora to get started.

- **Wiki software** — Wikis let you gather and organize large amounts of information online. Instead of having to write everything on a Drupal by yourself, by creating a wiki you can allow people to sign up for accounts and add and correct articles on your site. Wiki software available to the open source community includes MediaWiki (install the mediawiki package) and MoinMoin (install the moin package). See the `http://MediaWiki.org` and `http://moinmo.in` sites, respectively, for further information.
- **Content management system (CMS) software** — For some Web sites, you might want to offer a range of information. For an active online community you may want to offer articles, forums, online polls, downloads, and other diverse activities. Content management systems (CMSs) such as Drupal (install the drupal package) offer a platform for creating and managing those types of activities online. Other open source CMS systems include Plone (`http://plone.org`) and Zope (`http://zope.org`).

Before installing and making any of these types of Web sites available on the Internet, you should keep in mind that it will take some commitment to stay current with software updates and keep the site maintained. But if you are willing to make that commitment, the open source projects just mentioned can help you produce high-quality sites for publishing on the Internet.

## Summary

Tools available in Linux for publishing words and images on paper and the Web can compete with similar software available commercially. For producing hardcopy documents, you have word processors such as OpenOffice.org Writer, AbiWord, and StarOffice. To lay out pages, there is Scribus. To work with photos, you have GIMP, or for vector graphics you can use Inkscape.

Software for publishing content on the Internet is also available now in almost any category you can think of. For blogging, you can create a WordPress site. For image galleries, there is Gallery software. Content management systems include Drupal, Plone, and Zope. To create wikis, there are MediaWiki and Moin Moin.

# Chapter 7

## Music, Video, and Images in Linux

### In This Chapter

- Listening to music
- Using Webcams and TV Tuner cards
- Playing video
- Working with digital cameras and images
- Playing games on Linux

Nearly every kind of audio and video format available today can be played, displayed, encoded, decoded, and managed in Linux. With the development of the Theora video codec, there are now patent-free, royalty-free formats available for every major type of multimedia content available today. If you are starting from scratch, you can legally create, manipulate, and share your own multimedia content from Linux using all free applications and codecs.

This chapter covers many different tools that come with Fedora for playing or displaying digital music, video, and images. It also takes a swipe at explaining some of the legal issues surrounding software for playing commercial movie DVDs, MP3 music, and various audio/video formats in Linux.

Video content that is readily available on the Internet for playing movie clips, commercial films, and other content can be viewed using several different players in or available for Fedora. Also, you can view live television and video using TV Tuner cards (or TV cards for short) and Webcams.

Because CD-ROM is the physical medium of choice for recorded music, this chapter describes how to set up and use CD burners to create your own music CDs. After your CD burner is set up to record music, you can use the same CD burner to back up your data or to create software CDs. (The same tools can be used to burn DVDs as well.)

# Understanding Multimedia and Legal Issues in Linux

You can’t play commercial (encrypted) DVD movies or MP3 music with software delivered with Fedora because software needed to do so isn’t included in Fedora. That’s because there are patent claims associated with the formats used to store, encode, and decode that content that would prevent open source software that worked with that content from being freely distributed.

Commercial Linux vendors, including Red Hat, have decided not to add software codecs (which encode and decode multimedia formats), even if they were written from scratch and covered under the GPL, that are encumbered by contentious software patents. After Thomson and Fraunhofer Gesellschaff (which control the MP3 patent) began requesting licensing fees in 2002 of $0.075 for MP3 decoders (per system), Red Hat Linux dropped MP3 support. (See `http://www.mp3licensing.com/royalty` for details.)

Just to clarify, I am not talking about copyright here. Nobody can rightfully claim that it is okay to copy someone else’s commercial code and release it as free software. It would clearly violate copyright laws. What we are talking about are patents.

The idea of a patent is to allow someone to control the rights regarding who can make, sell, offer to sell, use, or import an invention that the patent applicant dreamed up. As it relates to multimedia software in particular, the encoding and decoding of audio and video content for many commercially released music and video formats are covered by patents. So, even if open source developers write every piece of code from scratch to encode and decode content, it may not be legal to distribute it without paying a royalty to the patent owner.

Major efforts are underway (especially in Europe) to oppose software patents. Refer to the Foundation for a Free Information Infrastructure Web site (`http://ffii.org`) for further information. The contention is that so many ideas related to software are being patented that it could severely cripple the ability to innovate (especially for open source developers or small software companies without huge legal teams).

Patents have been granted in Europe for common items that might appear on a Web page, such as selling things over a network, using an electronic shopping cart, and using rebates codes (see `http://webshop.ffii.org`). Although there are new laws in Europe that are aimed at preventing any further software patents, some software patents are still being granted and existing patents are still being used to discourage innovation.

Despite efforts against software patents, however, the fact remains that Fedora does not include some of the software that you would want to use to play your digital media. That doesn’t mean, however, that there is nothing you can do to legally play the commercial audio and video content you want to play in Linux. This chapter includes discussions on how to find the codecs you want and use them legally, when possible.

## Extending Freedom to Codecs

Fedora may not be able to give you the audio decoders you need to play every kind of media you want, but it gives you the freedom (and the tools) to go out and get those decoders yourself. For example, you can purchase codecs for non-free audio and video formats, such as MPEG4 video, Windows Media, and others. Or, if you are in a country where software patents are not recognized, Fedora finds and automatically downloads open source software that can play many different types of patent-encumbered codecs.

A company called Fluendo ([http://www.fluendo.com](http://www.fluendo.com)), which is responsible for the GStreamer multimedia framework used in Fedora, purchased an unlimited MP3 license that allows you to download the Fluendo MP3 Audio Decoder for free, to play your MP3 audio files. You can pay a small fee to get audio/video codecs such as Dolby AC3 Audio Decoder, Windows Media MMS Network Stream Reader, MPEG2 Video Decoder, or MPEG4 Part 2 Video Decoder. Read the licensing agreement that appears before you accept the download. Unlike software that comes with Fedora, you cannot freely redistribute the codecs you get from Fluendo.

## Listening to Music in Linux

Good-quality sound hardware is considered a necessity for today’s desktop and laptop computer systems. Whether playing songs downloaded from the Internet, sound tracks to digital movies, or audio from a TV card, any user-friendly operating system has to support a healthy list of sound hardware and audio applications.

Most popular sound devices for the PC, whether on separate cards or built into your computer’s motherboard, will be automatically detected when a Fedora system boots up. Appropriate modules will be loaded, so you can immediately begin using your sound card.

Beginning with Fedora 8, PulseAudio ([http://www.pulseaudio.org](http://www.pulseaudio.org)) became the default sound system used with Fedora, taking over that spot from Advanced Linux Sound Architecture (ALSA). PulseAudio basically provides the interfaces between audio applications and your sound card. A major improvement over other audio systems is that it allows you to control volume levels separately for different applications. Also, by incorporating plug-ins, PulseAudio lets you use audio applications that were designed for ALSA.

To control playback volumes and audio input and output devices, the pulseaudio package includes the PulseAudio Volume Control window. The alsa-utils RPM package contains the commands and configuration files you can use to tune your sound card and adjust audio levels. Other friendly graphical tools have been added by the GNOME and KDE projects for managing sound.

After your sound card is working and audio levels are adjusted, you can use any of the dozens of audio applications that come with Linux with your sound card. Those applications include
