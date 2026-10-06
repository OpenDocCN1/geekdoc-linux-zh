# CHAPTER 27 Lightweight Directory Access Protocol (LDAP) 701

+   3. In the Authentication Configuration screen, navigate to (using TAB on keyboard) and then select (using SPACEBAR on your keyboard) the following:

+   - Use LDAP Under the User Information section

+   - Use LDAP Authentication Under the Authentication section

+   4. Navigate to the Next button and press ENTER to select it.

+   5. Use the following information to complete the fields in the ensuing LDAP Settings screen:
Server: Idap://server-A/
Base DN: dc=example,dc=org

These fields refer the URI of our sample LDAP server using its hostname (you can also specify an IP address) and the Base DN of the directory.

+   6. After entering the information, navigate to the OK button and press ENTER to select and save your settings.

That's it. You are done.
We described a simple way to enable a Fedora client system to use Open LDAP server for your user authentication. We did not bother with a lot of details, because this is just a proof of concept. Following are some of the details you might have to deal with in a real production environment:

+   - Home directories You may have to ensure that users' home directories are available to when they're logging in any system. One way to do this is by sharing home directories via Network File System (NFS) and exporting to all client systems.

+   - Security Our sample setup did not have any security measures built into the infrastructure. This should be of paramount importance in a production environment so that user passwords do not go flying across the network in plain text.

+   - Miscellaneous Other issues weren't addressed here, but we'll leave them as a mental exercise for you to stumble upon ponder.

> TIP Take a look at the FreeIPA project (www.freeipa.org) for a canned identity management solution that combines and extends various concepts and solutions discussed in this and other chapters. FreeIPA is an integrated solution that uses Linux (Fedora, CentOS, RHEL, and so on), 389 Directory Server, MIT Kerberos, NTP, and DNS.