# Modern access control

access control requirements at the average site. All UNIX and Linux variants con-
tinue to support this model, and it remains the default approach and the one that's
most widely used today. And except when we discuss some specific alternatives,
we assume throughout this book that it's the approach you're using.

Nevertheless, it has some obvious shortcomings:

+   - From a security perspective, the root account represents a potential sin-
gle failure. If it's compromised, the integrity of the whole system
violated. There is no limit to the damage an attacker can inflict.

+   - The only way to subdivide the special privileges of the root account is by
writing suited programs. Unfortunately, as the Internet's steady stream
of security updates demonstrates, it's difficult to write truly secure soft-
ware. Besides, you shouldn't write custom software to express
sothing as "id like these three people to be able to perform
backups on the file server.

+   - The security model isn't strong enough for use on a network. No com-
puter to an unprivileged user has physical access can be trusted to
accurately represent the ownerships of the processes it's running. Who's
to say that someone hasn't reformatted the disk and installed their
hacked copy of Windows or Linux, with UIDs of their choosing?

+   - Many high-security environments enforce conventions that simply can't
be implemented with traditional UNIX security. For example, United
States standards require computer systems to forbid publi-
ged users (e.g., those with Top secret clearance) from repubishing high-security documents at a lower security level. Traditional
UNIX security depends on the good will and skill of individual users in
this regard.

+   - Because many access-control-related rules are embedded in the code of
of commands and daemons, you cannot redefine the system's
behavior without modifying the source code and recompiling. But that's
not practical in the real world.

+   - There is minimal support for auditing. You can easily see which groups a vari-
er belongs to, but you can't necessarily determine what those group
memberships permit a user to.

Because of these shortcomings, UNIX and Linux systems have undergone a vari-\ety of interventions over the years to enhance various aspects of the access control
system and to help make UNIX systems more acceptable to sites with high secu-
ity requirements. Some of the adjustments, such as PAM (see page 109), now
have nearly universal support. Others are relatively idiosyncratic. The following
sections outline the most common extensions.