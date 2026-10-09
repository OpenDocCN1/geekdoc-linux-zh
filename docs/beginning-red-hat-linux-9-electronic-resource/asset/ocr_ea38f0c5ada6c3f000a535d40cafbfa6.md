There are a number of benefits to be gained by implementing a file server:

+   - It reduces administration cost. Instead of having important data stored on many individual PCs (all of which would require backing up), you can store *all* your important data in one place (on the file server). Then, only the file server needs regular backing up.

+   - It provides the opportunity to enforce a more controlled and focused security policy, because the security policy needs only to be applied to the file server.

+   - It enables you to provide a more stable and reliable storage solution. It enables you to implement your storage solution on high-spec machines that provide high levels of uptime. Moreover, implementation of RAID or of mirrored SCSI disks (which help ensure data reliability) is more feasible on a central file server than on many PCs.

+   - There's also something to be gained in terms of cost of file storage (although this is less pertinent in these days of cheap storage). First, it makes best use of the available storage capacity by making it accessible to all users. Second, it provides a central repository from which common resources can be made available to all (eliminating the need for each user to store their own copy).

Once you've got a file system, what makes it a file server is the mechanism that enables the file system to be shared. There is plenty of software around for this purpose – Samba, the Network File System (NFS), the Andrew file system (AFS), and Coda are all examples. Some of these are shipped as part of the Red Hat Linux 9 distribution, and we're going to focus on one in particular – Samba.

*For more information on the others, see http://www.nfsv4.org, http://www.transarc.com/Product/EFS/AFS/index.html, and http://www.coda.cs.cmu.edu.*

# ## An Overview of Samba

**Samba** is an implementation of the Windows SMB and CIFS protocols on Unix. The Samba project was started by Andrew Tridgell, who wanted to mount his Unix server disk space onto a DOS PC. When he'd solved the problem, Tridgell discovered that what he'd built was an implementation of the SMB (server message block) protocol – a protocol for sharing files and other resources. Tridgell named his implementation Samba, and published version 1.0 in early 1992. Since that time, the Samba project has grown tremendously, and today there is still Samba development going on in the open source community.

So, Samba is a collection of programs that make it possible to share files and printers between computers equipped to use the SMB protocol – Windows by default, Linux/Unix with Samba, and (more recently) Mac OS X. Samba is freely available under GNU General Public License, and is included as part of the Red Hat Linux 9 distribution.