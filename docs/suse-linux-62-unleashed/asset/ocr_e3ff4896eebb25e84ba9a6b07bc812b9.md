and everything after __END__. If a directory is specified, Perl changes to the directory before executing the script.

# Code Examples

Over the last few years, a lot of people have picked up the notion that Perl is a CGI language, although it is not good for anything else. Nothing could be further from the truth. You can use Perl in every aspect of your system administration and as a building block in whatever applications you are planning to run on your shiny new Linux system.

The following sections contain a few examples of things you might want to do with Perl. Perl is versatile enough that you can make it do about anything.

# Sending Mail

There are several ways to get Perl to send email. One method that you see frequently is opening a pipe to sendmail and sending data to it (shown in Listing 25.8). Another method is using the Mail::Sendmail module, which uses socket connections directly to send mail. The latter method is faster because it does not have to launch an external process.

LISTING 25.8 Sending Mail Using Sendmail

```
open (MAIL, | /usr/bin/sendmail -t*); # Use -t to protect from users
print MAIL <<EndMail;
To: dpitts@mk.net
From: rbowen@mk.net
Subject: Email notification
David,
Sending email from Perl is easy!
Rich

EndMail
close MAIL
```

> Note
Note that the @ sign in the email addresses needs to be escaped so that Perl does not try to evaluate an array of that name.