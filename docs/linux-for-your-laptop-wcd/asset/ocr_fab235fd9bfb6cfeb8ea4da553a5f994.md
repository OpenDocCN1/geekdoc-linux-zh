```
D 0 Wed Jun 9 21:12:34 1999
D 0 Wed Jun 9 21:12:34 1999
RingCentral Fax.lnk A 364 Sat Jul 31 10:15:54 1999
cerols.DKN A 816 Tue Dec 7 12:15:06 1999
Register.lnk A 363 Tue Dec 7 11:51:46 1999
My Briefcase DR 0 Wed Jun 9 21:12:46 1999
Netscape Navigator.lnk A 583 Tue Dec 7 12:22:18 1999
Rio Manager.lnk A 403 Wed Jun 9 23:05:00 1999
MusicMatch Jukebox.lnk A 493 Wed Jun 9 23:05:30 1999
Netscape Communicator.lnk A 583 Wed Jun 9 23:54:56 1999
AOL Instant Messenger (TM).lnk A 586 Wed Jun 9 23:55:06 1999
RealPlayer G2.lnk A 421 Wed Jun 9 23:55:38 1999
explore2fs-1.00-pre2.zip D 325902 Sat Nov 13 11:24:08 1999
vmc D 0 Wed Nov 10 04:08:04 1999
WinZip.lnk A 385 Wed Nov 10 11:07:26 1999
eBowl.exe A 1130496 Thu Nov 18 17:05:52 1999
ext2fs D 0 Sat Nov 13 11:13:10 1999
Shortcut to dball on Green.lnk A 274 Sun Jan 16 11:39:36 2000
linuxdir_167.exe A 7213 Tue Nov 30 23:54:54 1999
fase.snd A 684032 Wed Jan 26 17:46:46 2000
ar D 0 Tue Dec 14 17:16:44 1999
mail.1.14.00 D 0 Sun Jan 16 11:40:16 2000
```

65505 blocks of size 32768; 18814 blocks available

smb:\\windows\desktop>

Use the `mget` command followed by a file name to retrieve a file from the Windows desktop to the current Linux directory:

```
smb:\\windows\desktop> mget explore2fs*
Get file explore2fs-1.00-pre2.zip? y
getting file explore2fs-1.00-pre2.zip of size 325902 as explore2fs-1.00-pre2.zip
(298.559 kb/s) (average 298.559 kb/s)
smb:\\windows\desktop>
```

Use the `mput` command followed by the name of a file in the current Linux directory to send it to the Windows desktop:

```
smb:\\windows\desktop> mput Linuxdocument.txt
Put file Linuxdocument.txt? y
putting file Linuxdocument.txt as \\windows\desktop\Linuxdocument.txt (13.0673 kb/s)
(average 13.0673 kb/s)
```