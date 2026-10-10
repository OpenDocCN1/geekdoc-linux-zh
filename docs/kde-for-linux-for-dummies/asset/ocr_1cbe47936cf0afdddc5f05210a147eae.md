This is where KDE comes in. We won't tell you that KDE tools make it as
simple to run a Linux system as it is to run an iMac, because that's not true.
You have much more control over the **operating system** in a Linux environ-
ment than you do over the Macintosh operating system. More control means
more effort, in computing as in life. This chapter provides you with two
things: an understanding of the administrative tasks you have to perform
because you're running Linux and a guide to the KDE tools that make those
tasks a little easier.

# # The Multiuser Environment

The key concept to keep in mind as you work with your Linux machine is that
you're in charge of a *multiuser environment*. Linux provides a way for several
people — or one person pretending to be several people — to use a single
computer. Users share the applications and system resources, but each indi-
vidual account is private and has its own storage area. The system adminis-
trator can see what the users are doing or what they've stored on the hard
drive, but users can't see anything related to other users' activities. Oh, the
power! Oh, the possibilities!

When you installed Linux on your system, you created a special account
called *root*, and you probably also created a personal account for yourself. As
soon as you completed those account creations, you had a multiuser system.
Yep, as easy as that! Yes, you're both root and trixie-belle, but your computer
doesn't know that. Your computer sees the two as separate entities, and
gives root complete access to everything on the machine, but requires trix-
ie-belle to follow the rules.

As you go through this section, remember that the multiuser information
applies to you even if you are the only human using your machine. Because
you have access both to root and to your user account, you have multiuser
concerns as much as if you also created accounts for your partner or room-
mate. If you do have other users on your machine, you have some interper-
sonal concerns as well. Those are mentioned later in the chapter, and there
are some ideas about being a good system administrator as well as a good
friend.

> Let's talk for a moment about root. That root account you created for your-
> self is pretty darn special. Any time that you need to make changes to your op-
> erating system, you likely need to do them as root. Root has access to all files
> on the system — even the personal ones in user accounts — and root can run
> any program; even the programs that will completely destroy your computer.
> Using your root account for day-to-day business is a bad idea. Use your user
> account for everything you'd usually use your computer to do. If you need to
> do something as root, you can log in specially to take care of the issue, and
> then log back out.

![](bbox=[0.12, 0.8, 0.22, 0.86])