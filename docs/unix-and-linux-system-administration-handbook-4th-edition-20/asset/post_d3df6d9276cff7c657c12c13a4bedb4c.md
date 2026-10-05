
# Organizations, conferences, and other resources

then wrote a memo to the boss asking to correct the situation and documenting the number of copies of the software that were licensed and the number that were in use. The admin quoted a few phrases from the license agreement and copied the precedent of the company and his boss's managers. In one case, this procedure worked and the sysadmin's manager was let go. In another case, the sysadmin quit when even higher management refused to do the right thing. No matter what you do in such a situation, things gets writing. For a written reply, or if all you get is spoken words, write short memo documenting your understanding of your instructions and send it to the person in charge.

## 32.11 ORGANIZATIONS, CONFERENCES, AND OTHER RESOURCES

Many Unix and Linux support groups—both general and vendor specific—help you network with other people who are using the same software. Table 32.3 presents a list of organizations, but plenty of other national and regional groups are not listed in this table.

## Table 32.3 UNIX and Linux organizations of interest to system administrators

| Name | URL | What is it |
| --- | --- | --- |
| FFS | ffs.org | Free Software Foundation, sponsor of GNU |
| USENIX | usenix.org | UNIX users group, quite technical |
| SAGE | sage.org | The System Administrators Guild associated with UNIX; holds the yearly LISA League of Professional System Administrators, a spinoff from UNIX/SAGE |
| LOPSA | lopsa.org | |
| SANS | sans.org | Runs sysadmin and security conferences; less technical than SAGE, with a focus on tutorials |
| The Linux Foundation | linuxfoundation.org | a nonprofit consortium dedicated to the growth of Linux |
| AUUG | auug.org.au | Australian Users Group, covers both technical and managerial of computing Australian SAGE, holds yearly conferences in Oz System Administration and Network Engineering group, has yearly conferences in Europe |
| SAGE-AU SANE | sage-au.org.au sane.nl | |

FSF, the Free Software Foundation, sponsors of the GNU project (“GNU’s Not Unix,” a recursive acronym). The “free” in the FSF is the name “free” of free speech and not of free beer. The FSF is also the origin of the GNU Public License, which is now in its third version and covers many of the free software packages used on USENIX and Linux systems.

USENIX, an organization of users of UNIX, and holds one general conference and several specialized (smaller) operating systems, conferences or workshops each year. The general conference has a parallel track devoted to open systems that features ongoing OS development in the Linux and BSD communities.

The big event for sysadmins is the USENIX LISA (Large Installation System Administration) conference held in late fall. Trade shows are often associated with these conferences.

As a service to the Linux community, the Linux Foundation operates a workshop dedicated to Linux kernel development. Access to this two-day event is by invitation only.

SAGE, USENIX's System Administrators Guild, is the first international organization for system administrators. It promotes administration as a profession by sponsoring conferences and informal programs. See sage.org for details.

SAGE, together with USENIX, its parent organization, puts on system and network administration conferences offering tutorials and technical sessions, invited talks, and help sessions. Occasionally, one-day workshops on special topics in parallel. For information, see usenix.org.

The USENIX and SAGE newsletter—login—is produced by both organizations; it contains administrative news, tips, reviews, and announcements of interest to sysadmins. SAGE has a list of resources for sysadmins. See sage.org for current information.

In 2005, a falling out between USENIX and SAGE left the future of SAGE in doubt. The result was that some of the old-timers in the SAGE organization formed a separate organization LOPSA, the League of Professional System Administrators, lopsa.org. As of early 2010, LOPSA does not hold conferences, but they do have some sessions scheduled. SAGE gave up its sysadmin certification program; let's hope LOPSA will pick it up.

SANS offers many courses and seminars in the security space and runs a certification-program. The exam format is multiple choice, open book, with a time limit. Applicants can take two practice exams before the real thing. Individual certification focuses on narrow topics; applicants can also earn a general security (GSEC) certification. Certification is valid for only 2–3 years, so you must keep up with recent developments and recertify (for an added fee) to stay current. See giac.org.

Many local areas have regional UNIX, Linux, or open systems groups. Some of these are affiliated with USENIX and are not. The local groups usually have regular meetings, workshops with local or visiting speakers, and often, differ together before or after the meetings. They’re a good way to network with other sysadmins in your area.

The premier trade show for the networking industry is Interop; its tutorial is of high quality. Interop used to be an annual event that was eagerly awaited by techies and vendors alike. Interop now happens several times a year—travel network circus, so to speak. The salaries of tutorial speakers have been cut in half, but the quality of the tutorials seems to have survived.

# Exercises

# 1231

## 32.12 RECOMMENDED READING

LIMONCELLI, THOMAS A. Time Management for System Administrators. Sebastasto-pol, CA: O'Reilly Media, 2005.

MACHIAVELLI, NICCOLÒ. The Prince. 1513.
Available on-line from gutenberg.org/etext/1232

BROOKS, FREDERICK P., Jr. The Mythical Man-Month: Essays on Software Engineering. Reading, MA: Addison-Wesley, 1995.

SENFT, SANDRA, AND FREDERICK GALLEGOS. Information Technology Control and Audit (3rd Edition). Boca Raton, FL: Auerbach Publications, 2008.

The site itil-toolkit.com is a great place to start if you seek to understand the mountains of jargon and management-speak associated with ITIL processes and standards.

The site itil.nist.org is the landing page for the NIST Information Technology Laboratory. Lots of information about standards. Go to the publications page.

The web site of the Electronic Frontier Foundation, eff.org, is a great place to find commentary on the latest issues in privacy, cryptography, and legislation. Always interesting reading.

sans.org/resources/policies hosts the SANS security policy project. Several good sample IT policies are available from this site.

Lots of resources for system administrators are also available on SAGE site: sage.org/field.html.

# 32.13 EXERCISES

E32.1 What are your recurring procedures? Which are reinvented each time? Which are risky?

E32.2 What are your dependencies on external providers? Do you need and have plan B? Explain why or why not. Describe plan B if it exists.

E32.3 Briefly interview internal customers to determine their expectations with respect to the computing infrastructure. Are the expectations reasonable? Are they consistent with the system administration group's goals?

E32.4 What organized infrastructure for system management is already established at your site? Identify the pieces that are still missing.

![](img/579ec8c67772f31ecf34844bbb71a2_png)

E32.5 One of your co-workers is going to leave for lunch tomorrow and never return, but you don't know which one. (No, you don't get to pick.) What critical procedures might be affected, and how prepared is your organization to cover for the staff staff?

E32.6 What would happen if you didn't come in for the next three months? How much would your colleagues feel when you finally come back, and why? What can you do in the next two weeks to reduce the trauma of such an event?

E32.7 Your boss orders you to cut the system administration budget by 30% by the end of the current year. Can you quantify the consequences of this cut? Present a summary that will allow the boss to make informed decision which services to reduce or discontinue.

E32.8 Who are some of the current major corporate supporters of Linux? What are their interests and motivations? What sort of contributions are they making?

E32.9 You are cleaning up after a disk crash and notice files in the lost+found directory. When you investigate further, you find that some of the files are mail messages that were sent between two students who are setting up a back door around the department firewall to archive MP3 files on a remote file server. What should you do? Are there policies or regulations in place that cover such incidents?

E32.10 Evaluate your site's local documentation for new users, sysadmins, standard procedures, and emergencies.

E32.11 Forecast the future of the various commercial and free UNIX Linux over the next five years. How will the current development and distribution models hold up over time? What will be the long-term impact of the adoption of Linux by hardware vendors? Differentiate between the server and desktop markets.
