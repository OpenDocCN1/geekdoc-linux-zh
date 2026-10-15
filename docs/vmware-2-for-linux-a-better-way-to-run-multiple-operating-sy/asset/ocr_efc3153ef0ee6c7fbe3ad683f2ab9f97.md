# Emulators

Generally speaking, an emulator is a program that enables you to run software that was not originally intended for your computer's hardware and OS combination. That can be a relatively small step (such as running a Windows program on a Pentium-based Linux PC, something that the PC is normally capable of if it isn't running Linux at the time) or a dramatic departure from the norm (such as running Macintosh, Apple II, or Commodore Amiga software on your PC).

Emulators generally, but not always, multitask with the host operating system, meaning that your desktop is behaving like two (or more) different computers at once.

To work their magic, emulator authors describe the functionality of a computer's hardware in software. For example, emulating an Amiga on a Pentium-based Linux computer requires a complete description of the operation of the Amiga's 68000-series CPU, as well as special code to replicate the Amiga's custom video display and sound capabilities. Inside the emulation window is a virtual computer that believes it is an assembly-line fresh Amiga computer, but it is really just a construct of the Linux operating system.

When a program runs inside an emulator, it can't tell the difference. It doesn't know that it's being fooled into running on a Linux PC. So it tries to run exactly as it would on the real computer it was designed for, calling on a CPU and hardware it expects to be there. Of course, that hardware isn't on your computer. Instead, the emulator traps those requests, interprets what the result should be, and sends the information back to the program inside the emulator. At the same time, when the emulated program sends out video or sound information, the emulator intercepts the information and translates it into video and audio that Linux can handle. See Figure 1.1 for a (very basic) illustration of the inner workings of an emulator.

For starters, acceptable emulator performance requires a large amount of system RAM, preferably as much available RAM as the target emulation system normally needs. Good emulators allow you to select how much you want the emulated computer to have. Many emulators also grab much more—several megabytes, depending on the emulator—to provide a fast buffer for the intense computations required to run an emulation.

BUZZWORD
Host operating system: The primary OS your computer boots into. In your case, this is Linux.

![](bbox=[0.07, 0.88, 0.78, 0.96])

Figure 1.1 How an emulator works.