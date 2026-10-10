+   c.  Port: port number, typically 22
+   
+   d.  Username: Username of the remote SSH server
+   
+   e.  Authentication
+       ■ Primary: PublicKey
+           ■ Properties: Use your identity file: c:\Documents and Settings\<username>\Application Data\VanDyke\CRT\publickey.pub
+       ■ Secondary: Password
+   4.  Select Connect.
+   5.  You should now be logged in to a SSsh Communications’ SSH server using a SSH2 key generated from SecureCRT.

While the use of public keys for authentication purposes is by far the better solution of password authentication, the process of making SSH client keys interoperate with various SSH servers may not be an easy process in an enterprise environment. For optimal usage, it is better to use tools and utilities that are interoperable with various platforms and technologies, and SSH is no different.  The use of VShell SSH servers has a significant advantage, since it accepts both OpenSSH keys and SSH2 keys without any need for any conversion from any client mentioned in this chapter. Similarly, using OpenSSH keys as your primary key may be a good solution, since both OpenSSH and VShell servers accept the OpenSSH format, leaving only one conversion required to work with SSH2 servers. Nevertheless, the choice of the SSH client-key format and SSH servers will depend on many items, not just the public-key conversation process. As best practice, it is a good idea to have both formats of your public key made: one for OpenSSH and another for SSH2 formats.

# ### SSH Agents

The SSH agent is a simple utility that allows end-users to handle passphrases attached to public-key files in a simpler way. If multiple passphrases are being used with multiple public keys, it may be cumbersome for the end-user to type and retype all the passphrases several times. The SSH agent utility remembers your passphrases for you after the first time you have authenticated with the passphrase. It is a utility that remembers your private keys and provides the authentication portion to other SSH connections. Therefore, after you initially authenticate with your passphrase, the SSH agent will prevent subsequent SSH sessions from asking you for your passphrase. The process to enable SSH agents involves the following four steps: