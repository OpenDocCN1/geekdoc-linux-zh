
# 446

# Hour 22

Sending electronic mail back and forth with users throughout the world is one of the most exciting and fun parts of learning UNIX. I often read magazine articles, for example, where the author lists an electronic mail address. It is a simple task to zip out a message if I have questions or kudos on the piece. Many magazines, from the Unix Reader to MacWorld, even list electronic mail addresses for the editorial staff. Even reporters from The Wall Street Journal and the New York Times are on the Internet now.

## Task 22.2: Talking with Remote Internet Users

To see who is logged in to a remote system, you can use a command finger; by default it will show you a summary of who is on the local account. Add a user to the command, and it will show information about the specified account. Specify a user on a remote system, and you can find out that user is logged in. Specify just the remote site, and it shows who is logged in at the current moment. You use finger accountname. To make it a remote system, append the hostname: finger account@host.domain. To check all users on a remote site, use finger@host.domain.

Once you've ascertained that a friend is logged in to a local or remote system, you can use the talk program to chat with the person live across the Internet. As opposed to the primitive line-oriented mode of write, talk is a full-screen program that enables both of you to type at the same time. Your screen shows the other person's typing on the bottom half of your screen.

1. A quick glance at the output of who shows that there are a lot of people currently logged in to the local system:

| root | Name | TTY | Idle | When | Location |
| --- | --- | --- | --- | --- | --- |
| taylor | Dave Taylor | co 1:13 | Mon 18:02 | | |
| kopje | Jeff Kip | aV | Mon 16:49 | | |
| adam | Adam Coy | Ab | Mon 16:41 | | |
| daffner | Lawrence Daff | sK | Mon 18:36 | | (doc27) |
| tsaa | Earl the Unctuous Aardva | sL 42 | Mon 12:48 | | (expert) |
| daffner | Lawrence Daff | *M | Mon 12:48 | | (localhost) |
| ben | Ben Moon | sN 8:42 | Mon 19:16 | (corona) | |
| ben | Ben Moon | sR 8:47 | Mon 19:22 | (corona) | |
| marteld | David Martin | *SY 7d | Mon 18:41 | (himbo) | |
| germaic | David German | sb | Mon 18:38 | (mac19) | |
| mk | Michael Kenny | *sc 2:48 | Mon 08:07 | (mk) | |
| mzabel | Mary Zabielski | *sf | Mon 18:45 | (sun1) | |
| fritzg | Geoff Fritzen | sh | 9 | Mon 18:45 | (pc43) | |
| brynta | Bryan Ayerson | *si | Mon 18:46 | (himbo) | |
| deckers | Sharon Deck | sk | Mon 18:51 | (xds31) | |

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_452_0.png)

## Internet E-Mail, Netnews, and IRC

2. To learn more about the account mk, I can specify that account name to the finger
% finger mk

```
Login name: mk (messages off) Real name: Michael McKenzie
Office: Math 204 Home phone:
Directory: /users/mk Shell: /bin/ksh
Universe: universe(ucb)
Member of groups: utech root longterm service
On since Dec 13 08:07:12 on ttysk from mk
2 hours 50 minutes Idle Time
Unread mail on this host.
```

Plan.
You can see that this is full of information. Notice that Michael is currently logged in to the system (the output says Dec 13 08:07:12 on).

3. To see who is logged in to the USENIX Association main computer in Berkeley, California, I can use:

```
% finger@usenix.org
Login TTY When Where
cmiu 2d Tue 10:10
nah Alain Henon p2 Mon 15:58 remote # 540895 Dia
toni Toni Vegetlia p1 3d Thu 07:29 exec
diane Diane Bertartini p3 9d Mar 08:41 mac2.usenix.org
mis Mark Seiden p4 3d Thu 21:46 seiden.com
scott Scott Sebastian p5 2d Fri 15:18 msnext.internet
lila Lila Carol Scott p6 3d Tue 14:54 biohazard
mis Mark Seiden p7 1l:12 Mon 08:09 thing1
toni Toni Vegetlia p8 3d Thu 22:09 seiden.com
ellie Ellie Young q1 1:00 Mon 10:33 bass:0.0
ellie Ellie Young q2 15:5d Wed 15:36 biohazard
ellie Ellie Young q3 1d Mon 10:33 bass:0.0
mis Mark Seiden q6 1d Fri 11:28 seiden.com
```

Here you can see that lots of folks are logged in, but almost everyone has a lot of idle time. A σ suffix indicates the number of days idle. So, you can see that Peter Mui's account has been idle for two days.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_453_0.png)

