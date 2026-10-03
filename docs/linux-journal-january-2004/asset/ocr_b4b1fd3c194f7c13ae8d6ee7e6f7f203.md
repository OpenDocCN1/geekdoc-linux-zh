![](bbox=[0.75, 0.02, 0.92, 0.23])

# Mondo and Mindi Tips

Thanks for the article about restoring with Mondo and Mindi in the October 2003 issue. It was good, but it could have included a couple more options, in my opinion. Option -g gives a nice graphical interface to the restoration process. Option -l GRUB -f /dev/xxx ensures that if one uses the GRUB loader, it will be integrated nicely. Option -k FAILSAFE adds compliance with Debian/GNU. I believe this last one is important for Debian users.

--
Jose Marrero

# NEC Source Code?

I was very interested in your article about NEC's fault-tolerant server [LJ, October 2003]. I'm an IT consultant here in Buenos Aires, Argentina with some exposure to fault-tolerant and mission-critical applications. I contacted Mr John Fitzsimmons (of Aspire Communications) four or five months ago in order to help me get the source code for NEC's FT Linux. As I understand it, the software must be released under the GPL, but as of today I wasn't able to get the software. So, it was great to know from your article that "...NEC told us they are firmly committed to releasing all changes to the public under GPL." I think I will have to wait just a little longer. Do you have an approximate date for that release?

One other point, as the article stated, "At the time of this writing, NEC was reviewing and documenting its kernel changes for a planned public release, perhaps through OSDL's Carrier Grade Linux Project...", could you tell me what I should do to get the release from OSDL? Will it be available to the general public or to OSDL members only?

--
Pablo J. Rogina, IT Consultant

> *Dan Wilder replies: I am not aware of any such release to date. I am copying Mr. Fitzsimmons on this note, in hope that he may have some comment.*

# Electronic-Only Subscription?

Just wondering if you are going to have an electronic copy of Linux Journal for subscription. For readers overseas, the subscription rate is kind of expensive. I guess that's due to the shipping cost. It would be really helpful if you could provide the electronic copy as a subscription option, with the same

cost as the subscription rate within the States, or cheaper.
--
Simon

> *You're not the first person who has asked this. We don't do this yet, but I've asked our subscription department to find out if we can.—Ed.*

# Mick's LDAP and IMAP Corrections

There are two errors in my article "Secure Mail with LDAP and IMAP, Part I" [LJ, November 2003]. First, early in the article I say (about Cyrus IMAP) "...use of databases rather than flat files to store messages has an obvious performance benefit." Actually, although Cyrus IMAP does use database files for indexing messages, it stores the messages themselves as individual flat text files.

Second, later in the article, I correctly point out that to configure Cyrus SASL on SuSE to use LDAP, you must edit the parameter SASLAUTHD_AUTHMECH in /etc/sysconfig/saslauthd. The problem is, the Cyrus SASL package in SuSE doesn't have LDAP support compiled in. You either need to build your own LDAP-enabled package with SuSE's cyrus-sasl2 source-RPM (SRPM) or forego direct LDAP support in SASL altogether and use the PAM method instead, which is compiled in by default. In the latter case, you need to install the module pam_ldap, and then create a file, /etc/pam.d/imap, containing these lines:

```
#PAM-1.0
auth    required    /lib/security/pam_ldap.so
account required    /lib/security/pam_ldap.so
```

Next, copy the file /usr/share/doc/packages/pam_ldap/ldap.conf to /etc/openldap/ldap.conf, and edit it to match your environment (the most relevant settings are host, base, binddn, bindpw and TLS_REQCERT). Finally, edit /etc/sysconfig/saslauthd to include this line:

```
SASLAUTHD_AUTHMECH=pam
```

I apologize for any confusion or inconvenience that either error may have caused.
--
Mick Bauer

# Busy Chef Working On Another Book

Tinyminds' Tony Brijeski (Fragadelic)

recently had the pleasure of sitting down with Marcel Gagné over some coffee and asked him some questions about his recently released book Moving to Linux: Kiss the Blue Screen of Death Goodbye and his views on where Linux is today. He even spilled the beans on the new book he is currently working on; you'll have to read the interview to find out about it at www.tinyminds.org.

--
Mark Angeli

# Modula-3 Better than C++ and Ada

This letter to the editor is a response to Dennis Ludwig's letter "Ada Isn't Awful", in the November 2003 issue. I am a counter-example to Dennis Ludwig's statement "I have yet to meet an Ada basher who really knows the language." I have programmed in Ada, mostly full-time since 1986, done serious development work on three Ada compilers and served as a resident Ada language lawyer for over ten years. It's awful, and I hate it. That said, it's not half as bad as C++, to which Ludwig primarily seems to compare Ada. I do agree with much of his cited Web article. Both languages are horribly over-complicated to a similar degree. Most working programmers in either language don't even come close to understanding their language. At least Ada is strongly type-safe, while C++ inherited all of C's worst type-unsafe and "undefined" behaviours, so lack of understanding in Ada is more likely to show up as compile errors instead of bugs.

But the best languages, such as the Pascals, Modula-2 and the Oberons, are an order of magnitude simpler, and some of them have useful feature lists comparable to Ada. My favorite is Modula-3, with a language definition ten times smaller than Ada. It has a more flexible type-safe separate compilation, far more powerful information hiding capabilities and a choice of garbage-collected or