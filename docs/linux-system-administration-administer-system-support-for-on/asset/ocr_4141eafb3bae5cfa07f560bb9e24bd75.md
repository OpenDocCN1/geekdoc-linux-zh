# # Troubleshooting

Because you're dealing with a computer, you always face two possibilities: (1) it may not do what you expect it to do, and (2) if it doesn't, you must be prepared to correct the glitch. Components such as hard drives can go south; you could change a configuration file in a way that completely destroys the way your system used to work. To combat such surprises, start with these measures:

+   If a problem emerges, ask yourself, *What was last changed before you noticed the problem?* Often that last change could be the culprit.

+   Keep logs on what you change on your system -- not only for troubleshooting, but also for keeping up to date on software upgrades.

+   If you have a really bizarre problem, yell for help: Post to the appropriate Linux newsgroup, state which version of Linux you're using and what distribution (it should be Slackware), and what your problem is; include screen captures.

To get into a troubleshooting frame of mind, consider a couple of possible sce-narios:

+   **Problem:** You've changed your sendmail configuration file and all the e-mail you send out now gets bounced back to you.

Approach: Most likely, your configuration is causing the problem. Before you change any configurations however, make sure you back them up (you might need to restore from them). An easy way to rename them is by adding an extension with the date. (For example, you can rename an older version of `/etc/resolv.conf` to `/etc/resolv.conf.060298`.)

+   **Problem:** Your PC crashed and now, when you reboot, it goes through the BIOS and says Loading LILO. . . and it reboots itself. Then it keeps doing this until you shut off your machine.

Approach: Remember the rescue disk that you made earlier? Pop it in the floppy drive and reboot. You should get the boot prompt again. When it appears, type the following command at the boot prompt:

```
boot: mount=/rootpartition
```

where *rootpartition* is the name of your actual root partition. My root disk, for example, is mounted in the directory `/dev/hda1` so the line looks like this:

```
boot: mount=/dev/hda1
```

The cause of this obsessive rebooting is obscure, but using the rescue disk seems to fix it.