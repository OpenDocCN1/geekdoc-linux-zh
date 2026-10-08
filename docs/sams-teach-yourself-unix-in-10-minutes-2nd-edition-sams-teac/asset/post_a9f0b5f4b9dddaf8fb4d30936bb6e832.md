
you simply shut off the power to a Unix machine, you interrupt all these processes, and probably destroy any files they were working on at the time. This happens often, and it is another reason why it's important that commands like these are restricted to the proper users. Haphazardly shutting the power to a Unix machine has the potential to completely corrupt the drives, leaving the system unusable. Be careful if you use this command at work. If you are working in your lab, then have fun, and try to create problems that you can use single-mode and fsck to fix it.

The shutdown command and a reboot command have obvious benefits. These two commands gracefully exit all running software, write out disk cache information to the drives, and complete their respective tasks. They are restricted to the root user for obvious reasons.

# Summary

In this lesson, you were introduced to root level commands that if not used properly could cause serious problems. However, if these commands are mastered and practiced, they can help you in a great ways that this 10-minute lesson could never cover in this page count. Make sure that if any of these commands interest you, and you want to progress on further this book, set up a Unix or Linux system at home or in a lab somewhere and practice! It is truly the only way to get good at this, specially something as cryptic as Unix. You need to practice and read more.

To tie the book, I would personally like to wish you the best in your Unix beyond this point. I hope you enjoyed this book and that you learned enough to get to the next level. Let me know at rshiminsonki@rsnetworks.net or visit me on the web at http://www.rsnetworks.net. It truly has been a pleasure to teach you the fundamentals of Unix. The following is a review of some of the other points from this lesson:

- Never touch a machine if it looks like it's running a root shell. Root is powerful and should only be used by experienced users and system administrators.
- Never ever turn the power to your machine off without permission from your administrator. If you've got a shutdown button on your machine, pretend it doesn't even exist.
- Root (administrative users) can change ownership of files for you, but consider whether it's really necessary or whether a copy will do.

# APPENDIX A
Learn More About Unix: Reference

Now that you are familiar with the operation of Unix, you can continue to learn more by visiting online resources. The Internet is an excellent resource to find information on Unix and Linux. I hope that this list is a gateway to the endless sea of what is out there. Make sure you continue your studies with Unix and practice as much as possible. Remember, the more you practice, the easier it gets. As soon as you know the commands cold, your control of Unix strengthens. I have also included some websites of Unix and Linux vendors; most have helpful tutorials and online documentation. These websites offer valuable information for specific operating systems. For example, if you were running Sun Solaris and needed to know Unix-based commands that may be specific to that operating system, you would want to visit the Sun website (http://www.sun.com). I also provided a few links to Linux vendors who sell inexpensive operating systems that are full-blown versions of Linux. Linux is similar to Unix, so if you can manage Linux, install it and practice as much as you can; your mastery of Unix will come quickly. In addition to reading a book like this, you can find more information on the following websites:

Unix Reference:

- http://www.freebsd.org/
- http://www.ugu.com/
- http://www.unix.org/
- http://www.sco.com/
- http://www.unixreview.com/

Linux Reference:

- http://www.tldp.org/
- http://www/slashdot.com/
- http://www.linux.com/
- http://www.linuxjournal.com/
- http://www.linuxquestions.org/
- http://www.novell.com/linux/
- http://www.redhat.com/
- http://www.google.com/linux

General Reference:

- http://www.rsnetworks.net/masterunixquickly/
- http://www.gnu.org/
- http://blackboxwm.sourceforge.net/

This page intentionally left blank

# INDEX

# SYMBOLS

$ , end-of-line regular expression, 164
$PWD environment variable, 169
$USER environment variable, 164
& (ampersand), running applications in background, 33, 138

* (asterisk) regular expression, 160-161
[brackets], 162-163
^ (caret), start-of-line regular expression, 164
.(period) dot files, 190
regular expression, 160-161
| (pipe), 155-156
~ (tilde), home directory, 52
-f option, 58
rm command, 81
-r option, 58
dvi extension, 197
.ps extension, 197
.hosts file, 205
tr extension, 197
xinitre, 132
creating, 34-35
name variations, 32

all option, displaying hidden data, 58
altering modification dates with touch, 78
anchors, 164
appending output to text files, 154
running in background, 33
starting with .xinitre, 32-35
window placement, 36
apro, 23
archives, case sensitivity, 58
arrays, 171
attachments (euclid), encoding, 134-135
attributes, 49-50
automating processes, crontab, 145
absolute file paths, 91
absolute path statements, 61-62
accessing, 17
activating KDE, 64
AfterStep, 42
alias command, syntax, 187
alias, 187
background processes, 138
backing up data, 144
batch command, 138
bit mask, set file, 215
Blackbox, 43
booting in single-user mode, 221-222
Bourne shell, 12
Bourne-again shell (BASH), 12, 34
built-in (KDE), 111
built-in help system, 16
info help format, 18
apropos command, 23
displaying, 18
man pages, 20
versus other resources, 19
whatis, 21-22
built-in KDE Editor, 111
bzip utility, 131
C-shell, 12, 17
case sensitivity, 4, 13, 58
of user accounts, 5
cat command, 95-96
chsh, 175-177
cp, 129
cursively, 86-87
copying files, 85
copying multiple files, 85-86
cron, 138, 145
Ctrl+c, 14
Ctrl+d, 14
Ctrl+z, 15
date, 182
df, 126-127
diff, 117-118
du, 127
executing in current directory, 189
find, 66-67, 126
locating files, 68
with popd command, 60-61
pushd command, changing directories, 60-61
passwords, 177
file system integrity, 222-223
print job status, 198-199
chfn command, 181-182
chmod command, 217
syntax, 216
choosing pathways, 178
chsh command, 175-177
command line, 6
command mode (vi editor), 104
commands. See also processes
geometry, 34
-help, 24
alias, syntax, 187
apropos, 23
arguments, case sensitivity, 58
atc, 146
bg, 138
built-in help system, viewing, 24
cat, 93-96
cd, 59-60
fsck, 222-172
head, 100
if, 173
jobs, 160
kill, 142
less, 98-99
in, 89-90
logout, 9
lnpq, 198-199
syntax, 197
lprm, 199-200
is, 19, 52, 126
options, 58
output, deciphering, 55-57
man, 21-22
man -k, 23
mkdir, 82-83
ore, 97
mv, 87-89
output, paging through, 78
password, 177
patch, 118
popd, 60-61
ps, 140
pushd, changing directories, 60-61
pwd, 31, 59
zip, 129
reboot, 223-224
recalling, 2
rlogin, 204-206
rm, 79-81, 84-85
rmdir, 83
root-level, 219
shutdown, 223-224
similarity to Windows commands, 60
slogin, 206
split, 116
ssh, 203-204
su, 221
sudo, 221
summaries of, 24
switches, 22
tail, 99
top, 14
uncompress, 129
utptime, 37
whereis, 70
which, 71
who, 183
gzip command, 129
zip command, 130

#AMS TEACH YOURSELF IN 10 MINUTES
