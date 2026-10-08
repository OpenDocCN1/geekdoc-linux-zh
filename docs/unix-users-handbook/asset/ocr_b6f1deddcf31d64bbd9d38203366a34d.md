In this chapter, I provide primarily background rather than setup information on many networking topics, because setup is predominately performed by system administrators. Most of what I cover is sometimes called "Internet Services." In general, I am going to cover the basics of networking in this chapter. This includes ARPA and Berkeley Services. Here is a list of topics I cover:

+   - General UNIX networking background
- Internet Protocol (IP) addressing (classes A, B, and C)
- Subnet mask
- ARPA Services
- Berkeley commands
- Host name mapping
- Network File System (NFS) background
- UNIX networking commands
- Some examples

I provide summaries and examples of many UNIX commands in this chapter. A great deal more detail can be found in the manual pages for these commands. I provide the full manual pages at the end of this chapter for many of the commands covered.

I use a variety of systems in the examples in this chapter, including Solaris, AIX, and HP-UX.

# ## UNIX Networking

Connecting to other machines is an important part of every UNIX network. This means connecting both to other UNIX machines as well as to non-UNIX machines. The machines must be physically connected