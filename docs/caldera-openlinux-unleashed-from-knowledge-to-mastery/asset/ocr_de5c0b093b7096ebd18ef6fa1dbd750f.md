Mail Services

445

CHAPTER 19

19

MAIL SERVICES

```
#
S10
R<@>		$&		errors to mailer-daemon
RE <@ $*> 	$&		temporarily bypass Sun bogosity
RS+	$: $>50 $1	add local domain if needed
RS*	$: $>94 $1	do masquerading

#
# Envelope recipient rewriting
#
S20
RS+ < @ $* >	$: $1		strip host part

#
# Header sender rewriting
#
S30
R<@>		$&		errors to mailer-daemon
RE <@ $*> 	$&		temporarily bypass Sun bogosity
RS+	$: $>50 $1	add local domain if needed
RS*	$: $>93 $1	do masquerading

#
# Header recipient rewriting
#
S40
RS+	$:	$>50 $1	add local domain if needed

#
# Common code to add local domain name (only if always-add-domain)
#
S50
RS+ < @ $* >*$	$@ $1 < @ $2 > $3	already fully qualified
RS*	$@ $1 < @ *LOCAL* >	add local qualification

##########################
### SMTP Mailer specification ###
##########################

#### @(#)smtp.m4	8.38 (Berkeley) 5/19/98 ####

Msmtp,	P=[IPC], F=mDFMuX, S=11/31, R=21, E=\r\n, L=990,
	T=DNS/RFC822/SMTP,
	A=IPC $
Mesmtp,	P=[IPC], F=mDFMuXa, S=11/31, R=21, E=\r\n, L=990,
	T=DNS/RFC822/SMTP,
	A=IPC $
Msmtp8,	P=[IPC], F=mDFMuX8, S=11/31, R=21, E=\r\n, L=990,
	T=DNS/RFC822/SMTP,
	A=IPC $
Mrelay,	P=[IPC], F=mDFMuXa8, S=11/31, R=61, E=\r\n, L=2040,
```