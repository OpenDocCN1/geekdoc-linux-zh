
That protocol is also the subject of considerable standards effort. There is already an international standard for network protocols: the ISO OSI. However, most UNIX systems have historically used a different protocol: TCP/IP. Trying to resolve differences among OSI, TCP/IP, and other network protocols will be difficult.

## Profiles and POSIX Standards

An important concept in the POSIX lexicon is that of a profile. As the number of standards grows, the number of combinations of standards grows exponentially. However, the number of sensible, coherent combinations is much smaller. Many of the POSIX committees are developing AEPs (application environments) rather than standards. An AEP is a “standard collection of standards” suitable for a particular application area. For example, the POSIX.10 developed a supercomputing AEP. This profile references a number of standards that would be useful for applications that run on supercomputers. These standards include POSIX.1, POSIX.2, the ISO Fortran (Fortran 90) standard, and the C standard. A user who needs the resources of a supercomputer will typically need the features provided by more or all of these standards.

Profiles are most useful as tools for procurements, particularly by large organizations, such as government agencies. Typically such organizations requiring conformance to one or two standards does not adequately specify their needs. For example, although POSIX.1 standard is quite useful and widely referenced, knowing that your system conforms to POSIX.1 does not by itself guarantee you much; most complex applications require facilities well within the scope of POSIX.1.

If you are going to ask hardware vendors to propose systems to satisfy a complex set of requirements, using a profile makes your job simpler. Thus it is not surprising that the U.S. government and the European Commission are actively involved in the development of POSIX profiles and also develop profiles for their own purposes. As the number of POSIX standards grows, these standards are taking a central place in government profiles.

## Appendix Summary

The IEEE POSIX committees have developed standards for programming and user interfaces, based on historical UNIX practice and standards. Most of the standards are compromises between versions of System V and versions of BSD, with a few innovations where compromise was not possible or technically inadvisable. The standards have met with broad acceptance from government bodies and industry organizations.

POSIX.1 standardizes C language interfaces to the core UNIX system facilities; Ada and FORTRAN versions of these interfaces are specified by POSIX.5 and POSIX.9. POSIX.2 standardizes a shell and a collection of utilities useful for scripts and interactive use, specifying how these tools should behave in international environments in which character sets and local conventions differ from those in the original UNIX environment. POSIX.4 specifies interfaces for real-time programs executing in UNIX-like environments.

Standards under development will cover parts of system administration, extended system security, networks, and user interfaces. Existing UNIX (and therefore GNU/Linux) system practice in all these areas forms the basis of new standards. In turn, innovations from these standards will find their way into future UNIX and GNU/Linux systems.

## IN THIS APPENDIX

The Free Software Definition 1449

## The Free Software Definition

| Croatian | Czech | Danish | Dutch | English | French | Galician | German | Hungarian | Indonesian | Italian | Japanese | Korean | Norwegian | Polish | Portuguese | Russian | Slovenian | Spanish | Turkish | 1

We maintain this free software definition to show clearly what must be true about a particular program for it to be considered free software.

"Free software" is a matter of liberty, not price. To understand the concept, you should think of "free" as in "free speech," not as in "free beer."

Free software is a matter of the users' freedom to run, copy, distribute, change and improve the software. More precisely, it refers to four kinds of freedom, for the users of the software:

- The freedom to run the program, for any purpose (freedom 0).
- The freedom to study how the program works, and adapt it to your needs (freedom 1). Access to the source code is a precondition for this.
- The freedom to redistribute copies so you can help your neighbor (freedom 2).
- The freedom to improve the program, and release your improvements to the public, so that the whole community benefits. (freedom 3). Access to the source code is a precondition for this.

1. This material is at www.gnu.org/philosophy/free-sw.html on the GNU site. Because GNU requests a verbatim copy, links remain in place (underlined). View the document on the Web to ensure you are reading the latest copy and to follow the links.

## Appendix E. The Free Software Definition

A program is free software if users have all of these freedoms. You should be free to redistribute copies, either or without modifications, either gratis or charging a fee for distribution, to anywhere. Being free to do these things means (among other things) that you do not have to ask or pay for permission.

You should also have the freedom to make modifications and use them privately in your own work or program, without mentioning that they exist. If you do publish your changes, you should not be required to notify anyone in particular, or in any particular variety.

The freedom to use a program means the freedom for any kind of person or organization to use it on any kind of computer system, for any kind of job, and without being required to communicate subsequently with the developer or any other specific entity.

The freedom to redistribute copies must include binary or executable forms of the program, as well as source code, for both modified and unmodified versions. (Distributing programs in runnable format is necessary for conveniently installed operating systems.) It is ok if there is no way to produce a binary or executable form (since some languages do not support that feature), but you must have the freedom to redistribute such forms if you find or develop a way to make them.

