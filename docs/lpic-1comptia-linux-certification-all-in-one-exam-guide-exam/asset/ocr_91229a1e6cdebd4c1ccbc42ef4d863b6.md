We had a recent issue at my child’s middle school where this very thing happened. The attendance secretary kept her password on a sticky note next to her keyboard. A student noticed this and, one day after school, logged in to her computer and used the school’s attendance tracking software to send out automated prank phone calls to the parents of all students in the school. This “exploit” was fairly innocuous, but it gives you an idea of just how easy it is to defeat the most complex security systems if users write down their passwords and leave the note in plain sight.

The “sticky note phenomenon” is yet another reason for enforcing good physical security. A ne’er-do-well can gain easy access to corporate information using a password that’s posted in plain sight. Once done, it can be very difficult to trace the breach back to the intruder.

Finally, you should train your users how to deal with social engineering attempts. This is actually one of the easiest and most effective tools in the intruder’s tooltop. Social engineering exploits human weaknesses instead of technical weaknesses in the system. Here’s how a typical social engineering exploit works.

The intruder calls an employee of an organization posing as another employee. The intruder tells the employee that he is “Fred” from Sales and is on the road at a client site. He needs to get a very important file from the server and can’t remember his password. He then asks the employee if he can use his or her password “just this once” to get the files he needs.

Most employees want to be team players and help out in an emergency. They are all too willing to hand out their password, granting the intruder easy access to the system. Some social engineering attempts are less direct. Instead of calling and asking for passwords, the intruder sifts through the company garbage looking for little yellow sticky notes with users’ passwords written on them. Some social engineering attempts are more “in your face.” The intruder sifts through the trash to find the name of a high-ranking person in the company. He then calls an employee posing as that person and demands that the employee divulge his or her password, threatening to fire them if they don’t comply. Pretty sneaky, huh?

The best way to combat social engineering is to, again, train your users. Teach them to not write down passwords. Teach them to not phone sensitive data in the trash—shred it instead! Teach them about social engineering phone calls and how to deal with them. Most organizations simply tell their employees to forward any calls asking for a password to the Help Desk (that’s you). Chances are, all they will hear is a click on the other end.

In addition to configuring password aging, you can also increase the security of your Linux systems by limiting logins and resources. Let’s review how this is done next.

# # Configuring User Limits

You can impose limits on how many times users may log in, how much CPU time they can consume, and how much memory they can use on a Linux system. This can be done in two ways:

+   - Using pam_limits to restrict access to resources
+   - Using ulimit to restrict access to resources