action, but it should make you suspicious because it can also indicate a break-in further advantage of the ssh is that X redirection takes place automatically. Again, the whole session is encrypted, and authentication is carried out by means of the ssh and not by means of xhost or xauth.

As you can see, the secure shell offers a significant increase in security and improves handling of the system. In my view, these programs belong to the standard equipment of every UNIX system since they are not only available for Linux, but also for almost all other UNIX systems. Ssh2 is advanced and probably more secure than ssh, but the necessary license is a drawback. Openssh be the program of choice (http://www.openssh.com).

If you have problems with the programs, you should start the daemon with the option -d (for debugging) and the client with the option -v (for verbose). Both programs will generate extensive protocols in all steps that have been carried out can be viewed. With these instruments, you should be able to track down all problems quite quickly.

Besides authentication via host name and RSA key as described, there are several further options. An even more secure one is the exclusive use of RSA for authentication, where only the pair of keys is used (in combination with a password group). For the rest, a certain confidence is put in the remote computer.

Every user can use the ssh-keygen command to create an individual private key which is stored in the file ~/.ssh directory. The corresponding public key is stored in identity.pub. For authentication, the local computer must transmit the public key to the target computer in the file ~/.ssh/authorized_keys.

If you use this method, the password must be freshly entered for each connection. This is annoying and in the long run relatively dangerous. For this reason, you can start the ssh-agent as the first program after the login (for example, instead of the window manager). This program then becomes the parent process of all further programs and can pass them the authentication via an inherited file descriptor.

For this purpose, you must replace the daemon of the window manager with the program ssh-agent, for example in the file ~/.xsession, passing the names of the programs to be started as parameters. Please note that processes started earlier in the file ~/.xsession have no access to the agent.

The password that belongs to the file ~/.ssh/identity can be entered by the program ssh-add; its management is then taken over by the ssh-agent tool. You can add or delete identities, or remove all existing ones from memory if you have to leave your office for a long period of time.

Practically all programs you can use in combination with rsh can also be employed with the ssh. Individual adaptations exist for rdist, which uses the