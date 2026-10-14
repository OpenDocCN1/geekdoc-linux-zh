# LISTING 23.5 Sending Mail Using Sendmail

```
#!/usr/bin/perl
open (MAIL, "| /usr/sbin/sendmail -t"); # Use -t to protect from users
print MAIL <<EndMail;
To: dpitts@mk.net
From: rbowen@mk.net
Subject: Email notification

David,

Sending email from Perl is easy!
Rich
.
EndMail
close MAIL;
```

# NOTE

Note that the @ sign in the email addresses must be escaped so that Perl does not try to evaluate an array of that name. That is, dpitts@mk.net will cause a problem, so you need to use dpitts\@mk.net.

The syntax used to print the mail message is called a here document. The syntax is as follows:

```
print <<EndText;
....
EndText
```

The EndText value must be identical at the beginning and at the end of the block, including any whitespace.

# LISTING 23.6 Sending Mail Using the Mail::Sendmail Module

```
#!/usr/bin/perl
use Mail::Sendmail;
%mail = ('To' => 'dpitts@mk.net',
'From' => 'rbowen@mk.net'
'Subject' => 'Email notification',
'Message' => 'Sending email from Perl is easy!',
);
sendmail(%mail);
```

Perl ignores the comma after the last element in the hash. It is convenient to leave it there; if you want to add items to the hash, you don't need to add the comma. This is purely a style decision.