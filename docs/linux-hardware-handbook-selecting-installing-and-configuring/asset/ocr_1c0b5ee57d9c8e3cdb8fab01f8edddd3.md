# ## Power Management Software

Notebook computers come with nickel-cadmium (NiCd), nickel metal hydride (NiMH), or lithium ion (LiOn) batteries. As a general rule, NiCd batteries aren't used on modern note-books, although you might find them on older models. Today's low-end models generally use NiMH batteries, whereas higher-end devices use LiOn batteries. LiOn batteries have higher capacities and suffer less from "memory" effects than do NiMH batteries.

> **CAUTION**
> There's little standardization in notebook computer batteries. A battery designed for one computer usually doesn't work in another. The main exceptions are in closely related computers from the same manufacturer.

In order to make batteries last as long as possible, most notebook computers implement a number of power-saving features. These features generally require communication between the hardware and the OS, and these features are often mediated by the BIOS. In Linux, they're implemented through the *Advanced Power Management Daemon* (APMD) package. The main APMD site for Linux is http://www.worldvisions.ca/~apemwar/ apmd/ .

# ## Linux Kernel Options

APMD requires a number of kernel options to function properly. You can activate these options in the General setup kernel configuration menu. Specific options you should consider include

+   - **Advanced Power Management BIOS support**  This option is required. Without it, none of the other options are available.
+   - **Enable PM at boot time**  Responding Y to this option enables most power manage-ment features. For instance, with this option enabled, the computer enters a power-saving sleep mode after a certain period of time.
+   - **Make CPU idle calls when idle**  This option can sometimes improve power savings slightly, by putting the CPU in a low-power mode if it's not been used for a while.
+   - **Enable console blanking using APM**  If you regularly work in text mode, enable this option. It tells the system to blank the screen using APM BIOS calls, which can save battery power. If you don't enable this option, the screen goes blank, but it's still powered.