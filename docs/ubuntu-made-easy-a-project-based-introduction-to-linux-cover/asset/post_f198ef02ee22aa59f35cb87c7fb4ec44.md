
LoCos tend to cover large geographic areas, normally on the scale of whole countries or states. As such, they tend to meet in less regularly, although many LoCos-related events throughout the year, including "launch parties" around the time of each Ubuntu release. You can find a list of LoCo teams at http://loco.ubuntu.com/teams/. Lugs are much more widespread than LoCos and tend to put a greater emphasis on meeting up. Typically, a LUG will hold regular meetings in a local community center (a pub, if you're lucky) and might organize talks or other Linux-related activities. The best way to find your nearest LUG is to use Google.

## Stickers and Other Goodies

If you have a penchant for showing off your Ubuntu addiction, you're in luck! Free stickers are available from Ubuntu-friendly computer manufacturer system76, and they're just great for replacing the unsightly Windows logo that you probably have hiding somewhere on your computer's case (see Figure 21-13). To order, browse to https://www.system76.com/community/stickers/ and send a stamped, addressed envelope to the relevant address on that page. No club would be complete without a membership badge, would?

![](img/d35fa962e6f9664d66dc83916f426418_406_0.png)

Figure 21-13: My laptop, complete with Ubuntu sticker (I couldn't remove the Windows one)

If stickers leave you cold, other Ubuntu-branded goodies (mugs, T-shirts, backpacks . . . you name it) are available for purchase through the Canonical store (http://shop.canonical.com/).

## Getting Involved

Lots of people enjoy being part of the Ubuntu community and want to give something back by volunteering to help. Reporting bugs is a great way to make a contribution, but that's only the start of it!

If you talk to existing contributors, you'll soon see that everyone's story is different. I stumbled into contributing to Ubuntu in early 2006, when I started tidying up some bug reports that were missing information. It was something to pass the time and took up half an hour per day. This was when Launchpad was new and all the bugs were being transferred from the system, the work was pretty fun. The members of the Bug Squad were incredibly encouraging, and soon I found myself spending more and more time doing Ubuntu stuff. As time went on, I started editing pages on the wiki (https://help.ubuntu.com/community/) and eventually found my way to the Documentation Team, where I coauthored a guide on switching Windows to Ubuntu. Now I'm one of the maintainers of the “upstream” help files at the GNOME project, among other things. Being a contributor has been a great experience—I've met tons of interesting people, indulged my interests in writing and computers, traveled to conferences around the world, and, most importantly, had tons of fun in the process.

Browse to https://www.ubuntu.com/community/ to get some ideas how you might be able to help. You don't need to be a geek to get involved: Artists, writers, multilingualists, marketers ... the list of ways to participate goes on. You might even like to attend a conference and have as much fun as the contributors in Figure 21-4! To start, all you need to do is join the relevant team and introduce yourself on its mailing list. If you are interested, one thing in particular that you should look out for is Ubuntu Open Week, or check https://wiki.ubuntu.com/UbuntuOpenWeek to see when the next one will be.

## Ubuntu Accomplishments

If you're not sure how to get involved, or whether involved is the right thing for the first place, you might like to try out a new app called Ubuntu Accomplishments (Figure 21-15). Intended to help you find a way to get involved with Ubuntu, it works a bit like a game. You start out completing one or two relatively simple community-oriented tasks, like getting a Launchpad account (as you already learned how to do) in “Passport to the Ubuntu Community”. For each task complete, you're awarded a trophy (a digital one, don't expect any engraved plaques through the mail), so you can flaunt your achievements. As you earn more trophies, other “levels” are unlocked, giving you access to more tasks that can earn you more trophies. Each task comes with instructions on how to complete it, so you learn how work as you go. In the process, you explore the Ubuntu community, contribute to a little, and have some fun at the same time. And even if you ultimately decide that Ubuntu isn't your cup of tea, you'll be left with a trophy or two for your troubles.

![](img/d35fa962e6f9664d66dc83916f426418_408_0.png)

You can find more information about Ubuntu Accomplishments, including installation instructions, at https://wiki.ubuntu.com/Accomplishments/. It's still in development as this book goes to press, so there are a few rough edges here and there. In particular, some of the tasks are quite technical in nature. But it's still worth trying it out—go get those!

| Accomplishment information | | | | |
|---|---|---|---|---|
| My Trophies Opportunities | opportunities for everything | Show Locked | | |
| Accomplishments Contributor | Approved Ubuntu Member | Attend LoCo Team Event | Bug Control Member | Bug Squad Member |
| Community Council Member | Filed bug was Confirmed | First Bazaar Branch Merged | Fridge Editor | Imported an SSH Key |

Figure 21-15: Gain a sense of achievement by finding ways of contributing to Ubuntu.

# 22

# WOUNDED WINGS

## Fixing Common Problems

![](img/d35fa962e6f9664d66dc83916f426418_410_0.png)

The purpose of this chapter is to arm you with some general-purpose tips, tricks, and troubleshooting hints. You'll find step-by-step instructions on how to fix several specific problems, but for the most part I need to keep the discussion general. This is because the way you resolve some issues will depend heavily on the peculiarities of your setup, and there isn't big enough a guide that covers every possible eventuality in suitable detail. Fortunately, the Internet harbors a sizable collection of Ubuntu-related guides, so even if you don't arrive at the exact answer you were looking for, I hope you'll be able to use some of my tips.

If you've run into a problem, flip through this chapter to see whether there's anything that might help. I've covered problems with installation, booting, sound and video, Internet and network connections, hard disks and storage, displays graphics cards, with pesky software issues as freezing or slowing down your computer. If you're not bothered by any particular quandary, you might like to skip through this chapter: Make yourself a hot beverage and head back to the games for some R&R.

## I Can't Get Ubuntu Installed

Not being able to install Ubuntu is a particularly unhappy problem because it means you've denied all fun from the previous 21 chapters of this book! Never fear; there's plenty you can convince Ubuntu to install on your computer, and if you're still struggling, you can try alternative installation methods like booting from a USB stick, or Appendix A.

## My Computer Won't Boot from the CD

If you tried to start your computer from the Ubuntu installation CD but never even got to the purple boot screen (see "Going for a Dip" on page 12) or the computer just boots into Windows every time, one of the following:

- Check the boot order. When your computer starts up (boots), it goes through a list of devices in a set order, checking to see whether they have an operating system on them. As soon as it finds an operating system, the computer will boot from that device, and it won't check any of the other devices. This means if the hard disk comes before the CD drive in the boot order, the computer will boot from the hard disk rather than the CD drive. To boot from the CD, you need to make sure that the CD drive comes first in the boot order. See "Going for a Dip" on page 12 for instructions on setting up the boot order correctly.

- Check the integrity of the CD. You could have a faulty or damaged CD that your computer isn't able to boot. It's possible to check whether a disc has faults on it by doing a checksum test. A checksum is a sort of fingerprint; you the checksum of your Ubuntu CD and compare it with the checksum of an Ubuntu CD that is known to be free of faults. If there is but one tiny difference between the two discs, the checksums will be different too—the "prints" won't match. Ubuntu uses the MD5SUM program to do its checksums. Go to https://help.ubuntu.com/community/MD/ and scroll down to the "MD5SUM on Windows"
