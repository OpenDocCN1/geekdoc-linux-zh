All Session Options directly correlate to settings that will be used only when connecting to the appropriate SSH server. The description and usage of the settings are provided in Table 3.15.

# Table 3.15 Session Options Settings and Descriptions

| SECTION | USAGE AND DESCRIPTION |
| :--- | :--- |
| Connection | Connection-specific information can be configured under this section. |
| | *Logon Scripts* |
| | - Automate Logon: Creates a script to automate the login process to an SSH server. |
| | - Logon Scripts: Allows the Secure CRT client to run automatic scripts to be used when logging on to a remote SSH server. |
| | *SSH2* |
| | - Use Compression: Enables compression on the connection. |
| | - Cipher: Encryption algorithm to be used for the connection. |
| | - MAC: Sets the type of hashes to be used when hashing the data being sent across the network. |
| | - SSH Server: Sets the type of SSH server being used on the remote server. Options are: Auto Detect, which is the best option; DataFellows, SSH Communications, and Standard. |
| | *Port Forwarding* |
| | - Locally sets outgoing tunnels for the session (discussed more in Chapters 6 and 7). |
| | - Remote: Set Incoming tunnels for the session (discussed more in Chapters 6 and 7). |
| | *X11* |
| | Allows the ability to secure X11 connections via the SSH connection by tunneling the X11 packets inside SSH |
| Emulation | Sets options and properties for emulated terminals with Secure CRT. |
| Appearance | Sets cosmetic appearances for the session. |
| Options | Sets keyboard options for the session. |
| File Transfer | Allows the specific location to be set for the Upload and Download of file with the Xmodem and Zmodem utilities. |
| | - Xmodem: File transfer utility that supports error detection during transfer. Note: Xmodem functionality is required on the remote server. |
| | - Zmodem: File transfer utility to download and upload files. Note: Zmodem functionality is required on the remote server. |