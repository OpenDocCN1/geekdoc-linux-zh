# Peropesis 2.1

**Nate Drake** grapples with the ultra-minimalist Peropesis. Will he relive Linux's glory days, recover a corrupted system or have a breakdown?

+   **IN BRIEF**
+   
+   Peropesis has a tirty footprint and loads into RAM in seconds. Next, master the Linux command line and compile your own programs – if you have the time and patience.

+   **SPECS**
+   
+   **CPU:** 1GHz
+   **Mem:** 256MB
+   **HDD:** N/A (Live only)
+   **Builds:** x86, 64

N ot to be confused with the capital of the First Persian Empire (that's Persepolis), the developers of Peropesis ('personal operating system') say it is "small-scale, minimalis, command-line-based Linux".

How small scale? This distro's ISO weighs in at just 205MB and is designed to run entirely in live mode. The helpful introductory manual on the Peropesis website says the distro is a good way to familiarise yourself with the command line, as well as programs commonly used in Linux.

It also points out that this system can be quickly booted in live mode and is compatible with UEFI and BIOS motherboards. That makes Peropesis perfect for mounting hard drives of faulty systems. A cynic might argue you could do exactly the same by live-booting the latest version of Ubuntu via the terminal and enjoy a quick game of Mines on the desktop as your drives are being rebuilt.

Still, Peropesis has a certain charm. It's entirely distribution-independent, having been written from scratch with open source code. It's also the one and only Lithuanian Linux distro we've reviewed to date. The online manual makes it far less daunting than other command-line-only distros we've encountered. Your first hurdle involves simply entering the root username to log in – no password required.

After this you can navigate the file structure or run one of the few built-in apps. Peropesis includes the Links text-web browser for visiting web pages. Sadly, this isn't to be confused with the Link2 or Lynx browsers, which have limited image support via X11, but it's surprisingly easy to navigate pages via text only. Making good on the earlier claim, the manual also covers how to use Peropesis to mount an external USB drive and use **chroot** to recover a faulty Linux OS.

On login, you may also notice the message saying 'No New Mail'. This is thanks to the S-nail mail client. As this again can only be accessed via the command line, you need to edit the ~/.mailrc yourself to add your credentials. Peropesis supports the cat, nano and ed commands for viewing and editing files. You can also navigate directories via pwd, ls and cd. We used these to list the contents of /bin to see what other programs come preinstalled. Luckily, Peropesis supports both the man command and --help flag if you see anything unfamiliar.

If you want to install any further programs, there's no package manager. This means you have to use wget to download the tarball of your chosen program, extract it via the command line and run configure and install. This will probably turn off Linux newcomers who are used to a colourful software centre.

Still, you may not have much of a choice if you want to boot the ISO on a system that uses proprietary firmware. The Peropesis manual cautions that the distro only includes a small amount of firmware but also shows you how to view system logs to check that the correct software is installed. The Peropesis forum (https://peropesis.org/forum) has a lively discussion on this topic, with users suggesting a more visually friendly package manager like Pkgsrc may be in order. Visit https://peropesis.org/bundle/ to see a full list of updates to the latest version of Peropesis. These include support for the Perl programming language (Python is notably absent, however!). There are also new versions of Autoconf, Automake and GCC to make compiling your own programs easier.

Officially Peropesis is in the open beta development stage, but we plan to keep an eye on it in future.

![](bbox=[0.46, 0.24, 0.91, 0.44])

**VERDICT**

**DEVELOPER:** Gediminas Mockus and the Peropesis team **WEB:** https://peropesis.org
**LICENCE:** CC BY-SA 4.0

| | **FEATURES** | **3/10** | **EASE OF USE** | **6/10** |
|---|---|---|---|---|
| | **PERFORMANCE** | **9/10** | **DOCUMENTATION** | **9/10** |

Peropesis introduces users to commands and the file structure of the Linux OS. It also boots in record time.

**Rating 7/10**