# Printing with SuSE Linux
CHAPTER 24

(such as irda-utils-0.9.4.tar.gz) from http://www.cs.uit.no/linux-irda/irda-utils/. Module support must be enabled for your kernel. (See Chapter 23.)

The basic steps to enable infrared inloading, building, and installing the Irda
distribution. You then need to create appropriate entries in your system's /etc/
conf.modules file and create the infrared device(s).

After you have installed the software and configured your system, the easiest way to say,
print to an infrared printer is to create a special entry in your /etc/printcap printer
database or to use a filter program, such as APSfilter (mentioned earlier). Laptop users
need to depress certain function keys to disable an existing serial port or to enable an IR
port, and you may need to use the setserial command to assign IRQ values to the Irda

# Some Program Tips

The following are some tips to help you print documents or set up applications for easier
printing.

# emacs

Want to print directly from GNU emacs? If you use emacs on the console or in text-only
mode, you can print the entire buffer, unformatted or formatted, by pressing Esc+X, typing
lpr-buffer, and pressing Enter. Alternatively, you can set the lpr-switches variable in your .emacs file to
 press Enter. Just make sure you set the point to the correct printer in your /etc/printcap file. If you use GNU emacs with X11,
select the Tools menu and then click the Print or (if you have selected text) Print Region
menu items (XEmacs users will find the Print option under the File menu or can use the
Print icon in the Emacs toolbar).

![](bbox=[0.833, 0.611, 0.961, 0.804])

# WordPerfect 8 for Linux

Thanks to Corel, nearly one million Linux users are happily enjoying Core’s
free-for-personal-use edition of WordPerfect 8 for Linux.

> Note
You can register and download a copy of WordPerfect 8 for Linux from http://
linux.corel.com/linux8/download.htm.