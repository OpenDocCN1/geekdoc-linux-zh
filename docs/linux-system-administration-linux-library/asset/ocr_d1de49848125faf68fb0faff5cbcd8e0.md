# Chapter 17 Setting Up Your Mail Server

+   - You can run fetchmail manually, by typing fetchmail whenever you want to check
new mail.

Most of the automated methods run fetchmail as root by default, the .fetchmailrc file must be placed in the /root directory. You can create a cron job that runs as an ordinary user, but this requires somewhat more effort to configure dropping a script in a sub True of /etc. Consult the cron man pages for more information on this topic. Normally, it doesn't matter whether fetchmail runs as root or as an ordinary user; either way, the program calls sendmail to deliver the mail locally. Depending upon who should know the passwords contained in .fetchmailrc, though you might want to be cautious about the user whose name fetchmail runs.

# Antispam Measures

In user circles, spam refers to junk e-mail—ads for dubious hair-loss remedies, illegal schemes, mysterious messages in languages you don't understand, and so on. Sadly, spam is a major problem for e-mail administrators. There are two aspects to this problem: preventing your system from being used as a source of spam, and blocking incoming spam that may annoy your users and consume system resources. A few steps can help prevent your system from becoming a source of spam. Blocking incoming spam is a tougher problem, but there are still some actions you can take to at least reduce the volume of your spam site sees.

# The Problem of Spam

Individual users, spam is typically an annoyance. A user who receives half a dozen a dozen spams a day may typically spend a few seconds determining that a message is spam and deleting it. This can easily work out to several hours a year wasted deleting spam! On occasion, spam may be offensive, as when it advertises an X-rated Web site or contains racist slurs. If the user has a slow network link, the spam may take some time to transmit—we've seen spams 150KB in size, and this is certainly not the world record for spam size.

To a mail administrator, spam is a more serious problem. In addition to annoying to users, spam consumes disk space and network bandwidth. These may not be major factors to a small site, but ISPs may need to increase hard-disk sizes or more network bandwidth to cope with spam. What's worse, spam generates complaints. This is particularly true if your own server becomes a source of spam. If somebody uses your system to send thousands of ads for aphrodisiac floor wax, chances are you'll get complaints in return—perhaps enough to seriously disrupt your life for a day or more. It's therefore critically important that your mail server not become a spam source.