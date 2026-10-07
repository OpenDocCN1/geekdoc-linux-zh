# Analyzing a Sample M Command

Examining one of the mailer entries from Listing 7.12 explains the structure of all of the mailer definitions. The entry for the smtp mailer from Listing 7.12 is:

```
Msmtp,

P=[IPC], F=mdFMux, S=EnvFromSMTP/HdrFromSMTP,
R=EnvToSMTP, E=\r\n, L=990,
T=DNS/RFC822/SMTP,
A=TCP $
```

Let's examine each field in this definition:

+   M Beginning a line with an M indicates that the command is a mailer definition. smtp Immediately following the M is the name of the mailer, which in this case is smtp.

+   P=[IPC] The P argument defines the path to the program used for this mailer. In this case it is [IPC], which means this mailer is delivered by Sendmail. Other mailer definitions, such as local, have the full path of some external program in this field. F=mdFMux The F argument defines the Sendmail flags for this mailer. Other knowing that these are really flags, the meaning of each individual mailer flag is of little interest, in this case, m says that this mailer can send to multiple recipients at once; DFM say Date, From, and Message-ID headers are needed; u says that uppercase should be preserved in headers and usernames; x says that message lines with a dot are prepended.

+   S=EnvFromSMTP/HdrFromSMTP The S argument defines the ruleset that process sender addresses. The ruleset names can be different for every mailer, allowing mailers to process e-mail addresses differently. In this case, the sender address in the mail "envelope" is processed through ruleset EnvFromSMTP, and the sender address in the message is processed through ruleset HdrFromSMTP. These rulesets are also addressable as 11 and 31 respectively. So it is possible that you'll see S for the smtp mailer defined as S=11/31 on some systems.

+   R=EnvToSMTP The R argument defines the ruleset used to process recipient addresses for this mailer. Every mailer can have a R value to allow each mailer to handle recipient addresses differently. Like the S field described above, the R field has two rulesets, one for the envelope header and one for the mail header, separated by a slash. In this case, ruleset (EnvToSMTP) is applied to all recipient addresses for the smtp mailer. EnvToSMTP is also known as ruleset 21, so this could have been written as R=21.

+   E=\r\n The E argument defines how individual lines in a message are terminated. In this case, lines are terminated with a carriage return and a line feed.