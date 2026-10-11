should happen, the program returns a null pointer in line 52 to indi-
cate that the peer_addr() function was not fully successful.

+   8. The pointer to the caller's buffer is returned in line 54 to indicate that
+   the call was successful.

If you skimmed over the steps described, the improvement that was made to
the program is described in step 7.

# Interfaces and Addressing

Before you move onto other aspects of socket programming in the chapters
that follow, there is one other concept related to socket addresses that must
be understood. This is the concept of interface addresses.

Using the familiar telephone example again, imagine the President's office
where there are two (or more) telephones on his desk. Using one of the tele-
phones, he can contact his wife to see how her day is going. On the other
hand, using the red telephone gets him in touch with the Russian presi-
dent. Each of these two telephones is, in a sense, an interface between two
different networks. These are

+   - The normal domestic telephone network.
+   - A private network to the Russian president's high-ranking office(s) on
+   secure lines.

The important point in this example is that you must use the correct inter-
face (telephone) to reach the correct network. For example, the President
would be unable to call his wife on the red telephone. Conversely, the
domestic telephone would not be able to reach the Russian president's high-
ranking office telephones, which are on secure lines.

In a similar manner, there are times when you want your socket program to
specify which interface to use when attempting to contact a remote
socket. This is done when you know that one interface is the only way to
reach the destination network.

When you are expecting to receive a telephone call, there are times when
you want to receive calls only on a particular telephone. For example, the
teenage daughter might want to receive calls only on the telephone
installed in her bedroom. For others in the household, they expect to
receive telephone calls only in a downstairs room where the other telephone
is installed. Your socket program will likewise sometimes want to accept
connections from only one specific interface and ignore all others.

# Specifying an Interface Address Example

A concrete example is shown in Figure 5.1, which specifies an interface
address.