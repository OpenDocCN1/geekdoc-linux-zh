wren.foobirds.org. If that system is unavailable, it will try parrot.foobirds.org. In the case of ibis, Sendmail will deliver the mail directly to ibis.foobirds.org. The /mx command lets you anticipate the delivery process.

The second command in Listing 10.12, /canon, asks DNS for a canonical name. In the example, the /canon command is given the hostname robinbreast, which it passes to DNS. DNS returns the canonical name robin.foobirds.org for the hostname robinbreast.

The last command in Listing 10.12 looks up a value in a database. In the example the database, which is the standard internal name for the generictable, the key used for the lookup is kathy. In Listing 10.12, the key kathy returns the value kathy.mccafferty from the generictable. Any database configured on the system can be searched with the /map command.

The commands that query DNS or search databases were not used in any of the tests run earlier in this text. Generally, you are not interested in the value returned by DNS or from the database; you are interested in these values on the addresses Sendmail is rewriting. About the time you will query DNS or a database is when you want to determine what values are providing to Sendmail. Because address test mode is generally used to debug or refine the Sendmail configuration, it is more likely that you will use one of the address test mode commands that let you examine the contents of the sendmail.cf file. Listing 10.13 shows these two commands in action.

# Listing 10.13 Looking at the Configuration File in Address Test Mode

```
mailer 0 (prog): P=/usr/sbin/smush S=EnvFromL/LdrFromL
R=EnvTol/HdrTol M=U:0 E=9DFMeloqsu L=0 E=\r
T-Tix-Unix/X-Unix/X-Unix A=smush -c $u
mailer 1 ("file\): P=<file> S=sparse/parse R=parse/parse M=U:0
F=9DEFMPqsu L=0 E=nTix-Unix/X-Unix/X-Unix A=FILE $u
mailer 2 ("include"): P=<include> S=sparse/parse R=parse/parse
M=U:0 F=fsu L=0 E=\nT T=<undefined>/<undefined>
A=Include $u
mailer 3 (smtp): P=[IPC] S=EnvFromSMTP/HdrFromSMTP
R=EnvToSMTP/EnvToSMTP M=U:0 E=DFMXamu L=990 E=\r\n
T=DNS/RFC822/SMTP A=TCP $$
mailer 4 (smtp): P=[IPC] S=EnvFromSMTP/HdrFromSMTP
R=EnvToSMTP/EnvToSMTP M=U:0 E=DFMXamu L=990 E=\r\n
T=DNS/RFC822/SMTP A=TCP $h
```