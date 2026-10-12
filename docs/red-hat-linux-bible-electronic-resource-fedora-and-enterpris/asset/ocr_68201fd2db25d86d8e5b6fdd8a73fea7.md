# Choosing an audio CD player

The player that pops up automatically when you insert a CD (on the GNOME desktop) is the gnome-cd player. However, several CD players that come with Red Hat Linux can be used to play CDs. Here are your choices for playing CDs with Red Hat Linux:

+   • **CD Player (gnome-cd)** — This is the default CD player for the GNOME desktop. Besides having standard play buttons, this player lets you get track information automatically from a CD database (such as freedb.org). Or, if your CD isn't listed in the database, you can enter your own track information manually.

+   • **KsCD Player (ksCD)** — The KsCD player comes with the KDE desktop. To use KsCD, the kdemultimedia package must be installed. From the Red Hat menu (KDE desktop), click Sound & Video → KsCD (or type ksCD from a Terminal window). Like gnome-cd, this player lets you get title, track, and artist information from the CD database. KsCD, however, also lets you submit information you type in yourself to a CD database (if your CD isn't found there).

+   • **Grip (grip)** — While the Grip window is primarily used as a CD ripper, it can also play CDs. Click Sound & Video → More Sound & Video Applications → Grip. It includes tools for gathering data from and submitting data to CD databases. It also includes tools for copying (ripping) CD tracks and converting them to different formats (encoding). (The grip package must be installed to use this command.)

+   • **CDPlay (cdp)** — If you don't have access to the desktop, you can use the text-based cdp command. This player lets you use keyboard keys to play your CD, select tracks, go forward or back, or eject. (The cdp package must be installed to use this command.)

+   • **X Multimedia System (xmms)** — The xmms player plays a variety of audio formats, but can also play directly from a CD.

If you prefer to use one of these players, you can disable automatic startup of gnome-cd by disabling automatic play in your CD Properties window (as described in the next section). The gnome-cd and cdp CD players are then described.

> NOTE: If you try some of these CD players and your CD-ROM drive is not working, see the sidebar "Troubleshooting Your CD-ROM" for further information.

# Automatically playing CDs

When you put an audio CD into your CD-ROM drive, a CD player automatically pops up on your desktop. If you are using the GNOME desktop, you can thank magicdev. The magicdev process monitors your CD-ROM drives and opens a CD player when it sees an audio CD.

The fact that inserting a CD starts a player automatically is nice to some people and annoying to others. If you just want the CD to play, this behavior is a good thing. However, if you want to choose your own CD player or not play the CD until you choose, you may find auto-playing