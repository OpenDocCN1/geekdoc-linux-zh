would make someone superuser when given our own secret password as well as when given the usual root password, which remained unknown to us.

> In the early days, one system administrator would mail a new root password to all the other system administrators on the system, apparently not realizing that we were monitoring their mail for exactly this kind of security slip.

This was a classic case of their not analyzing the situation. Ask yourself, “Why does the password need to be changed?” The only real argument is that “it might be compromised.” Well, if it is, the account certainly should not be trusted to send the new password through.

By the same reasoning, password aging can be ineffective if the SysAdmins will not hear from the real user in short order if she cannot log in. Such a situation would be a user who does not log in very often. This is because the intruder changed the password since password aging required this for continued access.

Sadly, they soon guessed that this was not a good procedure, and we had to return to functioning as passwordless superusers, which at times could be a bit inconvenient.

Late one night on Cory Hall UNIX, as I was using my illegitimate superuser powers to browse through protected but interesting portions of the system, I happened to notice a suspicious-looking file called * /usr/adm/su*. This was suspicious because there were almost never any new files in the administrative * /usr/adm* directory.

If I was suspicious when I saw the filename, I was half paralyzed when I saw it contained a full record of every command executed by anyone who had worked as superuser since the previous day, and I was in a full state of shock when I found, at the end of the file, a record of all the commands that I’d executed during my current surreptitious session, up to and including reading the damning file.

It took me perhaps 10 minutes of panic-stricken worry before I realized that I could edit the record and delete all references to my illicit commands. I then immediately logged out and warned all other members of the group. Because nothing illicit ever appeared, the system administrators were lulled into a sense of false security. Their strategy worked brilliantly for us, allowing us to work in peace for quite a while before the next set of traps were laid.

The next potential trap I found was another new file in * /usr/adm* called * password*, that kept track of all unsuccessful attempts to log in as root or to *su* to root, and what password was used in the attempt. Because none of us had known the root password for months and therefore weren’t going to become superuser by anything as obvious as logging in as root, this wasn’t particularly threatening to us, but it was very interesting. The first few days that we watched the file it showed attempts by legitimate system administrators who had made mistakes of various sorts.