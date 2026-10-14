# PLANNING

The adage, “A stitch in time saves nine,” is certainly true when applied to system administration. Regrettfully, a significant amount of your work as an administrator is done under tremendous time constraints, with anxious users standing in the wings, if not actually in your office. Planning is often sacrificed in these circumstances. In the next few chapters, we discuss the fundamental concepts of installation, system startup and shutdown, the file-system, upgrades, and patches.

# INTEGRATION

Integration, with respect to this book, is the sharing of resources between diverse operating systems. For clarity, we need to compare this with interoperability and coexistence. The three are ascending levels of the same concept. Coexistence is simply the state of cohabitation on a network. There are often applications provided to facilitate the transfer of information between diverse systems, but not without direct manipulation by the user. Integration is the next level, providing shared resources among constituent systems. The most commonly shared resources are filesystems, email, information and domain services, printing, and networking. Interoperability is the highest level of interaction, with identical application resources made available regardless of the operating system. A common example of interoperability is a database application, which must be distributed throughout a heterogeneous environment.

Our focus will be on integration, the middle ground between coexistence and interoperability. Specifically, we will be concerned with creating a stable environment for the user to work with. Network address resolution, user and system identification, shared filesystems, email, printing, networking, and security are the key issues in creating an integrated infrastructure. We will discuss tools and strategies for accomplishing these goals between Windows 2000 and a variety of UNIX operating systems.

# ADMINISTRATION

The administrative tasks are, simply put, the most boring. However, they are easily the most critical to the users. Tasks in this part of the book deal directly with the users, or with the tools necessary to support them. Creating user accounts (and deleting them) is of obvious importance. Backups, performance-tuning, and developing user interfaces also affect the quality of the user environment. Many of the tools necessary to accomplish these tasks, and others in this book, are discussed here as well.

It is extremely easy to forget that the reason most systems and networks exist is to support some set of activities performed by users. We believe that