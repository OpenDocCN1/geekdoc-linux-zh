```
=> 'install-sendmail-5.3.1.tar.gz'
Connecting to cork.linux.ie:80... connected!
HTTP request sent, awaiting response... 200 OK
Length: 39,807 (application/x-tar)

OK -> ... [100%]

21:18:30 (7.78 KB/s) - 'install-sendmail-5.3.1.tar.gz' saved [39807/39807]
```

```
[-kevin@mo kevin]$ cp -kevin/install-sendmail-5.3.1.tar.gz .
[-kevin@mo kevin]$ tar zxf install-sendmail-5.3.1.tar.gz
[-kevin@mo kevin]$ cd install-sendmail-5.3.1
[-kevin@mo install-sendmail-5.3.1]$ ./install-sendmail -c
```

It then asks the following questions:

Which language do you wish to use? English(1)
1.1 What address do you want all the emails from your machine to have? gonzo.gov
1.2 Will all mail for gonzo.gov come to this machine? n
2.1 Do you want your outgoing email to be sent via an outside email server?
If you're on a modem dial-up connection you probably should say Y here. y
2.1.1 Where do you send your email? (outgoing smtp server, probably your ISP
[smtp.isp.com])? mail.gonzo.gov
2.2. Use remote mail? If you have a dial-up connection, you can compose mail
when you're offline, then 'queue' it for delivery when you're connected.
(You'll have to run 'usr/bin/sendmail -q' to deliver the mail, however.)
Local mail (mail to people who login to your machine) will still be delivered
as normal. If you answer "no" to this question, all mail will be delivered
immediately, rather than queued. This might cause your machine to dial-up your
connection, even at peak times.
Would you like to queue remote mail? y
3.1 Do you like to serving mail to a local network? n
4. Virtual Domain Support
4.1 Do you need this feature? I'll provide a way for you to
enter aliases too. n
5. Generics Table Support
5.1 Do you want to map local email addresses to new ones? y
5.1.1 Enter the local username you want to map.
Type "none" when you're finished.
[bob]? kevin
5.1.1 What address should people see when veep writes an email?
[den@fsomeplace.org]? csainhs@gonzo.gov
5.1.2 Enter the local username you want to map.
Type "none" when you're finished.
[?] none
6. Incoming Mail Servers
6.1 Do you want Fetchmail support? y
6. Incoming Mail Servers
6.1.1 Enter a pop server you poll for mail. Type "none" when you're finished.
[pop.isp.com]? pop.gonzo.gov