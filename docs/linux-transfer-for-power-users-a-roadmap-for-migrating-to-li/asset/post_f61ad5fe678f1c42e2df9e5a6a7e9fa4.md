
![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_313_0.png)

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_313_1.png)

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_313_2.png)

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_314_0.png)

When you’re ready, click the “Write files to CD” button. After 15 to 45 seconds, a series of informational dialogs will document the progress, as shown in **Figure 34**.

When all files have been written, the CD will eject (if you checked that box in Figure 33). Pop the CD back in, and after a few moments, the CD will show up on the desktop like any other CD, as shown in **Figure 35**. You can now manipulate the files on the newly burned CD just like any other CD.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_314_1.png)

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_314_2.png)

## Summary

Linux has made great strides in hooking up to a wide variety of hardware in the past couple of years, and even better compatibility is high on the list of most open-source projects. Indeed, the biggest stumbling block these days is the recalcitrant vendor that doesn’t want to open up its APIs to Linux developers, but the number of those companies is shrinking daily. Life is good and it’s only going to get better.

The purpose of this chapter is to get you started with Linux on your desktop, but of course there’s a lot more than what I can cover here. In addition, new versions of Fedora Core are released on a regular basis. I’ll keep you up to date by writing new articles as well as posting updates related to this book. These materials can be found on Hentzenwerke’s Web site, www.hentzenwerke.com. Click “Catalog” and navigate to the page for Linux Transfer for Windows Power Users.

# Chapter 13 Security

In Chapter 1, I mentioned that one of the top 10 mythes with respect to Linux is that “because it's more secure, you don't have to worry about security.” And, yes, it is a myth: You do have to worry about security. The only computer that's completely secure is the one that's turned off, unplugged, and sitting in a locked box in the middle of the room. In this chapter, I'll address a variety of topics dealing with security from the point of view of a power user: from strong passwords and separate user accounts to virus protection and firewalls.

Security is a hot topic these days, and I'm not going to get into a big argument with folks in the Microsoft camp about how operating system is more secure. There's plenty of material available for research on the Web and from various consulting companies; some of it will convince you that Windows is more secure and some of it will convince you that Linux is. And obviously, I'm biased. I spent over a decade developing software on Windows, and I'm moving everything to Linux.

All I can offer is my personal experience running Windows and Linux servers and workstations side-by-side for the last couple of years. I've experienced attack targeted against Windows boxes that are many orders of magnitude larger than those that target Linux computers. Whether the attackers look for holes in Windows server software, aim at vulnerabilities in desktop software and applications, or rely on the naiveté of Windows users, the fact is that more attempts are made against Windows than against Linux. My Web server logs are filled with tens of thousands of attacks against Windows exploits; I've yet to be hit by a Linux exploit (knock on wood, of course). And my Windows workstation is being hammered by viruses in a dozen different ways incessantly throughout the day, through e-mail viruses, Web-site spoofs, and other means. I've yet to receive a Linux-based virus though e-mail, and if I did get one, it would have to be a shell script—and I'm not aware of any Linux mail client that ever allowed the execution of attachments by default.

That's because, generally, attackers want to make the biggest splash possible, and they do that by attacking the largest installed base with the most vulnerable population. And right now, that target is Windows. But as Linux becomes more popular, it will offer an increasingly attractive target, and undoubtedly someone out there would like to become known as the person who engineered the first widespread Linux attack. So don't let the current minuscule likelihood of being attacked let you stay complacent.

## Your own password

When you installed Fedora Core, presumably you followed the instructions and created your own user account instead of just cruising around as “root.” (If you didn't, I'll show you how to create a user account in an upcoming section.)

When you created your user account, you also created a password. At some point, you will probably want to change it. Here's how. Select Main Menu | Preferences | Password, and you'll be prompted for the password for the currently logged-in user, as shown in Figure 1.

Why? Obviously you know your password, because how else could you be logged in? The answer is ... perhaps it isn’t at your computer right now. Someone could have wandered by your machine while you went for a coffee, and changed your password on you, and you’d never be the wiser—not until tomorrow when you tried to log in and found your password didn’t work. That would start the day out wrong.

Once you enter your password (or the password for whichever user is shown—maybe you’re changing the password for one of your kids on this machine), you’re asked for a new password (see Figure 2). Linux will do some checks on the password you enter. For example, if you enter “mouse” or “herman,” you’ll get an error (see Figure 3).

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_317_0.png)

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_317_1.png)

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_317_2.png)

So enter a good password. What makes a good password? Oh, gosh, lots of things. First, make it long enough. Fedora Core won't let you enter a two- or three-letter password; it has to be at least five characters long.

The second attribute of a good password is that it's a completely random combination of letters and characters. Despite what the movies will have you believe (I'm referring specifically to Spaceballs), "12345" is not a good password. On the other hand, "j4$R83_dT" is much better because it contains all of the elements that people advise: lowercase and uppercase letters, numbers, and even a symbol thrown in for good measure. The problem is that it's hard to remember and type.

A good compromise is a combination of letters and numbers that means something to you but is put together in a random manner. For example, suppose you played soccer goalie as a youngster, and you lived at 1026 North Elm Avenue. Combining these attributes could generate passwords like these: "so1026cCelmer" or, even better, "go10NEal26!".

You don't want to make it so hard, though, that you won't remember the trick you used, and end up writing it down on a piece of paper taped to your monitor.

Once you've entered a secure password, you'll be prompted to retype it (see Figure 4). If you don't retype it the same way (you might have mistyped, but you need to mistype twice the same mistaken way), you'll be warned, as shown in Figure 5.

And that's all there is to it. You don't have to have any special privileges, but you do have to know the original password.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_318_0.png)

*Figure 4. Retyping your password ensures that you didn't make a mistake typing it the first time.*

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_318_1.png)

*Figure 5. If you don't repeat the password properly, you'll be notified.*

## Change root password

Just as with your user password, you may find a need to change the root password. One common reason is that when people start out with Linux, they provide a “weak” password for root so that they can easily remember it and get on with getting acquainted with their new operating system. After a while, you’ll realize that it really is time to create a stronger root password. Here’s how.

Select Main Menu | System Settings | Root Password, and you’ll be prompted for the root password, as shown in **Figure 6**, much like when you changed your own password. In this case, you’re running an application that requires root access.

After entering the current root password, you’ll be prompted to enter and re-enter the new password, as shown in **Figure 7**.

The same process applies as with your user password: The new passwords must match, for example. And, again, that’s all there is to it.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_319_0.png)

Figure 6. You have to know the root password in order to change it.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_319_1.png)

Figure 7. Enter and re-enter the new root user password.

## Users and groups

As I’ve mentioned regularly, using root as your daily account is one surefire way to expose yourself to security problems, make yourself susceptible to accidentally trashing your system, and attract ridicule from friends who know better. But because you’ve been using Windows, where running as Administrator is a common practice, perhaps you haven’t taken those warnings to heart yet. If not, now is the time to create a user account for your daily use.
