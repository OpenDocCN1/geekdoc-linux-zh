# # File Security

Security begins at the file permission level and should be carried out carefully. Whether you want to protect a file from snooping by an unauthorized invader or another user, you should carefully set your umask (file creation mask) to set your files for maximum security.

Of course, this is really only important if you have more than one user on the system or have to consider hiding information from certain users. However, if you are on a system with several users, consider forcing umask settings for everyone and set read-and-write permissions only for the user, and no permissions for everyone else. This is as good as you can get with file security.

For very sensitive files (such as accounting or employee information), consider encrypting them with a simple utility. There are many such programs available. Most require only a password to trigger the encryption or decryption.

# # Modem Access

For most Linux users, protecting your system from access through an Internet gateway isn’t important because few users have an Internet access machine directly connected to their Linux box. Instead, the concern should be about protecting yourself from break-in through the most accessible method open to system invaders: modems.

Modems are the most commonly used interface into every Linux system (unless you’re running completely standalone or on a closed network). Modems are used for remote user access, as well as for network and Internet access. Securing your system’s modem lines from intrusion is simple and effective enough to stop casual browsers.

# ## Callback Modems

The safest technique to prevent unauthorized access through modems is to employ a call-back modem. A callback modem lets users connect to the system as usual; it then hangs up and consults a list of valid users and their telephone numbers, before calling the user back to establish the call. Callback modems are quite expensive, so this is not a practical solution for many systems.

Callback modems have some problems, too, especially if users change locations frequently. Also, callback modems are vulnerable to abuse because of call-forwarding features of modern telephone switches.