In order for the freedoms to make changes, and to publish improved versions, to be meaningful, you must have access to the source code of the program. Freedom, accessibility of source code is a necessary condition for free software.

In order for these freedoms to be real, they must be irrevocable as long as you do not right; if the developer of the software has the power to revoke the license, without doing anything to give cause, the software is not free.

However, certain kinds of rules about the manner of distributing free software are acceptable, when they don't conflict with the central freedoms. For example, copyleft (very simply stated) is the rule that when redistributing the program, you cannot add restrictions to deny other the central freedoms. This rule does not conflict with the central freedoms; rather it protects them.

Thus, you may have paid money to get copies of GNU software, or you may have obtained copies at no charge. But regardless of how you got your copies, you always have the freedom to copy and change the software, even to sell copies.

“Free software” is a matter of liberty, not price. To understand the concept, you should think of "free" as in "free speech," not as in "free beer."

Free software is a matter of the users' freedom to run, copy, distribute, change and improve the software. More precisely, it refers to four kinds of freedom, for the users of the software:

- The freedom to run the program, for any purpose (freedom 0).
- The freedom to study how the program works, and adapt it to your needs (freedom 1). Access to the source code is a precondition for this.
- The freedom to redistribute copies so you can help your neighbor (freedom 2).
- The freedom to improve the program, and release your improvements to the public, so that the whole community benefits. (freedom 3). Access to the source code is a precondition for this.

1. This material is at www.gnu.org/philosophy/free-sw.html on the GNU site. Because GNU requests a verbatim copy, links remain in place (underlined). View the document on the Web to ensure you are reading the latest copy and to follow the links.

A program is free software if users have all of these freedoms. You should be free to redistribute copies, either or without modifications, either gratis or charging a fee for distribution, to anywhere. Being free to do these things means (among other things) that you do not have to ask or pay for permission.

You should also have the freedom to make modifications and use them privately in your own work or program, without mentioning that they exist. If you do publish your changes, you should not be required to notify anyone in particular, or in any particular variety.

The freedom to use a program means the freedom for any kind of person or organization to use it on any kind of computer system, for any kind of job, and without being required to communicate subsequently with the developer or any other specific entity.

The freedom to redistribute copies must include binary or executable forms of the program, as well as source code, for both modified and unmodified versions. (Distributing programs in runnable format is necessary for conveniently installed operating systems.) It is ok if there is no way to produce a binary or executable form (since some languages do not support that feature), but you must have the freedom to redistribute such forms if you find or develop a way to make them.

In order for the freedoms to make changes, and to publish improved versions, to be meaningful, you must have access to the source code of the program. Freedom, accessibility of source code is a necessary condition for free software.

In order for these freedoms to be real, they must be irrevocable as long as you do not right; if the developer of the software has the power to revoke the license, without doing anything to give cause, the software is not free.

However, certain kinds of rules about the manner of distributing free software are acceptable, when they don't conflict with the central freedoms. For example, copyleft (very simply stated) is the rule that when redistributing the program, you cannot add restrictions to deny other the central freedoms. This rule does not conflict with the central freedoms; rather it protects them.

Thus, you may have paid money to get copies of GNU software, or you may have obtained copies at no charge. But regardless of how you got your copies, you always have the freedom to copy and change the software, even to sell copies.

“Free software” is a matter of liberty, not price. To understand the concept, you should think of "free" as in "free speech," not as in "free beer."

Free software is a matter of the users' freedom to run, copy, distribute, change and improve the software. More precisely, it refers to four kinds of freedom, for the users of the software:

- The freedom to run the program, for any purpose (freedom 0).
- The freedom to study how the program works, and adapt it to your needs (freedom 1). Access to the source code is a precondition for this.
- The freedom to redistribute copies so you can help your neighbor (freedom 2).
- The freedom to improve the program, and release your improvements to the public, so that the whole community benefits. (freedom 3). Access to the source code is a precondition for this.

1. This material is at www.gnu.org/philosophy/free-sw.html on the GNU site. Because GNU requests a verbatim copy, links remain in place (underlined). View the document on the Web to ensure you are reading the latest copy and to follow the links.

A program is free software if users have all of these freedoms. You should be free to redistribute copies, either or without modifications, either gratis or charging a fee for distribution, to anywhere. Being free to do these things means (among other things) that you do not have to ask or pay for permission.

You should also have the freedom to make modifications and use them privately in your own work or program, without mentioning that they exist. If you do publish your changes, you should not be required to notify anyone in particular, or in any particular variety.

The freedom to use a program means the freedom for any kind of person or organization to use it on any kind of computer system, for any kind of job, and without being required to communicate subsequently with the developer or any other specific entity.

