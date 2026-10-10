SSH_HOME/.ssh/known_hosts file, and refuses to connect hosts whose host key has changed. This provides maximum protection against trojan horse attacks. However, it can be somewhat annoying if you don't have good /etc/ssh_known_hosts files installed and frequently connect new hosts. Basically this option forces the user to manually add any new hosts. Normally this option is disabled, and new hosts will automatically be added to the known hosts files. The host keys of known hosts will be verified automatically in either case. The argument must be "yes" or "no".

**User**     Specifies the user to log in as. This can be useful if you have a different user name in different machines. This saves the trouble of having to remember to give the user name on the command line.

**UserKnownHostsFile**     Specifies a file to use instead of SSH_HOME/.ssh/known_hosts.

**UseRsh**     Specifies that login/rsh should be used for this host. It is possible that the host does not at all support the ssh protocol. This causes ssh to immediately exec rsh. All other options (except HostName) are ignored if it has been specified. The argument must be "yes" or "no".

# # ENVIRONMENT

ssh will normally set the following environment variables:

+   *   **DISPLAY**     The DISPLAY variable indicates the location of the X11 server. It is automatically set by ssh to point to a value of the form "hostname:n" where hostname indicates the host where the shell runs, and n is an integer >= 1. Ssh uses this special value to forward X11 connections over the secure channel. The user should normally not set DISPLAY explicitly, as that will render the X11 connection insecure (and will require the user to manually copy any required authorization cookies).

+   *   **HOME**     Set to the path of the user's home directory.

+   *   **LOGNAME**     Synonym for USER; set for compatibility with systems that use this variable.

+   *   **MAIL**     Set to point to the user's mailbox.