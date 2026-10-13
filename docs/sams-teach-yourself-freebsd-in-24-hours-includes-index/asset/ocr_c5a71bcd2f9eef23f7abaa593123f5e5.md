# Summary

In this, the final hour of our course on FreeBSD, you learned how to turn your machine into a file-sharing server and client using a variety of protocols. You learned how to set up an FTP server, both for authenticated and anonymous users. You learned how to use NFS, sharing files back and forth over a networked filesystem. Finally, you learned how to set up a basic Samba configuration in order to communicate with Windows machines on a local network.

Each of these protocols, particularly NFS and Samba, is a great deal more flexible than our coverage here indicates; if you find that you have the need and the desire, you will be able to extend your knowledge of these protocols to the point at which you can increase the performance and convenience (as well as the security) of your file-sharing mechanisms to whatever level you prefer.

# Q&A

Q What's the point of using FTP to serve files? Why not just use HTTP?

A HTTP has indeed supplanted much of the purpose for FTP's existence, particularly in the case of large binary downloads (such as software archives). However, FTP has advantages in its dual-channel connection model (which allows it to operate through firewalls), its built-in user authentication, the ability to upload files and perform filesystem operations on the server, and the fact that its transport mechanism is tuned to support large binary files rather than small text/HTML files (as with HTTP).

Q My /var partition is too small to hold a large public anonymous FTP archive.

A You can create a location in another, larger partition to hold the content that would normally go into /var/ftp. For example, move the contents of /var/ftp to /usr/ftp, and then make a symbolic link there with the following command:

```
ln -s /usr/ftp /var/ftp.
```

Q Isn't there a way to browse NFS shares on a local network?

A There is, actually. A system called Service Location Protocol (SLP) is available to help machines on a LAN track each other's NFS services. You can install OpenSLP (a free implementation of SLP) from the ports, at /usr/ports/net/openslp.