
Here are suggestions for creating a menu item and adding a desktop icon:

+   To create the menu item, edit /etc/ske1/.fluxbox/menu and /etc/ske1/.jwmrc. Because Zile is a console-based program and its path is /usr/bin/zile, our menu line item to be added looks like this:

```
[exec] (Zile) {aterm -e /usr/bin/zile}
```

+   The icon for Zile in /etc/ske1/.xdesktop/zile.lnk looks like this:

```
table Icon
Type: Program
Caption: Zile
Command: aterm -e /usr/bin/zile
Icon: /home/dsl/.xdesktop/program.png
X: 420
Y: 384
end
```

> NOTE
> I am using one of the generic icons available in DSL. Other generic icons are binary.png, gear.png, and shellscript.png. You may change the icon later by right-clicking the displayed icon. See Chapter 4, “Configuring and Saving DSL Settings,” for details.

## Removing Applications

Because DSL is extremely small in size and is not pure Debian, core applications are usually removed by force. This usually implies using the find command to locate all related files. Often, the command ldd is used to display all the dependent libraries used by an application.

Still, the process of removing an application can be quite daunting. DSL’s compact and denseness is the result of much hacking code. For example, one of the common applications that many want to remove is Firefox. Using the standard approach, find / -name firefox does not reveal all that was used for Firefox in DSL. There are Firefox references in configuration files. The system configuration for unionfs contains references to Firefox. The file at /etc/init.d/mkunion needs to be cleaned of the Firefox references. From this example, you can see that to unravel DSL, dense and compact size can be a challenge.

## Other Customizations

Other features you may want to customize include passwords, themes and backgrounds, default time zones, DSL-specific features, and the default desktop.

### Setting Passwords

You should always use the chroot method if you want to change passwords. Then, issue the standard command to perform this action.

```
# passwd
Changing password for user root
Enter the new password (minimum of 5, maximum of 8 characters)
Please use a combination of upper and lower case letters and numbers.
Enter new password: (Password entered will not be displayed)
Re-enter new password: (Password entered will not be displayed)
Password changed.
```

### Themes and Backgrounds

The standard theme for DSLs Fluxbox desktop is /usr/share/fluxbox/styles/default. This is actually a link to the current default theme, envane. The background image is actually specified in the theme. In DSL, you typically use the Fluxbox rootCommand tag to specify the image. The default images available for Fluxbox are located at /usr/share/fluxbox/backgrounds.

> NOTE
> When using the direct method, always prefix the actual paths with source/KNOPPIX.

### Language

The default language, currently us, can be supplied as a boot option (lang=it) or by editing line 95 of the standard KNOPPIX script at /etc/init.d/knoppix-autoconfig.

```
95 [ -n "$LANGUAGE" ] || LANGUAGE=us
```

### Default Timezone

The default timezone is related to the language selection inside the knoppix-autoconfig script. Between lines 97 and 340, you can find one very large case statement. This case statement assigns basic time and language settings, based on the language that is currently set. Depending on language selection, you can also change the default timezone. For example, language en specifies a timezone of US/Eastern. This is where you can change it, for example, to US/Pacific.

### DSL Specific

Just as KNOPPIX uses a bash script from most of the boot time configurations, so does DSL. The script is located at /etc/init.d/dsl-config. Many boot options can be found here. This is where the processing of boot time MyDSL extensions occurs. It is where many of the daemon requests are processed. Most options unique to DSL are in the master boot time configuration file.

### Default Desktop

The default desktop can be supplied as a boot option (for example, desktop=jwm) or by editing the script at /etc/init.d/dsl-config line 240. This line, as it is set by default, sets the default desktop to fluxbox, if jwm isn’t specifically identified (probably from a boot option):

```
240 case "$DESKTOP" in fluxbox|jwm) ;; *) DESKTOP="fluxbox"; ;; esac
```

## Advanced Customizations

More advanced DSL customizations can be used to directly modify the DSL boot process itself. This can include changing Isolinux boot loader files (such as boot screens and options), as well as modifying the initial ramdisk used when DSL first boots.

### Boot Screen and Initial Boot Options

Using the preceding remastering setup, the initial boot files for image, message, and default boot options are located at master/isolinux relative to your mount point and working remaster directory. The following three files are of interest:

- **isolinux.cfg**: This is the configuration file for the Isolinux boot loader. It specifies the image to be displayed, the boot message, and all of the default boot options, as well as several boot images to load. This is a simple text file and may be edited with any text editor.

- **boot.msg**: This is the initial displayed text that appears before the boot prompt. Again, it is a simple text file and any text editor can alter its contents.

- **logo.16**: This is the image shown on the initial boot screen. This image file must be of the LSS16 image format. This is a 16-color, 640×480 image.
