network (locally, you can use write) to a logged-in user without having to log
in another computer.

sendfile can only be used if the appropriate server is running on the
target computer, which currently is seldom the case. Furthermore, the computer
must be directly reachable via TCP/IP. If you send files via mail, the target
computer does not even need to be online, provide a corresponding MX entry
exists for the computer in the DNS.

The system administrator can prohibit the use of this service to individual
users in the file /usr/local/etc/nosendfile Each user can create a file
with aliases for destinations. The transmission of files and messages from alien
computers can be prohibited.

Another function often missed under UNIX is sending a short message to a
logged-in user. If this user works on the same computer, you can use the write
command. However, if the user is logged in on another computer, you cannot
write. If sendfile is installed, you can send a brief message with sendmsg
which is immediately displayed to the user.

| Additional Information and Sources |
| --- |--- |
| Author: | Uli Horlacher |
| email: | framstag@rus.uni-stuttgart.de |
| ftp server: | ftp.uni-stuttgart.de/ |
| ftp path: | /pub/unix/comm/sendfile/ |
| File: | sendfile.tar.gz |
| Size: | about 300 Kbytes |