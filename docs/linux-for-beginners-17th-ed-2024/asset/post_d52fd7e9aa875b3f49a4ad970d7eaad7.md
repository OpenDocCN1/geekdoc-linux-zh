
## Install Apps via the Terminal — Part 2

- **STEP 5** If you enter `ls` again, you’ll notice that a new folder has been created: `vim74`; in light blue text representing a folder in `Mint`. It’s always handy to create root folders for the main app. You can upgrade apps through this method the individual versions will each have their own folder.

![](img/5019375da05cbf0090115165d80772a1_52_0.png)

- **STEP 6** Type in `cd vim74` to enter the folder, and `ls` again to view its contents. There will likely be a fair number of files present; most are app’s core files, while others will be labelled `README` or `INSTALL`. It’s always wise to read these files first as they provide valuable information regarding the installation.

![](img/5019375da05cbf0090115165d80772a1_52_1.png)

- **STEP 7** The first part of the installation requires you to enter `./configure`. The `./configure` command will check your system for any missing dependencies associated with the app. If you received an error regarding a C Compiler, then enter: `sudo apt-get install build-essential`. The third-party app `Ncurses` was recorded as missing. We need to install that with: `sudo apt-get install libncurses5-dev libncursesw5-dev`.

![](img/5019375da05cbf0090115165d80772a1_52_2.png)

- **STEP 8** You may need to keep installing new dependencies, depending on the app. After each new dependency is installed, re-run `./configure` and when it doesn’t report back with an error you can continue to the next stage of the installation. Note: you may need to search online for some error messages.

![](img/5019375da05cbf0090115165d80772a1_52_3.png)

- **STEP 9** With a successful `./configure`, the system will create a `Makefile`. This needs to be ‘made’ by entering: `make` into the Terminal. This may take a while, depending on the size of the app.

![](img/5019375da05cbf0090115165d80772a1_52_4.png)

- **STEP 10** Finally, you need to enter: `sudo make install` into the Terminal. This will install the app, and make it ready for use in the system. When complete you can now execute the app, in this case by entering `vim` into the Terminal or searching for it via the Dash.

![](img/5019375da05cbf0090115165d80772a1_52_5.png)

## Using the Terminal

```text
Kernel command line: block2mtl.block2mtl=/dev/hda2,131072,rootfs root=/dev/mtdbl
cOckO rootfstype=jffs2 init=/etc/preinit noinitrd console=tty0 console=ttyS0,384
00n8 reboot=biOS
Found and enabled local APIC
Enabling fast FPU save and restore... done.
Enabling unmasked SIMD FPu exception support... done.
Initializing CPU#0
PID hash table entries: 32 (order: 5, 128 bytes)
Detected 1991.657 Mhz processor.
Console: colour VGA+ 80x25
console [tty0] enabled
console [ttyS0] enabled
Dentry cache hash table entries: 1024 (order: 0, 4096 bytes)
Inode-cache hash table entries: 1024 (order: 0, 4096 bytes)
Memory: 5112k/8128k available (1497k kernel code, 2624k reserved, 597k data, 196
k init, Ok highmem)
virtual kernel memory layout:
fixmap : 0xffffb000 - 0xfffff000 (280 KB)
vmalloc : 0xc1000000 - 0xffff7000 (1007 MB)
lowmem : 0xc0000000 - 0xc07f0000 ( 7 MB)
.init : 0xc0313000 - 0xc0344000 (196 kB)
.data : 0xc027653c - 0xc030bcf0 (597 kB)
.text : 0xc0010000 - 0xc027653c (1497 kB)
Checking if this processor honors the WP bit even in supervisor mode... Ok.
Calibrating delay using timer specific routine... 4047.64 BogoMIPS (lpj=20238210)
```

![](img/5019375da05cbf0090115165d80772a1_54_0.png)

### Linux Kernel 0.01

```c
/*
 * Copyright Linus Torvalds
 * Based on WRITE-BAKED 838-MODE - Q-51.1
 * Hopefully (this will be a faster complete VTI.01 implementation.
 */

/*
 * 838: The 838-SIM-1324-41-BRIDGE-DRIVER
 */

#include <linux/mod.h>
#include <asm/io.h>
#include <asm/bio.h>
#include <asm/segm.h>

#define SCREEN_DATA 128000
#define SCREEN_END  (0xC600)
#define LINES 25
#define COLUMNS 80
#define SPAM 16

extern void keyboard_interrupt(void);

static unsigned long origin=SCREEN_DATA;
static unsigned long mtr_end=SCREEN_DATA+LINES*(COLUMNS+2);
static unsigned long p0m;
static unsigned long top_i=bottom_LINE;
static unsigned long line_i=LINES*COLUMNS;
static unsigned long state;
static unsigned long npar,nar*(NPAR);
static unsigned long gear;
static unsigned char attr=NOT;
```

