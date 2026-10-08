# Chapter 4: Surveying the Application

NOTE The ! character has special meaning on the UNIX command line and will need to be escaped in grep searches.

```
[root@meddle] # get.sh www.victim.com /index.html | grep "<!--"
www.victim.com [192.168.189.113] 80 (http) open
<-- $id: index.html,v 1.155 2002/01/25 04:06:15 hpa Exp $ -->
ent 17, rcvd 16417: NOTOCK
```

At the very least, this shows us that the .html file is actually a link to the index.shtml. The .shtml extension implies that parts of the page were created with server-side includes. Induction plays an important role when serving the application, and why it's important to be familiar with various types of Web technologies. Pop query: What type of program could be responsible for the information in the S1d showed above?

Comments may seem innocuous, but even simple lines can be helpful. Multiple requests for the same page might return different comment fields. This is due to the fact that the servers reside behind load balancers. Given enough time, we might be able to figure out the size of the server farm! For example, two sets of comments might contain:

```
<-- ServerInfo: MPSFEISIB093 2001.10.3.13.34 Livel --
<-- Version: 2.1 Build 84 --

<-- ServerInfo: MPSFEISA096 2001.10.3.14.30 Livel --
<-- Version: 2.1 Build 84 --
```

A look at some other pages might reveal more cryptic HTML comments. Five different requests for pages from a site might reveal:

```
--whfUAXNBYdATE5E+6fEB9I3BKGXuuZuW --
--wh6fHHX2yMhPvJcmIKE69660QB2Ftaa --
--whfmMCA7AcHyHcmMhrubXnWxlGb1Fb3Fnl --
--whfJEVISFElHtCm2edn4kRIl6/QHGq --
--whfZBsBySWYI97KBeJyeQs+K3nIM96be --
```

An MD5 hash with a salt of "whif" perhaps? We're not sure.
Do not stop at separators. HTML source has all kinds of hidden treasures.
Trying for a few of these strings:

+   * sql
* select
* insert
* #include
* exec