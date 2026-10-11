# NEWS

Kernel News

# Zack’s Kernel News

![](bbox=[0.05, 0.19, 0.31, 0.4])

Chronycler Zack Brown reports on the latest news, views, dilemmas, and developments within the Linux kernel community.
By Zack Brown

# When the Process Is the Feature

The Linux kernel development process has undergone many changes through the years. Linus Torvalds was the first to understand how to run an open source project. The GNU General Public License (GPL) had existed for years, but the GNU projects that used it were isolated, and potential contributors were largely turned away. Linus’s great innovation was to encourage people of all skill levels to chip in, resulting in such an increase of development speed that pretty soon the entire open source world burst into existence. The Linux kernel was really where all of that started.

Since then, the kernel development process has followed its own evolutionary processes, with subsystem maintainers feeding patches for inclusion in the source tree up through highly trusted “lieutenants” to Linus. At a certain point, Linus also switched from simply releasing new versions of the kernel to using actual revision control, first the proprietary BitKeeper tool and then Git, which Linus wrote himself specifically to deal with the BitKeeper owner revoking permission to use the tool.

Among the many changes to kernel development over the years, one of the thorniest has been the struggle to balance stability with new development. It seems to be widely accepted wisdom that developers much prefer writing new features than stabilizing and maintaining those features over the long term. Linus tried several approaches to solving this dilemma. At one point, he alternated between a very long development cycle and a very long stabilization cycle. But the period of stabilization was quite painful for many, and he iterated quite a bit on finding a better method.

His current approach involves each kernel version having its own short window of time for receiving new features, followed by a series of “release candidates” that in principle become

more and more stable, and then finally he releases the new kernel version, and the cycle begins again. These relatively short cycles allow developers to enjoy the fun part of development while still taking the time to stabilize their work and make it more reliable for end users.

Recently during the Kernel’s usual stabilization phase, Kent Overstreet, the main developer of the bcachefs filesystem, submitted a very big patch for bcachefs. This is a new filesystem that Linux accepted into the source tree in 2024, although it is still flagged in the kernel as being an experimental feature.

Kent’s patch fixed a bunch of small bugs, but then went on to do some more major changes, which had originally been intended for the next kernel’s “merge window” (the time when new features would be acceptable). Kent sent them in this patch because he felt they were important. However, Linus did not like his approach.

Linus replied to his patch, saying: “No, enough is enough. The last pull was already big.

> “This is too big, it touches non-bcachefs stuff, and it’s not even remotely some kind of regression.

> “At some point ‘fix something’ just turns into development, and this is that point.”

Linus went on to say, “Nobody sane uses bcachefs and expects it to be stable, so every single user is an experimental site.” He concluded, “The bcachefs patches have become these kinds of ‘lots of development during the release cycles rather than before it’, to the point where I’m starting to regret merging bcachefs. If bcachefs can’t work sanely within the normal upstream kernel release schedule, maybe it shouldn’t *be* in the normal upstream kernel.”

Kent, maybe feeling a bit blindsided by Linus’s comments, strongly defended the strengths of bcachefs. He said, “Universal consensus has been

Author
The Linux kernel mailing list comprises the core of Linux development activities. Traffic volumes are immense, often reaching 10,000 messages in a week, and keeping up to date with the entire scope of development is a virtually impossible task for one person. One of the few brave souls to take on this task is Zack Brown.