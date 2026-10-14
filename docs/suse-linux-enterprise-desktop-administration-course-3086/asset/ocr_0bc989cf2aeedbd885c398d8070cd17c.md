+   - The first time you start Novell iFolder under your current local login identity, Novell iFolder prompts you to set up a Novell iFolder account. To go directly to the Novell iFolder Account Assistant, select Yes.
+   - Right-click the Novell iFolder Services icon in the Notification area, open the Novell iFolder Preferences dialog box on the Accounts tab by selecting Account Settings, and then open the Novell iFolder Account Assistant by selecting Add.

2. Follow the on-screen instructions to specify the values shown in Table 13-2.

| Parameters | Description |
|---|---|
| Novell iFolder Server Address | The DNS name or IP address of the Novell iFolder enterprise server where you have an account. Get this information from your Novell iFolder administrator. For example: `svr21.example.com` or `192.168.1.1` |
| Make This My Default Server | Select this option to set the current server as your default server. This will allow the Novell iFolder to select this server automatically when adding new folders. |
| Username | Specify your user identity for this account. Your Novell iFolder administrator decides whether the format you should use is your network user ID (LDAP common name) or your e-mail address. For example, if your name is John Smith with a user ID of `j.smith` and an e-mail address of `john.smith@example.com`, your administrator configures a setting for the server that determines which of the two formats to accept in the User Name field for authentication purposes. |
| Password | Specify the password for your username. |
| Remember My Password | Select Remember My Password to log in automatically to this iFolder account whenever you log in to your computer. If your network password changes, automatic authentication fails gracefully the next time Novell iFolder attempts to log in to the Novell iFolder account. Novell iFolder prompts you to log in with your new password and allows you to specify and save the new password. |
| Account Is Default | When you have multiple accounts, select Account Is Default to make this account the one selected by default in the drop-down list of accounts when you create and upload Novell iFolders. |

Table 13-2

3. If your administrator has set your encryption policy to on or enforced, Novell iFolder will prompt you to enter your passphrase and select the Passphrase recovery agent. The dialog shown in Figure 13-35 appears.