
## Running Other Emulators

Wait, there’s more. If you’re starting to get really curious about emulation, there are a wide variety of emulators and emulation support Web sites out there. One launch point as good as any is http://www.vintagegaming.com, which should be enough to get you started emulating almost any computer or popular computing device.

As I explained in Chapter 17, “Emulating the Macintosh,” it is possible to run Windows emulators inside a VMware virtual machine (although you should not attempt to run VMware for Windows inside a Windows VM!).

There are advantages to running an emulator in a Windows VM instead of Linux. Generally, Windows emulators are distributed as binary files, rather than source code that must be compiled, as many Linux emulators are. And among emulators that exist for both Windows and Linux, some (but not all) have better configuration and customization interfaces.

There is some downside. The speed penalty from the VMware layer can be a hassle. Plus joysticks are not available in VMware, so if you plan to use them, you need to stick with Linux emulators.

A perfect example of the advantages of a VMware-based emulator cropped up as I wrote this chapter. I wanted to include an Apple II emulator in the book. The Apple II was the first true mass-market personal computer and one of the most successful in the home and educational markets. It also was the launch pad for the wildly popular Ultima RPG game universe. (See where it all began in Figure 18.15.)

Unfortunately, I couldn’t find a Linux Apple II emulator that would reliably compile with a minimal amount of tinkering, and I couldn’t justify spending pages and pages explaining modifications to the source code.

![](img/b2b6702758c230ce537468351fc8af15_382_0.png)

So I settled on ApplePC, a DOS/Windows Apple II emulator that runs splendidly in VMware. There's no need to tinker with the source code, and the emulator is quite compatible. ApplePC runs in a DOS window, although you can also hunt down pure Windows-based Apple emulators, such as AppleWin. Both are available through http://www.vintagegaming.com.

Through emulation, you can relive the pre-Macintosh glory years of Apple and reintroduce yourself to the literally hundreds of wildly popular mind-bending adventure games (such as the one pictured in Figure 18.16), famous on the Apple II+, IIe, and IIc.

There are even emulators available for devices such as the Palm PDA! Palm makes the source code available for Linux users, but it requires the FLTK graphics toolkit, making for an inconvenient two-stage install. If you want to see whether that's worth the trouble, download the Windows version of the emulator from http://www.palmos.com/dev/tech/tools/emulator.

> Like most emulators, the Palm emulator requires Palm ROM code. The emulator can download a ROM from a Palm device you own, or you can register for the Palm developer program free of charge to obtain the ROM images from Palm Inc.

When you download the ROM, you have a real live Palm device running in the confines of your desktop. Figure 18.17 has the proof. Purists might say a desktop emulator ruins the point of a portable, but emulation enthusiasts know better.

![](img/b2b6702758c230ce537468351fc8af15_383_0.png)

Figure 18.16 ApplePC, via VMware, runs Cranston Manor, one of many classic graphics/text adventure games for the Apple.

![](img/b2b6702758c230ce537468351fc8af15_384_0.png)

Figure 18.17 The Windows version of the official Palm OS emulator works well through VMware.

### Conclusion

There are literally dozens of computers, game consoles, and electronic devices that can be emulated through Linux and a VMware virtual machine that I have not touched on. I hope the “emulation sampler” in this chapter will encourage you to go beyond the bounds of VMware’s ability to expand your computer’s range of operating systems and branch out into emulating a variety of software and hardware platforms from the last 30 years of computing.
