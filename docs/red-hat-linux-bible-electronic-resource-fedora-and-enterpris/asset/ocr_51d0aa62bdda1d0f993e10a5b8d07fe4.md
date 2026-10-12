remotely. it would use the remote CPU and when you save a file, it is saved to the remote file system.

CAUTION: Don't forget when a remote shell or file editor is open on your desktop. Sometimes people forget that a window is remote and will edit some important configuration file on the remote system by mistake (such as the /etc/fstab file). You could damage the remote system with this type of mistake.

# Securing remote X applications

There are several different traditional methods available to prevent just any X application from appearing on your display. Each method offers a different level of security, as well as different amounts of setup. The major security methods that are supported include:

+   - Host Access — This method, described earlier as a default method, lets you decide which host computers can have access to your computer's X display. Use the xhost command to indicate those computers that are allowed access (xhost +hostname) and those that are not (xhost -hostname). If you allow a host access, any user from that computer is allowed access. This security method works best with small networks and single-user computers owned by people you trust.
+   - Magic Cookie — This method, referred to as the MIT-MAGIC-COOKIE-1 method, lets you grant an individual user remote access to your display. The remote client must present a valid cookie before it can access your display.

The steps go something like this: You generate a magic cookie (using the mcookie command); you refer to the cookie when you start your X server (usually from a copy of the cookie in your $HOME/.Xauthority file); you distribute this cookie to remote computers that want to show X clients on your display; and the remote client refers to this cookie when it starts.

There are other X security methods that are also based on storing one or more randomly generated keys in the .Xauthority file. XDM-AUTHORIZATION-1 uses a two-part key — a DES encryption key (56-bit) and some random data (64-bit) — to enable access. When a system supports secure RPC, the SUN-DES-1 method can be used to enable access by setting up public and private key pairs that can be validated on a per user basis. Finally, the MIT-KERBEROS-5 method enables both the X client and X server to validate each other (using a Kerberos trusted third party).

CROSS-REFERENCE: For more information about Kerberos, visit the Kerberos home page at web.mit.edu/kerberos/www/.

# Using SSH to run remote X applications

Not only does the ssh command provide a secure mechanism for logging in to a remote system, it also provides a way of securely running remote X applications. After you log in to