this isn't necessarily faster than using the archie program if you have it on
yystem!). Finally, if you aren't on the Internet at all, you can send
electric mail to archie at any of the three systems listed. Use prog
search-string, and ensure that the last line of your message is quit so it is
knows when to stop reading your mail for commands.

![](bbox=[0.172, 0.285, 0.238, 0.313])

+   1. To start out. I want to see what archie servers are known by my version of archie:
% archie -L
Known archie_servers:
archie.ans.net (USA [NY])
archie.rutgers.edu (USA [NJ])
archie.sura.net (USA [UO])
archie.unit.edu (USA [US])
archie.vgill.ca (Canada)
archie.funet.fi (Finland/Mainland Europe)
archie.au (Australia)
archie.doc.ic.ac.uk (Great Britain/Ireland)
archie-wide.ed.jp (Japan)
archie.ncu.edu.tu (Taiwan)
archie.sura.net is the default Archie server.
For the most up-to-date list, write to an Archie server and give it
the command 'servers'.

The notice line from the end: My archie server is archie.sura.net.
The other servers listed can be accessed but aren't checked directly. Usually,
it doesn't matter which server is used because the information available through
direct servers is mostly listed. If you just know something's out there but
can find it, check a few different servers with archie -h hostname.

+   2. To search for a specific program, I can simply enter the name of the program. I
interested in finding a UNIX program called newmail:
% archie newmail

```
Host plaza.aernet.edu.au
Location: /unet/comp.sources.unix/volume25
FILE -r--r--r-- 15049 Dec 20 1991 newmail
```

```
Host gumi.isi.edu
Location: /share/pub/vmh/bin
FILE -rxr-xr-x 534 Jul 9 18:26 newmail
```

```
Host venera.isi.edu
Location: /pub/vmh/bin
FILE -rxr-xr-x 534 Jul 9 11:26 newmail
```

![](bbox=[0.068, 0.893, 0.145, 0.963])