> To find out what the weather is like in the greater San Francisco area, finger weather@rogue.linux, which will connect you to the Lawrence Livermore National Laboratories in Walnut Creek, California.

JUST A MINUTE

4. To learn more information about a specific user on a remote site, specify the of the name and the user's system:

```
% finger ellie@usenix.org
[usenix.org]
```

# Hour 22

```
Login name: ellie In real life: Ellie Young
Directory: /staff/ellie Shell: /bin/csh
On since Dec 13 10:33:57 on tty1 from boss:0.0
1 hour 3 minutes Idle Time
Mail last read Mon Dec 13 15:05:08
```
You can see that Ellie has been logged in since December 13 but had over an hour of idle time.

5. To talk with someone on a remote system, use finger to verify that the person is logged in, not off doing something (which is what a high idle time suggests), use talk:
% finger marv@netcom
Login name: marv In real life: Marvin Raab
Directory: /oil/marv Shell: /bin/csh
Logged in since Mon Dec 6 15:22 on tty8 5 seconds idle time
Mail last read Mon Dec 13 15:22:22 1993
Plan.
% talk marv@netcom

![](img/f32f6f533c129de2ebafcd2b4ff01b1c9_454_0.png)
Once he responds, the screen looks like:

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_455_0.png)
Notice the cursor is in the top pane. Anything enter will be sent to Marvin, character by character, so we can interactively chat and even type at the same time without words getting jumbled. When I'm done, simply press ^C to quit. The finger program offers further information about users on your own and remote systems, using it is an essential first step in talking with your friends on the Internet. Try taylor@netcom, and if I'm logged in, what heck! Try talking hi!

## Task 22.3: Searching with Databases

The next step on your tour of Internet resources is the Wide Server, or WAIS. The WAIS system is a collection of databases accessible through a single search or query, and it was developed as a joint project of Apple Computer, Dow Jones Service, and Thinking Machines, Inc., in Boston. WAIS is a database of databases. By this writing, there are over 500 databases accessible for conducting searches through WAIS. The range of information is astounding—from acronyms for White House to cold fusion. The program is reasonably friendly to use, though it takes a bit of experience to be comfortable doing searches.

1. To connect to the WAIS system, use telnet to connect to quake.think.com, and log in wais. You can find an alternative WAIS server at the address wais.com if quake.think.com is unavailable.

```
 telnet quake.think.com
Trying...
Connected to quake.think.com.
Escape character is "^".
SunOS (quake.think.com)
login: wais
Last Login: Wed Dec 15 11:13:56 from alexia.lis.uiuc.
SunOS Release 4.1.3 (SUNC-STANDARD) #9: Wed Oct 27 18:18:30 EDT 1993
Welcome to wais.
```
After a few seconds, the screen clears and is replaced by:

| SWAIS | | Source Selection | Sources: 510 Cost |
|---|---|---|---|
| 001: | f | archie.au | aarnet-resource-code | Free |
| 002: | [nadsb.gscf.nasa.gov] | AAS jobs | Free |
| 003: | [nadsb.gscf.nasa.gov] | AAS meeting | Free |
| 004: | [reath.cs.uedu.au] | academic_email_conf | Free |
| 005: | [maine.univ.edu] | acronyms | Free |
| 006: | [archive.ost.edu] | aeronautics | Free |
| 007: | [ftp.colorado.edu] | ftp-co-colorado-edu | Free |
| 008: | [nostromo.osf.edu] | agricultural-market-news | Free |
| 009: | [archive.ost.edu] | alt.ducker | Free |
| 010: | [wais.oit.edu] | alt.gopher | Free |
| 011: | [sunite.unc.edu] | alt.sys.sun | Free |
| 012: | [wais.oit.carleton.edu] | alt.wais | Free |
| 013: | [alfred.ccs.2lu.se] | amiga-clips | Free |
| 014: | [munin.bbu.2lu.se] | amiga_fish_contents | Free |
| 015: | [combs.anu.edu.au] | AU-Original-Policies | $0.00/minute |
| 016: | [combs.anu.edu.au] | AU-Original-Studies | $0.00/minute |
| 017: | [combs.anu.edu.au] | AU-Original-DNA-L | $0.00/minute |
| 018: | [combs.anu.edu.au] | AU-Original-DNA-Studies | $0.00/minute |
Keywords: | <select> selects, w keywords, for move, <return> searches, q quits, or ?
