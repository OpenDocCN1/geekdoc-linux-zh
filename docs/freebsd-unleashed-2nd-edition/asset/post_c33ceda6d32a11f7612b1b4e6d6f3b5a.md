
with the remainder comprised of NetBSD, OpenBSD, and a few other little-known variants. In the wider server market, Windows NT/2000 claims about a 20- to 30-percent share, with Unix (both commercial and open source) estimated at about 65 percent. By any measure, this means FreeBSD is not an especially large player. However, market share alone does not dictate the quality of a piece of software (as anyone reading this book likely knows).

FreeBSD usage is growing. A steady stream of Linux-based and commercial Unix-based businesses are moving to FreeBSD for its stability and its performance, desiring an open-source solution that’s free of the distribution politics of Linux (which is true because of its nature—FreeBSD is a complete operating system, whereas Linux is simply a kernel). Stories also abound of high-profile, Web-based services running on FreeBSD simply because it is the only solution that can handle the load (the services’ parent companies’ own operating systems notwithstanding). The end result is an increasing respect for FreeBSD in the server community, and a growing desire to move toward its tempting mixture of stability, standards compliance, openness, and power.

Migration away from Windows NT/2000 or Linux means a tradeoff of two things: software availability and established practices. These two things are the largest stumbling blocks typically faced by seasoned server veterans eyeing FreeBSD for the first time—the former applying more significantly to Windows (because more and more Linux programs are being ported to FreeBSD); the latter applying to both. The following sections look at both these migration paths in turn and address the barriers.

## Migrating from Windows NT/2000

If you’re switching to FreeBSD from a Windows server platform, the problems you are most likely to face involve not just what software is available but a number of fundamental differences in how the computer is used. The topological role a Windows server plays in a network is quite different from that of a FreeBSD server.

Windows NT/2000 is almost exclusively GUI based, without a mature or widely used remote administration method. This means that to use Windows NT/2000 effectively, you usually need to be physically sitting at the machine. Getting used to a command-line interface to do your work can be a daunting task, but it’s crucial to Unix systems’ great advantage of remote accessibility.

In this section of the chapter, you learn that setting up a FreeBSD server to provide certain common services involves much less commercial software, licensing, and client/server installation than is required to set up other servers. You learn about migrating client/server applications to the FreeBSD system, and you learn information about some of the important differences in maintaining security in FreeBSD rather than Windows 2000. An important part of keeping your system secure is keeping your system up to date; later in this section, you learn how to keep your FreeBSD system current with the latest developments. Of course, one big difference you’ll notice when you migrate from Windows to FreeBSD is the change in software availability, licensing, and registration. When you move to FreeBSD, you deal with free and open-source software packages that you compile yourself, with support coming from grassroots Internet sources or third-party support services rather than from large software vendors.

### NOTE

Built-in and third-party components of Windows NT/2000 are gradually increasing the remote accessibility of the platform. These days, you can manage services remotely that are controlled through the Services control panel, and various methods exist to acquire a DOS command line on the server machine. However, these are both subsets of the complete functionality of a system—they're limited to the functionality explicitly built in to the control mechanism you're using. Complete configurability of installed server software often relies on administrative client programs, as we'll discuss next.

### Client/Server Applications

Most enterprise software for Windows servers is developed on a model in which you install the server portion physically (generally from CD). In this model, you then install an administrative portion—a *client*—on your desktop machine as well as on the machine of anyone else who will be administering the server. “Terminal server” packages are available, which allow you to directly control the server machine itself, but due to the intensely graphical Windows GUI, these tools are much simpler and elegant to use. You must accept a major philosophical shift when moving to Unix.

There are virtually no specialized client/server applications for FreeBSD. Some operate through a graphical Web-based interface accessed by a common Web browser (for example, streaming audio/video servers, calendaring servers, and the like). For the most part, however, all administration takes place through a remote terminal.

SSH (or Telnet, as a recourse) is the dominant all-purpose tool for doing anything in the Unix world. Technologically, using Telnet is one of the most efficient and streamlined methods imaginable for working with the server—all you're sending and receiving is text. It's also the most versatile method, giving you much wider access to the server's operations than any graphical tool could. Naturally, though, this also means you have more power to break things. It's a tradeoff: the ease of use, safety, and directed functionality of Windows client/server software for the versatility, risk, and esoterica of terminal-based administration.

### Security

Whole books have been written on the Windows NT/2000 security model, and the topic is well beyond the scope of this chapter. However, if you're used to the Windows style of users, domains, and permissions and you're moving to FreeBSD, there are a few things you'll want to know that will help you keep your security model roughly intact.

The "root" account is the equivalent of "Administrator." That is hardly a secret. However, beyond that there are a few things you can do to keep your services running with their accustomed privileges and to give your trusted administrators exactly as much power as they need—and no more. The first step is to know what some of the fundamental differences are between the Windows NT/2000 and FreeBSD security models:

- FreeBSD uses the User, Group, and Other mode bits to specify ownership and permissions, whereas Windows NT/2000 use Access Control Lists. This scheme is discussed in Chapter 9, "Users, Groups, and Permissions."

- Windows NT/2000 has the concept of *trusted paths*, allowing for the implicit authentication of users coming from specified hosts. For instance, you can tell Windows to "trust" any user connecting from a particular computer under some or all circumstances, thus eliminating the need for user authentication where it isn't necessary. FreeBSD doesn't have this capability unless you use Kerberos, as you'll see in Chapter 29, "Network Security."

- Login names in FreeBSD must be 16 characters or fewer and contain only lowercase characters or digits. No spaces or special characters are allowed. In Windows, usernames can be as many as 20 characters long, although the same kinds of special-character restrictions apply.

- Windows NT/2000 has as many as 27 different assignable user rights for file modification and execution with various privileges. FreeBSD distinguishes between processes executed by root (the super-user), processes executed by individual users, and processes executed in *setuid* or "set user ID" mode, in which the process takes on the privileges of whoever owns the executed file.

- FreeBSD and Unix don't have hierarchical groups. Windows NT/2000 allows you to place a group of users inside another group, to an arbitrary depth; this is not possible in FreeBSD. All groups exist at the same *level*.

- Windows "domains" don't exist in the Unix world. Instead, remote authentication services (as with the Domain Controller in Windows NT/2000) and security domains are handled by the NIS or "yellowpages" system. Details on NIS can be found in *man nis*.

- Peer-to-peer file sharing, done by NetBIOS under Windows, is typically done over NFS between Unix systems. You can do Windows-style NetBIOS file and printer sharing in FreeBSD by using the Samba package. NFS is covered in Chapter 32, "The Network Filesystem (NFS)," and Samba is discussed in Chapter 33, "File and Print Sharing with Microsoft Windows."

- Windows uses the Authenticode scheme for verifying code authenticity in downloaded software packages. This is a signing scheme by which downloaded software must present a "certificate" to the user for acceptance or rejection, adding a layer of security against potentially malicious software. Unix has no such standardized
