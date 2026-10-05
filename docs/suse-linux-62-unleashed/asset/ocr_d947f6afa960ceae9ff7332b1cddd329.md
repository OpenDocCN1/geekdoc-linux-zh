# SMTP and Protocols CHAPTER 9

# sendmail as MTA: Client (Sender) and Server
(Receiver) SMTP

As mentioned before, sendmail can function as an MTA because it understands the SMTP
protocol (V.8 sendmail also understands ESMTP). SMTP is a connection-oriented
protocol, so a client and a server (also known as a sender and a receiver) always exist. The
SMTP client delivers a letter to an SMTP server, which listens continuously on its
computer's SMTP port. sendmail can be an SMTP client or an SMTP server. When run by
an MUA, it becomes an SMTP client and speaks client-side SMTP to an SMTP server (not
necessarily another sendmail program). When your sendmail starts in daemon mode, it
runs as a server. When in this server mode it does two main tasks, the first is continuously
listening on the SMTP port for incoming mail. The second is managing the queue of mail
that has not been delivered yet and periodically retrying delivery until the message is finally
divered successfully or the retry limit is exceeded.

# sendmail Is Not a Final Delivery Agent

One thing that sendmail doesn't is final delivery. sendmail's author wisely chose to
leave this to other programs. sendmail is a big, complicated program that runs with
superuser privileges. That's an almost guaranteed recipe for security problems, and quite a
few have occurred in sendmail's past. The additional complexity of final mail delivery is
the last thing sendmail needs.

# sendmail's Auxiliary Files

sendmail depends on a number of auxiliary files to do its job. Most important are the
alias file and the configuration file, sendmail.cf. The statistics file, sendmail.st, can be
created or not, depending on whether you want statistics on how many messages are sent to
and received from your host. This includes total amount of email traffic in kilobytes as
well. sendmail.hf, which is the SMTP help file, should be installed if you intend to run
sendmail as an SMTP server (most sites).

![](bbox=[0.885, 0.595, 0.995, 0.765])

The other file that might be required on your host is sendmail.cw, which contains all of the
alternate hosts for your email server. For example, if your main email server is
mail.whizzer.com, which is specified as an MX for whizzer.com, you would need to put
whizzer.com in this file to tell sendmail to deliver whizzer.com email on mail.whiz-com.

That's all that needs to be said about sendmail.st, sendmail.hf, and sendmail.cw. Other
auxiliary files are covered in the Sendmail Installation and Operating Guide, or SIOG for
short. The SIOG is usually found in /usr/doc/sendmail/doc/op/ps or in the source