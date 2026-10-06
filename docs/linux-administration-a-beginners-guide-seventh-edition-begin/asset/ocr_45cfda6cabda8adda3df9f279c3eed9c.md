# CHAPTER 23 Network File System (NFS) 605

# Versions of NFS

The protocol behind NFS has evolved and changed a lot over the years. Standards committees have helped NFS evolve to take advantage of new technologies, as well as changes in usage patterns. At the time of writing, three well-known versions of the protocol exist: NFS version 2 (NFSv2), NFS version 3 (NFSv3), and NFS version 4 (NFSv4). An NFS version 1 also existed, but it was very much internal to Sun Microsystems and, as such, never saw the light of day.

NFSv2 is the oldest of the three. NFSv3 is the standard with the widest use. NFSv4 has been in development for a while and is the newest standard. NFSv2 should probably be avoided if possible and should be considered only for legacy reasons. NFSv3 should be considered if stability and widest range of client support are desired. NFSv4 should be considered if its bleeding-edge features are enabled and probably for very new deployments where backward compatibility is not an issue.

Perhaps the most important factor in deciding which version of NFS to consider would be the version your clients will support.
Here are some of the features of each NFS version:

+   - NFSv2 Mount requests are granted on a per-host basis and not on a per-user basis. This version uses Transmission Control Protocol (TCP) or User Datagram Protocol (UDP) as its transport protocol. Version 2 has a file size limitation of less than 2GB that they can access.

+   - NFSv3 This includes a lot of fixes for the bugs in NFSv2. It has more features than version 2, performance gains over version 2, and can use either TCP or UDP as its transport protocol. Depending on the local file system of the NFS itself, clients can access files larger than 2GB in size. Mount requests are also granted on a per-host basis and not on a per-user basis.

+   - NFSv4 This version of the protocol uses a stateful protocol such as TCP or Stream Control Transmission Protocol (SCTP). It has improved security features such as Kerberos; for example, client authentication can be conducted on a per-user or a principal basis. It was designed with the Internet in mind, and as a result, this version of the protocol is firewall-friendly and listens on the well-known port 2049. The services of the RPC binding protocols (such as rmount, lockd, and statd) are no longer required in this version of NFS because their functionality has been built into NFSv4 combines these previously separate protocols into a single protocol specification. (The portmap service is no longer necessary.) It support for file access list (ACL) attributes and can support both version 2 and version 3 clients. NFSv4 introduces the pseudo-file system, which allows NFSv4 clients to see and access the file systems operated on the NFSv4 server as a single file system. NFSv4 is currently at minor revision 1 (NFSv4.1) with revision 2 (NFSv4.2) already in the works.