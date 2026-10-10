# ## Using Vi Modes

At any given moment, Vi is running in one of three modes:

**Command mode**\hfill This mode accepts commands, which are usually entered as single letters. For instance, i and e both enter edit mode, although in somewhat different ways, as described shortly, and o opens a line below the current one.

**Ex mode**\hfill To manipulate files (including saving your current file and running outside programs), you use ex mode. You enter ex mode from command mode by typing a colon (:), typically directly followed by the name of the ex mode command you want to use. After you run the ex mode command, Vi returns automatically to command mode.

**Edit mode**\hfill You enter text in edit mode. Most keystrokes result in text appearing on the screen. One important exception is the Esc key, which exits from edit mode back to command mode.

![](bbox=[0.12, 0.39, 0.2, 0.445])

If you're not sure what mode Vi is in, press the *Esc* key. This will return you to command mode, from which you can reenter edit mode, if necessary.

![](bbox=[0.12, 0.475, 0.2, 0.54])

Vi terminology concerning modes is inconsistent. Ex mode is sometimes called *line mode* or *command-line mode*, and edit mode is sometimes referred to as *text mode*. Some sources don't refer to ex mode as a separate mode at all, but instead refer to extended commands or use similar terms.

# ## Editing Text

As a method of learning Vi, consider the task of editing /boot/grub/menu.lst to add a new kernel. (Some distributions call this file /boot/grub/grub.conf.) Listing 3.4 shows the original menu.lst file used in this example. If you want to follow along, enter it using a text editor with which you're already familiar, and save it to a file on your disk.

# #### **Listing 3.4**: Sample /boot/grub/menu.lst File

```
```plaintext
default=0
timeout=10
splashimage=(hd1,5)/grub/splash.xpm.gz
title Fedora 10 (2.6.28)
    root (hd1,5)
    kernel /bzImage-2.6.28 ro root=/dev/sda4 rhgb
    initrd /initrd-2.6.28.img
```
```