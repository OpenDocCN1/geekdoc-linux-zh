Mesmtp,
P=[IPC], F=mDMFuXa, S=EnvFromSMTP/HdrFromSMTP,
R=EnvToSMTP, E=\r\n, L=990,
T=DNS/RFC8222/SMTP,
A=TCP $

Msmtp8,
P=[IPC], F=mDMFuXa8, S=EnvFromSMTP/HdrFromSMTP,
R=EnvToSMTP, E=\r\n, L=990,
T=DNS/RFC8222/SMTP,
A=TCP $

Mdsmtp,
P=[IPC], F=mDMFuXa%, S=EnvFromSMTP/HdrFromSMTP,
R=EnvToSMTP, E=\r\n, L=990,
T=DNS/RFC8222/SMTP,
A=TCP $

Mrelay,
P=[IPC], F=mDMFuXa8, S=EnvFromSMTP/HdrFromSMTP,
R=MasqSMTP, E=\r\n, L=2040,
T=DNS/RFC8222/SMTP,
A=TCP $

Mlocal,
P=/usr/bin/procmail, F=lsdFMAw5|@qSpFhn9,
=EnvFrom/HdrFrom, R=EnvTol/HdrTol,
T=DNS/RFC822/-X-Unix,
A-procmail -Y -a sh -d su

Mprog,
P=/usr/sbin/smirsh, F=lsdFMOqeu9, S=EnvFrom/LdrFrom,
R=EnvTol/HdrTol, D=$2;;
T=X-Unix/X-Unix/X-Unix,
A-smrsh -c $

Mprocmail,
P=/usr/bin/procmail, F=dMSFphnu9,
=EnvFromSMTP/HdrFromSMTP,
R=EnvToSMTP/HdrFromSMTP,
T=DNS/RFC822/-X-Unix,
A-procmail -Y -m sh $f su

The sendmail.cf file created by redhat.mc macro contains eight mailer definitions. The first five mailers define mail for TCP/IP delivery. The first one, designed to deliver traditional-set ASCII SMTP, is called smtp. The next mailer is for Extended SMTP mail and is called esmtp (It is the default mailer for Internet Mail.). The smtp8 mailer definition handles unencoded eight-bit SMTP data bound for remote servers that cannot handle Extended SMTP. The dsmtp mailer is used when the recipient initiates the mail connection and downloads with the ETRN command. Finally, relay is a mailer that relays TCP/IP mail through an external mail relay host. All of these mailers were covered in Chapter 5, “Understanding a Vendor’s Configuration,” in relationship to the MAILER (smtp) macro