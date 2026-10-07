# Linux Web Server Toolkit

exchange data between applications, like the Web or your e-mail program. The next section takes a look at these protocols.

# Data Exchange Protocols

There are a number of protocols that allow information to be exchanged between Internet sites. You might wonder why a single protocol was not created to do every-thing we're now describing as separate protocols. The UNIX way of doing things is to have a set of tools, with each tool handling a specific task well. This way you can choose the exact set of tools that fits your needs and be guaranteed that everything will be done efficiently. This works because UNIX provides easy ways to connect tools together, so you don't waste time by using multiple tools instead of one large. So, to transport information across the Internet, many protocols were developed for specific purposes. You're probably familiar with some of these protocols. Because each was developed for a specific goal, it was refined over time to be very good at one thing. Table 4-3 lists some key Internet data exchange protocols, followed by the most commonly used.

There are dozens more that are not listed in Table 4-3, but they are used for specialized tasks that don't pertain to setting up your Web server on Linux. The exam-ples given here are the important ones for Web servers. Details about adding other features like FTP to your Web server are covered in Chapter 14.

# TABLE 4-3 Common Internet Data Protocols

| Protocol | Description |
|---|---|
| SMTP | Standard e-mail protocol |
| HTTP | The World Wide Web protocol |
| FTP | The File Transfer Protocol |
| WAIS | Used for WAIS searchable database indexes |
| Gopher | Used by gopher information services (a less graphical precursor to the Web; was very popular in universities) |
| NNTP | Newsgroups (such as comp.os.linux.announce or alt.fans.billyjoel) |
| Telnet | Remote login communication system |
| NFS | Network File System, for remote access to filesystems as if they were local |