The freedom to redistribute copies must include binary or executable forms of the program, as well as source code, for both modified and unmodified versions. (Distributing programs in runnable format is necessary for conveniently installed operating systems.) It is ok if there is no way to produce a binary or executable form (since some languages do not support that feature), but you must have the freedom to redistribute such forms if you find or develop a way to make them.

In order for the freedoms to make changes, and to publish improved versions, to be meaningful, you must have access to the source code of the program. Freedom, accessibility of source code is a necessary condition for free software.

In order for these freedoms to be real, they must be irrevocable as long as you do not right; if the developer of the software has the power to revoke the license, without doing anything to give cause, the software is not free.

However, certain kinds of rules about the manner of distributing free software are acceptable, when they don't conflict with the central freedoms. For example, copyleft (very simply stated) is the rule that when redistributing the program, you cannot add restrictions to deny other the central freedoms. This rule does not conflict with the central freedoms; rather it protects them.

Thus, you may have paid money to get copies of GNU software, or you may have obtained copies at no charge. But regardless of how you got your copies, you always have the freedom to copy and change the software, even to sell copies.

“Free software” is a matter of liberty, not price. To understand the concept, you should think of "free" as in "free speech," not as in "free beer."

Free software is a matter of the users' freedom to run, copy, distribute, change and improve the software. More precisely, it refers to four kinds of freedom, for the users of the software:

- The freedom to run the program, for any purpose (freedom 0).
- The freedom to study how the program works, and adapt it to your needs (freedom 1). Access to the source code is a precondition for this.
- The freedom to redistribute copies so you can help your neighbor (freedom 2).
- The freedom to improve the program, and release your improvements to the public, so that the whole community benefits. (freedom 3). Access to the source code is a precondition for this.

1. This material is at www.gnu.org/philosophy/free-sw.html on the GNU site. Because GNU requests a verbatim copy, links remain in place (underlined). View the document on the Web to ensure you are reading the latest copy and to follow the links.

A program is free software if users have all of these freedoms. You should be free to redistribute copies, either or without modifications, either gratis or charging a fee for distribution, to anywhere. Being free to do these things means (among other things) that you do not have to ask or pay for permission.

You should also have the freedom to make modifications and use them privately in your own work or program, without mentioning that they exist. If you do publish your changes, you should not be required to notify anyone in particular, or in any particular variety.

The freedom to use a program means the freedom for any kind of person or organization to use it on any kind of computer system, for any kind of job, and without being required to communicate subsequently with the developer or any other specific entity.

The freedom to redistribute copies must include binary or executable forms of the program, as well as source code, for both modified and unmodified versions. (Distributing programs in runnable format is necessary for conveniently installed operating systems.) It is ok if there is no way to produce a binary or executable form (since some languages do not support that feature), but you must have the freedom to redistribute such forms if you find or develop a way to make them.

In order for the freedoms to make changes, and to publish improved versions, to be meaningful, you must have access to the source code of the program. Freedom, accessibility of source code is a necessary condition for free software.

In order for these freedoms to be real, they must be irrevocable as long as you do not right; if the developer of the software has the power to revoke the license, without doing anything to give cause, the software is not free.

However, certain kinds of rules about the manner of distributing free software are acceptable, when they don't conflict with the central freedoms. For example, copyleft (very simply stated) is the rule that when redistributing the program, you cannot add restrictions to deny other the central freedoms. This rule does not conflict with the central freedoms; rather it protects them.

Thus, you may have paid money to get copies of GNU software, or you may have obtained copies at no charge. But regardless of how you got your copies, you always have the freedom to copy and change the software, even to sell copies.

“Free software” is a matter of liberty, not price. To understand the concept, you should think of "free" as in "free speech," not as in "free beer."

Free software is a matter of the users' freedom to run, copy, distribute, change and improve the software. More precisely, it refers to four kinds of freedom, for the users of the software:

- The freedom to run the program, for any purpose (freedom 0).
- The freedom to study how the program works, and adapt it to your needs (freedom 1). Access to the source code is a precondition for this.
- The freedom to redistribute copies so you can help your neighbor (freedom 2).
- The freedom to improve the program, and release your improvements to the public, so that the whole community benefits. (freedom 3). Access to the source code is a precondition for this.

1. This material is at www.gnu.org/philosophy/free-sw.html on the GNU site. Because GNU requests a verbatim copy, links remain in place (underlined). View the document on the Web to ensure you are reading the latest copy and to follow the links.

## Other Texts to Read

Another group has started using the term "open source" to mean something close
(but not identical) to "free software". We prefer the term "free software" because,
once you have heard it refers to freedom rather than price, it calls to mind freedom.
