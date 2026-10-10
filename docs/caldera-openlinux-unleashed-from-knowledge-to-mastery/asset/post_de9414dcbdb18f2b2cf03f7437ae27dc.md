
that will help you solve all those problems you are having documenting your Web page. CWEB2HTML will convert a WEB format file into an HTML file for browsers on the Web.

## Exotica (or Really Fancy Typesetting)

For those of you who want to do some interesting things with typesetting, the Web has available many tools that work with TeX to provide various functionalities.

Some of the more interesting tools are discussed in the following sections.

### Typesetting Music

If you want to typeset either polyphonic or other multiple-stave music, you will want to check out MusicTeX by Daniel Taupin.

It is available from:

ftp://ftp.gmd.de/music/musictex/

Another alternative (with a very similar name) is MusiXTeX, which is available from:

http://doc2.wi-inf.wissen.de/doc/musixtex-173s-1/

MusiXTeX supports wide pages as used by most musicians, as well as LaTeX-formatted narrow pages. It will typeset the following: staves, notes, chords, beams, slurs, and ornaments.

It comes with extensive documentation and samples. It is a bit complicated to use, but the output (and the ease of change of the output) will make it worthwhile for most musicians.

### Typesetting Plots

The standard for typesetting plots using TeX or LaTeX is DISLIN. It is a high-level library of subroutines and functions that will assist you in displaying plots for inclusion in a LaTeX document.

Most commonly, you will use DISLIN to produce a PostScript plot and include this image in your TeX document. However, the product comes with several other drivers so that you can perfect the plot before you commit it to PostScript for your document.

The major site for information and usage can be found at:

http://www.limp1.mpg.de/dislin/

An RPM-installable copy of the software can be found at:
http://linusp.usp.br/rpm2html/contrib/libc5/i386/dslin_vf-7.1-1.i386.html

### Typesetting Feynman Diagrams

Feynman diagrams are interesting things. If you are interested in high-energy physics, you probably use them every day.

They are named for their inventor, Richard Feynman, who was a high-energy physicist when he wasn’t playing practical jokes. At Los Alamos, the most heavily guarded military installation in the U.S., Feynman learned to pick locks, and he would often leave safes and filing cabinets open to show that they were no good. He also enjoyed sneaking out of a hole in the fence and then going to the front of the compound and surprising the guards. All in all, he would’ve loved Linux (he died in 1988).

So if you ever need to typeset a Feynman Diagram, you can use Michael Levine’s package to do this, and you can find it at:
http://ftp.tex.ac.uk/tex-archive/macros/latex209/contrib/feynman.tar.gz

So you don’t think there is only one of these packages for Feynman Diagrams, you might also check out Thorsten Ohl’s contributions at:
http://ftp.tex.ac.uk/tex-archive/macros/latex/contri/b/supported/feynfm.tar.gz
which works in combination with MetaFont or MetaPost and will produce a font of images used in Feynman Diagrams or, alternatively, a PostScript image.

### Summary

In this chapter, you have been introduced to the typesetting capabilities in native Caldera, as well as functions available via the Web. You have created a typeset document, learned about Literate Programming, and learned how to convert from one form of typeset document to other forms of printed and displayed documents. Finally, you have learned a little bit about typesetting music and graphs and Feynman Diagrams, which are named after a Nobel prize–winning jester.

# 29
## CHAPTER
## Setting Up Sound and Multimedia

### IN THIS CHAPTER

- Introduction 672
- Getting Sound 672
- Linux Kernel Sound 673
- OSS—Open Sound System 679
- ALSA—The Advanced Linux Sound Architecture 683
- Audio Data Manipulation and Conversion 687
- Extracting Digital Audio Data 689
- MPEG 1 Layer 3 Encoding 692
- Lossless Audio Encoding Using Shorten 695
- SoundTracker Modules 697
- Introduction to MIDI 700
- Software MIDI Synthesis 702
- Where to Go from Here 705

