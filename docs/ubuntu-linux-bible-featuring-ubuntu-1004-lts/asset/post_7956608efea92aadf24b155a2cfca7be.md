
## Chapter 25: Connecting to Other Systems

and store it in the directory ~/.tsclient in your home directory. In the future, you can select one of these files after starting tsclient, enter your password, and quickly establish a connection to the indicated terminal server.

## Using Other Remote Connection Software

Although it is not supplied as part of a default Ubuntu linux installation, another popular software package for graphically connecting to remote systems is the free version of NoMachine NX, known as FreeNX (named freienx) is not provided in the Ubuntu repositories and is not installed by a standard Ubuntu system, primarily because its Linux clients are KDE-based, and therefore many KDE libraries. However, versions of FreeNX are available from some of the default, user-supported repositories listed in Chapter 19. See that for additional information.

FreeNX is a free, GPL implementation of NoMachine's NX (NoMachine NX) Server (www.nomachine.com). NoMachine has developed a compression technology that substantially reduces the size of X Window communications and adds other performance improvements through caching and general protocol optimization. The NX application clients are included in the FreeNX package—the clients for Microsoft Windows, Mac OS, and Solaris are available as free downloads from the NoMachine site. The free and commercial versions of the NX server differ primarily in terms of capabilities (and, of course, cost). FreeNX provides all of the core capabilities of the commercial NX server for remote connections, but does not currently include the SMB and printing (Common Unix Printing System) support provided by the commercial NX server.

If you're already a VNC fan, NX is definitely worth a look for its superb compression technologies and associated performance improvements, and also because it inherently uses SSH for communications between client and server. FreeNX is effectively equivalent to VNC and supports Linux Terminal Server (www.ltsp.org), Windows Terminal Server, Citrix Metaframe, and standard X Window DMC (Display Manager Control Protocol). However, it is not part of any official Ubuntu repository from Canonical, so you won't be able to get support from them if you encounter any problems. (You may still get free sympathy,.)

## Summary

Networking is a given in today's academic, business, and home computing environments. The need to access more and different systems goes hand-in-hand with that. This chapter discussed command-line mechanisms for connecting to remote Linux and UNIX systems and explained how to install the SSH server on your system so that people can securely connect to your Ubuntu system. I then explored VNC (Virtual Network Computing) clients that enable you to remotely connect to the consoles of graphical systems such as Microsoft Windows, Mac OS X, Linux, and UNIX systems. The chapter concluded by discussing mechanisms for connecting to a Microsoft Windows Terminal Server from your Ubuntu system, and then introduced the popular NX and FreeNX software that enables you to securely connect to just about any remote graphical console service.

The next chapter discusses the related topic of connecting to remote file servers to access files that are stored on them, and explains how to share files from your Ubuntu system so that other systems on your network can quickly and easily access them. Music server, anyone?

## File Transfer and Sharing

Sooner or later, you're going to want to copy a file to or from another computer system. In the old days before networking and e-mail (which you may not even remember), this usually involved writing a copy of the file to removable media of some sort, such as a floppy disk, carrying that floppy from one system to the other, and then copying the file from the floppy disk to the other system. This was known as sneaker net—you just can't beat that humor!

Today, to the fact that networking is almost ubiquitous and that most businesses and many homes have their own networks, electronic file transfer is an important capability. There are many ways to transfer or copy files from systems, ranging from Point-to-Point (PPP) file transfers to the Peer-to-Peer (P2P) file transfers much beloved of the music and film industries. In Point-to-Point file transfers, you explicitly copy a file from one system to another, and you therefore know the addresses or identities of both hosts. In Peer-to-Peer transfer, groups of files share with each other without necessarily knowing or caring about the specific systems from which they are getting the files or to they are sending. In Peer-to-Peer transfers, somebody obviously has to know what hosts are sharing what files, but this is usually built into the software—more about later in this chapter.

The first section of this chapter discusses popular Point-to-Point file transfer solutions that are built into your Ubuntu Linux system. The second section of this chapter, "Peer-to-Peer File Sharing on Ubuntu," discusses various P2P solutions that are easily installed and used on your system.

## IN THIS CHAPTER

- Transferring files between systems
- Sharing files with Windows systems
- Sharing files with Linux and UNIX systems
- Sharing files Peer-to-Peer
- Using BitTorrent

## Part II: Ubuntu for Desktop Users

## Note

You may have noticed by now that I am not a lawyer and I have significant disdain for industry groups that try to suppress technologies just because they can be used to do something that may be illegal. Heck, I could conceivably club someone to death with my laptop, but does that mean that we should outlaw laptops? There is absolutely nothing inherently illegal about Peer-to-Peer file sharing. P2P is a great way to easily share and transfer large files among multiple systems, with everyone sharing part of the load. What you do with your business is explaining how you can use it is mine.

## Transferring Files to Other Systems

As noted in the introduction to this chapter, this section discusses how to copy files between systems in cases which you know the identities of the machines involved in the transfer. Common examples of this sort of file transfer are "I need to copy this file from my laptop to the machine on my desk," "I want to put this file on our home media server, so we can play it from any machine in the house," or "I need to put this spreadsheet on the company file server so my boss can see that I'm actually working from home." In each of these cases, you have authorized access to the machines at both ends of the transfer and you know their names, whether by qualified hostname (www.vonhagen.org), IP address (74.86.122.100), or your local hostname on your network (laptop, server1, etc.). You'll also know the name of the directory in which the file you are looking for, and the name of the Windows share in that file is located for SMB/CIFS file server.

In having authorized access to the system that you're transferring to, the appropriate service already be running on the remote system, holding up a sort of electronic catcher's mitt that can receive the files you're transferring there. This chapter focuses on the client side of file transfers—transferring files to something that's ready to receive, and doing anything you need to do to enable your local machine to reach them. This chapter doesn't discuss how to set up shared directories on Microsoft Windows or Linux systems. For information on sharing Linux directories so that you can reach them directly from a PC running Microsoft Windows, Mac OS X, or Linux, see Chapter 35, "Setting Up a Samba Server." For on sharing Linux directories via NFS so that you can reach them directly from a PC running Mac OS X or Linux, see Chapter 34, "Setting Up an NFS Server." You can also contact NFS Servers from Microsoft Windows but only by installing special software that doesn't come with default.) Information about setting up an FTP server is provided as a sidebar in this chapter, I received a few requests for information on that topic from readers of the first edition of this book.

## Tip

Another common file transfer scenario is,"My brother would really like a copy of this file." In that case, I'd suggest just attaching the file to an e-mail message and sending it to him, as long as the file in question is under the size of any quota that is imposed by the recipient's e-mail server and the e-mail server doesn't block files with specific extensions (you can always change the file extension). You don't know the name of his machine or its IP address, and probably don't have direct access to the machine anyway.
