```
GRUB_DEFAULT=0
GRUB_HIDDEN_TIMEOUT=0
GRUB_HIDDEN_TIMEOUT_QUIET=true
GRUB_TIMEOUT="10"
GRUB_DISTRIBUTOR='\`lsb_release -i -s 2> /dev/null || echo Debian\`
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
GRUB_CMDLINE_LINUX=""

# Uncomment to disable graphical terminal (grub-pc only)
#GRUB_TERMINAL=console
...
```

You can assign values to the following variables:

# GRUB_DEFAULT=num | saved

The *num* specifies the ordinal number of the default menu entry. Menu entries are numbered starting with 0, so setting this variable to 0 specifies the first menu entry. The default menu entry is the one GRUB boots if you do not select a different entry as GRUB boots the system. Setting **GRUB_DEFAULT** to *saved* causes GRUB to boot the most recently booted menu entry.

# GRUB_HIDDEN_TIMEOUT=num

The *num* specifies the number of seconds GRUB waits with a blank screen (the menu is hidden---thus it is called a *hidden timeout*) or displays the image you specify in */etc/grub.d/05_debian_theme* (page 587) before booting the system. Setting *num* to 0 causes GRUB to pause just long enough so that if the user is holding down the SHIFT key as the system boots, GRUB displays its menu. GRUB ignores this variable on systems with more than one bootable system.

# GRUB_HIDDEN_TIMEOUT_QUIET=true | false

Specifies whether GRUB displays a countdown timer during a hidden timeout (see **GRUB_HIDDEN_TIMEOUT**). Set to *false* to display the timer or *true* not to display the timer.

# GRUB_TIMEOUT=num

The *num* specifies the number of seconds GRUB waits before booting the system. Set *num* to -1 to cause GRUB to wait until the user selects a menu item. Setting *num* to 0 causes the SHIFT key to lose its effect: The user will not be able to display the GRUB menu before the system boots.

# GRUB_DISTRIBUTOR=string

The *string* specifies the name of the distribution as displayed by GRUB. The *string* as supplied with Ubuntu is executable and is replaced with its output because it is enclosed within back ticks (command substitution; page 362):

```
\`lsb_release -i -s 2> /dev/null || echo Debian\`
```

With the -i and -s options, **lsb_release** sends the string *Ubuntu* to standard output. Standard error is discarded (2> /dev/null) and, if **lsb_release** fails, the string *Debian* is sent to standard output.