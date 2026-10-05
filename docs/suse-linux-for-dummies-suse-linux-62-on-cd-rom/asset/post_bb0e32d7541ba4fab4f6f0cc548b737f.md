
# 282 Part VI: The Part of Tens

Likewise, I use Appligare Presentation Editor to make presentations about Linux on Linux. When I am talking about Linux at a show or a convention, I can demonstrate what I am talking about using X Window System while I have the presentation slides on the screen. If I used Microsoft PowerPoint, I would have to reboot the system into Linux to do the demo, an awkward approach at best. Appligare has many of the same facilities as Microsoft products. Recent editions of Appligare can read and create PowerPoint output, and now I can run my system truly FAT-free.

## Visit Web Sites

You have a variety of Web sites available for help. Some of these sites provide technical information, some provide news of the Linux community, and others furnish a bandstand for the Linux community to voice their opinions. For example:

- Linux International: www.li.org
- LinuxHQ: www.linuxhq.com
- Linux Today: www.linuxtoday.com
- Linux Documentation Project: www.metalab.unc.edu/LDP/
- Linux Now: www.linuxnow.com
- Linux Journal, Linux Gazette, Linux Resources: www.ssc.com
- Linux Focus: www.linuxfocus.org
- Linux Weekly News: www.lwn.net
- Slashdot: www.slashdot.org
- Freshmeat: www.freshmeat.net
- File Watcher: www.filewatcher.org

This list is not exhaustive. You can find many more URLs in some of the sites mentioned here.

Opinions in some of the lists are for mature audiences only. Most of the lists are moderated and most of the opinions are mature, but people sometimes get carried away.

![](img/96a9ce6a13d8d15ed05f867f41574278_309_0.png)

# Chapter 17: Ten Sources of Help

## Attend Conferences

You can attend a number of conferences and trade shows for more information on Linux. All these shows are accurate as of the time I'm writing this, but events may change. Where possible, I've listed the more general Web addresses for these events. You might have to do a little Web surfing for the next event of the year. If you get stuck, try the Linux International Web site, which has an Events page that lists new events.

## Linux Kongress

Linux Kongress is the oldest Linux event. Held in Germany every year, it's a technical conference with a small trade show. The Web site is www.linux-kongress.de.

## Linux Expo

Linux Expo is held in the Raleigh/Durham, North Carolina, area every spring. It's a technical conference, trade show, and all-in-all good time. In 1998, more than 2,000 attendees and numerous vendors were there. The Web site is www.linuxexpo.org.

## USENIX/FREEIX

USENIX, a technical organization that has long supported UNIX people, has several technical conferences and small trade shows per year on various topics. A few years ago, a separate set of presentations, called FREEIX, was created for freely distributed operating systems as Linux. If you're interested in a good technical conference that attracts UNIX giants such as Dennis Ritchie or a Linux developer, you might want to take a look at www.usenix.org.

## CeBIT

CeBIT, the largest computer trade show in the world, is held yearly in Hanover, Germany. It often draws more than 600,000 people. Last year, Linux International (www.li.org) had a booth with several other Linux vendors and drew a mostly trade show, with very little (if any) conference sessions on Linux. To find out more about CeBIT, check out www.messe.de.

## Comdex

For the past four years, Comdex has had a Linux Pavilion, made up of an ever-growing set of vendors who are trying to explain to more than 200,000 resellers, distributors, and other vendors that Linux is and how to use it. Comdex is held both in the spring and fall, and you can check it out at www.comdex.com.

## IDG's Linux World

Linux World is a new show with conferences. The Web site is at www.linuxexpo.com.

## Try to Help Others

After you've exhausted all avenues of help (or maybe even before), you should just try to do whatever you want to do. Often, you will find that the pieces fit together or that the software is not as difficult as you thought. Here are some tips:

- If you are investigating a large software package, scan the documentation one time and then concentrate on the necessary topics.

I still remember the first time I tried to learn groff(1), a powerful text-processing system. The documentation was daunting, and I thought I would never learn the package. It turns out was right; I learned enough to do a few simple things that was all I needed. With those "simple things" (less than 2 percent of the package), I could write letters, create overhead slides, and do the necessary text processing. When I needed another command, I'd look it up in a reference book.

- Create a small sample of what you want to do.

If you're working with a new command or part of Linux, create a small example of one part of the command or software that you don't know and see how that works.

- Keep it small.

A friend named Mike Gancarz (Hi, Mike!) wrote a book called The Philosophy of Unix. In this book, he talks how Unix systems were created and programmed in the early days, utilizing lots of the small, cryptic (I prefer the word terse) commands that lurk below the glossy interface of X Window System. With these commands, you can create

![](img/96a9ce6a13d8d15ed05f867f41574278_311_0.png)

![](img/96a9ce6a13d8d15ed05f867f41574278_311_1.png)

powerful programs called shell scripts or just use the commands one at a time to transform your data. The main tenet of his book is to keep things simple and small.

- Remember Linux is only a piece of code and your computer is only a machine.

So what if you make a mistake? You're probably running Linux on a machine that has only one user, you. That's the great thing about Linux. It runs on such inexpensive machinery that you

![](img/96a9ce6a13d8d15ed05f867f41574278_312_0.png)

The way to cement a thought or an idea, however, is to explain it clearly to someone else. Helping others install Linux will help some of the concepts. Another idea is to attend a Linux Fest, where lots of people go (with their machines) to install Linux. Here you not only get to help someone else but also can learn something from other attendees.

# Chapter 18

## Ten Problem Areas and Solutions

- I can't boot Linux anymore
- My disk numbers have changed since installation
- My CD-ROM isn't detected
- I don't know how to remove LILO and restore my MBR
- I can't use LILO to boot
- The ls command doesn't show files in color
- Linux can't find a script (or a program)
- When I start X Windows System, I see a grey screen
- I don't know how to make X Windows System start at boot time
- I never seem to have the correct time

In any complex, technical situation, people end up having problems and issues that they need help. The problems in this chapter were taken from a database of questions and answers created after hundreds of people installed the CD-ROM. Some of these questions have been answered in the rest of the book, but because they still generate "what happened" questions, I repeat the information here.

## I Can't Boot Linux Anybody

Problem: You've installed Linux and everything is fine (naturally). Then one day make a change to your Windows or Windows NT system, and Linux stops working. You no longer use the lilo boot prompt, so you can no longer specify that you want to boot Linux.

Solution: Various operating systems tend to think that they are the only operating system on the disk or on the system. Therefore, when they are installed or updated, they write things to an area of the system called the Master Boot Record (MBR). This process overlays the Linux boot loader (called LILO) and stops you from booting Linux. The best correction requires an ounce
