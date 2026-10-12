The first IRC clients were text-only. They were most often written with the use of the curses library, which is used to program terminal-independent, text-only user interfaces. The most popular of these text-based IRC clients is probably the ircII client, especially if you count the numerous spin-offs and clones of it that are available.

Later on several IRC clients with graphical user interfaces appeared on the Internet scene. The introduction of these clients has certainly helped to increase the popularity of IRC among less computer literate users. One of the most popular GUI clients is undoubtedly mIRC, which is only available for the Windows operating system. There are several very good GUI IRC clients available for Linux.

This chapter will look at both a GUI and a non-GUI IRC client that are included with the Red Hat 7 distribution. It will examine the non-GUI IRC client first because many of the commands that are used with it can also be used in the GUI client. You will get a much better understanding of how IRC works by seeing what commands are available and how they are used.

# Using a Non-GUI IRC Client—ircII

The ircII client sprang from the original irc client created by Jarkko Oikarinen. It is widely used and most likely one of the most popular non-GUI IRC clients ever. There are several IRC clients that are either based on the ircII source or that clone the behavior of ircII. The command setup used in ircII has become so popular that the same, or very similar, commands are now widely used in several other UNIX programs, especially in other IRC clients. However, this might not be so strange since the commands are very similar to the actual commands used within the IRC protocol, which is used for the communication between the client and the server.

# Tip

Another very popular IRC client is bitchx. This is not included with the Red Hat 7 distribution. However, if you like to use IRC via a non-GUI client, you will probably want to get your hands on bitchx. It has many enhancements and improvements over ircII. For example, it handles uploading and downloading of files via dcc and it also has support for ANSI graphics and mIRC colors. The bitchx client is available as an RPM package and you can find it at <http://www.bitchx.org/>.

GUI clients try to shield the user from having to use the sometimes obscure commands of text-only clients. Even so, most GUI clients also support the use of /-like commands. Since IRC to a large extent is about constantly typing, it can be much faster to actually