Did you know that the first Linus kernel, as programmed by Linus Torvalds, only occupied 65KB of memory? And that since version 0.01, the Linux kernel now boasts over 18 million lines of code. Not bad for a university project that now runs the New York Stock Exchange, and powers the US Department of Defence's fleet of nuclear submarines.

#### DID YOU KNOW...

## Creating a File Using the Terminal

Using the Terminal, you're able to create folders, files and even execute Linux Mint apps. In truth, if you didn't have the GUI at hand, you could still accomplish the same from the Terminal.

### MORE TERMINAL WORK

Creating content using the Terminal isn't quite as strenuous as it may first appear. Yes, the Terminal can look a daunting place for the newcomer, but once mastered it's really quite intuitive.

- **STEP 1** Open up the Terminal, and make sure you're in the Home folder. If not use the **cd** command to return you to the Home folder from wherever you're currently located.

![](img/5019375da05cbf0090115165d80772a1_55_0.png)

- **STEP 2** Let's start by creating a new folder within Home, and call it **Test**. The command you'll need is **mkdir** in **Test**. Press **Enter** to create the folder when you've typed in the command, then **cd /Test** and press **Enter**. This will Change Directory (hence **CD**) to the newly created Test folder.

![](img/5019375da05cbf0090115165d80772a1_55_1.png)

- **STEP 3** Your command line should change to the Test folder and if you enter **ls** (List folder contents) there'll be nothing within the folder, as you've just created it. The **mkdir** command is fairly self explanatory: Make Directory followed by the name of your choosing.

![](img/5019375da05cbf0090115165d80772a1_55_2.png)

- **STEP 4** To create an empty text file, called **Test.txt**, enter in the Terminal: **touch Test.txt**, then use **ls** to view the new file in the folder. Touch is a standard Linux command that allows the creation of files without the need to open a text editor, save the file, then close the editor.

![](img/5019375da05cbf0090115165d80772a1_55_3.png)

## Creating a File Using the Terminal

- **STEP 5** Let's say you now wanted to create a text file. We'll call it **Test2.txt**, complete with some content. To do so, enter: **cat > Test2.txt.** This will create the file **Test2.txt** and put the Terminal into an editing mode.

![](img/5019375da05cbf0090115165d80772a1_56_0.png)

- **STEP 6** You'll notice that the cursor is flashing below the **cat > Test2.txt** command, without the usual prompt. This editing mode will allow you enter the text that the file will contain. Enter some text, then press **Ctrl+D** to exit and write the contents to the file.

![](img/5019375da05cbf0090115165d80772a1_56_2.png)

- **STEP 7** Of course you don't always have to use the Terminal to enter text into a file. Mint comes with a text editor called **Xed**, which is similar to Windows' Notepad. To view the previously created file in Xed, type into the Terminal: **xed Test2.txt**, and press **Enter**.

![](img/5019375da05cbf0090115165d80772a1_56_4.png)

- **STEP 8** Xed is a GUI app, and you can enter text and save the file, or any file, accordingly by using the app's main window; and the **File > Save**, or **File > Save As** functions from its top menu bar options.

![](img/5019375da05cbf0090115165d80772a1_56_1.png)

- **STEP 9** If, however, you prefer to remain working in the Terminal to edit/save/create files, you can use **Nano**. Nano is a simple Terminal-based text editor. To try it with the example, enter: **nano Test2.txt.** There's a menu along the bottom of the screen. To exit and save any content in Nano, press **Ctrl+X** and follow the on-screen instructions.

![](img/5019375da05cbf0090115165d80772a1_56_3.png)

- **STEP 10** We've used the Terminal to launch a Mint app, **xed**, but any app can be launched from within the Terminal. For example, try: **firefox** and press **Enter**. Close Firefox to return to the Terminal. Providing you know the name of the app, it can run from the Terminal. Additionally, entering **firefox** opens Firefox, AND lets you still use the Terminal.

![](img/5019375da05cbf0090115165d80772a1_56_5.png)
