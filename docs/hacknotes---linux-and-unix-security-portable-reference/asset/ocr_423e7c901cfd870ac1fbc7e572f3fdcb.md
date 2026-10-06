# Chapter 1: Footprinting 5

# Looking for Sensitivity in Log Files

Many programs are known to write specific log files. Sometimes, these log files are accidentally placed within the web root of the web server. For example, a query such as: "Index of dead.letter on http://www.google.com/ will provide you with links to webs serving the dead letter file (see Figure 1-1). Note that the dead.letter file is created by some e-mail clients when a user is sending an e-mail, and it may contain part of the e-mail being composed. This file, along with other such log files, may provide critical and confidential information to potential intruders.

Search Engines

![](bbox=[0.139, 0.335, 0.809, 0.61])

John,

I have reset your password to 'abcd123'. Please change it immediately.

Eric,

On Sun, 12 Jan 2003 webmaster@somecompanyanyasample.com wrote:
> Dear Eric,
> Could you please reset my personal account(john) password? I can't
> remember it. Thanks. John.

Figure 1-1. Contents of a user's dead.letter file being served by a web server