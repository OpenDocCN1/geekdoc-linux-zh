

![](img/b2b6702758c230ce537468351fc8af15_351_0.png)

Figure 17.6

![](img/b2b6702758c230ce537468351fc8af15_351_1.png)

Figure 17.7 Oh, no! More Lemmings comes in the Executor demo distribution.

## Configuring Executor

Executor has a surprisingly small number of important configuration options and does a good job of guessing effective default values. However, you might want to make certain adjustments both when you launch the emulator and while Executor is running.

Browser does not have MacOS's intricate series of control panels. Instead, it has a single configuration screen you can open with Alt+Shift+5. Figure 17.8 shows a sample configuration screen.

You should never have to touch these settings until you discover that a program is not running properly.

![](img/b2b6702758c230ce537468351fc8af15_352_0.png)

Figure 17.8. The Executor preferences screen incorporates most of the emulator's configurable options in a single location.

Executor doesn't run MacOS, but some programs expect to be told which version of MacOS they are running on. Executor can "spoof" this information and by default tells programs it is plain old System 7. You might need to update the System heading to a higher number (such as 7.5.3 or 7.6.1) to get some programs to run because they might refuse to load if they think they are running on an older version.

You can disable sound if it is malfunctioning or taking up too much CPU time. If you are experimenting with really old Macintosh programs, you might want to click No 32-bit Warnings, which keeps Executor from telling you the program might be too old to run. (However, a program that is not "32-bit clean" can cause Executor to crash or hang.)

Some advanced settings must be made at the command line. Executor defaults to a 640×480 Macintosh display, but you might want to make it larger by appending -size 800×600 or -size 1024×768 to the executor-demo-sdl command.

You can expand or shrink the memory reserved for Executor with the option -memory. -memory 16.5M reserves 16.5MB for Macintosh programs and the Executor emulator overhead. Executor can access up to 64MB of memory and may default to 32MB or more on your PC. The Executor startup screen tells you how much memory is in use.

-grayscale can come in handy if you are running software that expects a black-and-white Macintosh.

> When in doubt, read the documentation. Executor installs a man page (type man executor at a command prompt) and provides extensive online documentation at http://www.ardi.com.

## Understanding Executor's Limits

Executor is clever, but not perfect. ARDI cannot emulate undocumented MacOS system calls, and Executor has incomplete or buggy emulation of some of the more obscure and esoteric documented operations. This problem makes some software completely incompatible, probably forever.

Executor also does not give you a multitasking Mac environment: You can only run one application (or the Browser) at a time. You can, of course, save your work, quit, and load another application, but you cannot switch between applications as a real Macintosh running MacOS 7 can.

Despite Executor's MacOS version number spoofing, some programs use an unusual method to determine the OS version and quit because they don't believe they are running on a proper MacOS 7 machine. I have seen programs quit claiming that they require System 6.0.7 or better, a test Executor should—but can't always—pass.

Although serial and parallel ports can be shared with Mac programs, networking (such as Ethernet sharing) is not permitted, nor can Executor drive a modem for dial-up networking. Because you can easily access Executor files in Linux and vice versa, this is not a crippling limitation, but it will prevent you from running any Macintosh programs that rely on networking or outside communication.

## Using Basilisk II

If you want to replicate the entire Macintosh experience, Basilisk II is the way to go. Although more complicated to install and configure, once it is complete you might swear that there's an Apple badge on your computer.

Basilisk II, like Executor, is not perfect. But the full Macintosh emulation should help you avoid some of the frustrating compatibility problems that can arise with Executor.

## Installing Basilisk II

Believe it or not, it is possible to run Basilisk II in a Windows virtual machine. In fact, I recommend you give it serious thought if the Linux version gives you trouble. Although you will suffer some reduction in speed because of the VMware layer, the Windows version is a little easier to troubleshoot.

## Installing Basilisk II for Linux

Although the source code for Basilisk II is available and you are welcome to modify and compile it yourself, you will probably have an easier time simply using the prepared RPM installer:

