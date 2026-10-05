# System optimization

Information on updates for fixing bugs and security gaps can be found on the Internet at the following address:

http://www.redhat.com/support/docs/errata.html

Many RedHat CDs, the update packages listed there are included with the distribution (usually in the updates directory), provided they were available at the time of pressing the CD.
Obviously, you only need to carry out an update if you have installed the affected package. You can easily find this out with `rpm -q` name. The command for an update is simply `rpm -U file.rpm`.

# Configuration details

In principle, you now have a functioning Linux system. However, some minor modifications are needed. The following measures recommendations (in the author's opinion) significantly improve working comfort with RedHat Linux. However, extent to which you want to follow these recommendations is obviously left to you. (Even more configuration hints and tips are included in Chapter 6.)

# Default desktop

The default desktop system is GNOME. Alternatives (provided they are installed) 'Another Level' known from earlier RedHat versions (a complex window menu) and KDE. To set the default system, you simply use the switchdesk program, which modifies the file `~/.clients` or `~/.clients-xxx`.

# Keyboard focus in new windows

If you use GNOME with the window manager Enlightenment (this is the default setting), you will probably be irritated by the fact that new windows do not automatically receive the keyboard focus. To remedy this nuisance, you start the GNOME control center gnomecc and click the button RUN CONFIGURATION TOOL FOR ENLIGHTENMENT the dialog sheet DESKTOP:WINDOW MANAGER BEHAVIOR option ALL NEW (POPUP) WINDOWS GET THE KEYBOARD FOCUS. In the Enlightenment configuration dialog you will also find a number of other practical setting options.

# Emacs special keys

In GNU Emacs, functions in the same way as Backspace. The following file `~/.emacs` corrects this misbehavior:

```
; (global-set-key [delete] 'delete-char)
(global-set-key [home] 'beginning-of-line)
(global-set-key [end] 'end-of-line)
```