### Introduction

When presented with the task of writing a chapter on Linux sound and multimedia, I had a couple of options. I could have chosen to write a broad, shallow treatment of the topic, briefly touching on a wide variety of multimedia technologies without providing much practical information. Or, I could have chosen to provide focused in-depth coverage of the hottest sound and multimedia technologies in the Linux world, packing the chapter to the brim with inside information on how to push Linux multimedia to its limits. Fortunately for you, I picked the latter, figuring that you probably were looking for more than a simple overview of Caldera’s multimedia capabilities.

In the second half of this chapter, I focus on cutting-edge Linux sound technologies and applications, such as audio data manipulation and conversion, digital audio extraction, MPEG 1 Layer 3 encoding, lossless audio compression, a review of MIDI technology and an in-depth look at MIDI software synthesis engines. At the very end of the chapter, I provide you with links to online resources that you can use to expand your Linux multimedia knowledge beyond the scope of this book. If you have already mastered the art of configuring your sound card under Linux, you can skip to the “Audio Data Manipulation and Conversion” section.

If you have not yet configured your sound card so that it works properly under Caldera, or you are interested in exploring other sound architectures, read on—I cover the configuration of sound under Linux in depth. In addition to covering standard kernel sound driver setup, we will look into the Open Sound System (a commercial option) and the Advanced Linux Sound Architecture (ALSA), an excellent free alternative. I also provide much-needed information regarding the tricky topic of ISA PnP sound hardware configuration, as well as explore possible sound configuration pitfalls and driver compatibility issues.

### Getting Sound

There are several ways to get sound working under Linux, but the basic principle is identical in each case. The trick is to create and install kernel modules that then can be loaded by the kernel. They will provide an interface so that user programs can access your sound hardware safely. If you happen to own an ISA PnP sound card, there is a possible additional step of configuring the PnP resources of your card.

As I mentioned, although the principle is identical, you have several different techniques available to you to actually get sound working. We will explore three in this chapter. The first technique is the use of the standard Linux kernel sound modules, which might be all

you need. The second technique is a relatively inexpensive commercial option called OSS, which features sound support for a wider variety of new hardware. Finally, I cover ALSA—the Advanced Linux Sound Architecture. ALSA is a non-commercial effort to provide enhanced support for a wide variety of sound cards, and it is free.

### Choosing a Sound Card

Before purchasing a sound card for use with Linux, do a little research and verify that drivers for the card are available in the most recent Linux kernel, in OSS, or in ALSA. Many sound card manufacturers have not yet realized the importance of supplying Linux developers with specifications for their sound cards, or they will release such information only after the developer signs a nondisclosure agreement (NDA), which would violate the terms of the GNU Public License. If at all possible, choose a PCI-based sound card that is supported under Linux. Such a card will offer higher performance and be easier to configure.

### Linux Kernel Sound

If you have a PCI-based card or standard ISA (non-PnP) card, setting up sound is quite easy. For PCI-based cards, it’s just a matter of loading kernel modules in the right order, starting with a basic sound module called soundcore, and progressing to a hardware-specific module designed for your particular brand of sound card. ISA cards also require you to specify the correct interrupts and memory addresses for the card as command-line arguments when loading the hardware-specific module. ISA PnP sound cards are handled identically, except that before you load the hardware specific kernel module, you need a special set of PnP tools to communicate with the ISA PnP card and configure it to use interrupts and IO addresses that you specify. After the ISA PnP card is configured properly, you can treat it as if it were a standard ISA (non-PnP) card, and load the sound card module with the appropriate parameters. If you’re confused, don’t worry. I will cover each method step-by-step.

### Initial Manual Configuration

First, we are going to attempt to load the sound drivers manually and verify that they are working properly. After we get them working, I will explain how to make changes to your system so that the sound is properly configured on startup.

![](img/df365d352a104b50fea29e59a052de4d_710_0.png)
