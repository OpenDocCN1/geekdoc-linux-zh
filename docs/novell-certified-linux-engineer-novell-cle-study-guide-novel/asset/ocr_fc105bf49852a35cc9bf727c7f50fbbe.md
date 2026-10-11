Using these levels, you can configure the following iFolder policies in the Global Client Policies screen:

+   ▶ **Encryption**—Enabling this policy encrypts user files stored on the iFolder server using the pass phrase.

+   ▶ **Save Password**—Enabling this policy allows the user to save his or her password in the iFolder client.

+   ▶ **Save Pass Phrase**—Enabling this policy allows the user to save his or her pass phrase in the iFolder client.

+   ▶ **Recover Pass Phrase**—Enabling this policy allows the network administrator to recover a user's lost pass phrase. You should use this policy with caution. Because the pass phrase is used as the key to encrypt files, allowing the administrator to see a user's pass phrase also gives him or her the ability to decrypt the user's files on the iFolder server.

+   ▶ **Automatic Sync**—Enabling this policy will cause iFolder clients to automatically synchronize changes with the iFolder server. If this policy is disabled, users must manually synchronize their iFolder clients with the iFolder server.

+   ▶ **Sync to Server Delay**—If the Automatic Sync policy is enabled, this policy configures the amount of time, in seconds, after which a change that's made to a file in the iFolder directory is synchronized to the iFolder server.

+   ▶ **Sync from Server Interval**—If the Automatic Sync policy is enabled, this policy specifies the interval in seconds that the iFolder client waits between queries to the iFolder server to download updated files.

+   ▶ **Conflict Bin Space**—This policy specifies the amount of space to be reserved for Conflict Bin files for each iFolder user. By default, the space allocated is 25MB. If users primarily work with word processing documents, this allocation should be sufficient. If your users work with graphic, video, or audio files, you should consider increasing the amount of space allocated to the Conflict Bin.

+   ▶ **iFolder Location**—This policy specifies the default location for the iFolder directory on the users' workstations.

> **WARNING**
> It's important that you understand that the policies marked with an asterisk in Figure 8.12 are not dynamic. They are applied only when the iFolder user account is first created. If you change one of these policies after user accounts have been created, you must delete the user accounts and re-create them in order for the change to be applied.