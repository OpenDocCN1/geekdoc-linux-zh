in 1979 when a few sites decided to share some software and information on topics of common interest. They agreed to contact one another and to pass the information along over dial-up telephone lines (at that time running at 1,200 baud at best), using UNIX's `uucp` utility (UNIX-to-UNIX copy program).

The popularity of Usenet led to major changes in `uucp` to handle the escalating volume of messages and sites. Today much of the news flows over network links using a sophisticated protocol designed especially for this purpose: NNTP (Network News Transfer Protocol). The news messages are stored in a standard format, and the many public domain programs available let you read them. An old, simple interface is named **readnews**. Other interfaces, such as `rn`, its X Window System cousin `xrn`, `tin`, `nn`, and `xnews`, have many features that help you browse through and reply to the articles that are available or create articles of your own. In addition, Netscape and Mozilla include an interface that you can use to read news (Netscape/Mozilla News) as part of their Web browsers. One of the easiest ways to read netnews is to go to groups.google.com. The program you select to read netnews is largely a matter of personal taste.

As programs to read netnews articles have been ported to non-UNIX and non-Linux systems, the community of netnews users has become highly diversified. In the UNIX tradition, categories of netnews groups are structured hierarchically. The top level includes such designations as **comp** (computer-related), **misc** (miscellaneous), **rec** (recreation), **sci** (science), **soc** (social issues), and **talk** (ongoing discussions). Usually at least one regional category is at the top level, such as **ba** (San Francisco Bay Area), and includes information about local events. New categories are continually being added to the more than 30,000 newsgroups. The names of newsgroups resemble domain names but are read from left to right (like Linux filenames): `comp.os.unix.misc`, `comp.lang.c`, `misc.jobs.offered`, `rec.skiing`, `sci.med`, `soc.singles`, and `talk.politics` are but a few examples. The following article appeared in `linux.redhat.install`:

> ```
> > I have just installed Fedora 12 and when I try to start X I get the
> > following error message:
> >
> > Fatal Server Error.
> > no screens found
> >
> > XIO: Fatal IO error 104 (connection reset by peer) on X server "",0.0" after
> > 0 requests (0 known processed) with 0 events remaining.
> >
> > How can I solve this problem?
> >
> > Thanks,
> > Fred
> ```
> 
> Fred,
> 
> It would appear that your X configuration is incorrect or missing. You should run `system-config-display` and set up the configuration for your video card and monitor.
> 
> Carl