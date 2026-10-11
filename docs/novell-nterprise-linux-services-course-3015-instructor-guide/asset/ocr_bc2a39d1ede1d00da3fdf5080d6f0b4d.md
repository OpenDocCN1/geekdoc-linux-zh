To recover a user’s pass phrase, do the following:

+   1. In the iFolder Management console, select **User Management**.
+   2. Search for the appropriate user; then select *username*.
+   3. Scroll down to the bottom of the list; then select **Recover**.
+   4. Enter your security pass phrase; then select **OK**.
+   5. When the pass phrase appears, let the user know what it is.

# ## Change a User Pass Phrase

When users install the iFolder client the first time, they are asked to authenticate to the iFolder server. They are then asked if they would like to encrypt their data.

If they choose to encrypt their data, iFolder then prompts for a pass phrase. This pass phrase becomes a part of the key that is used to encrypt the data when it is transmitted to the iFolder server.

If a user wants to change a pass phrase because he or she has forgotten the pass phrase, you can recover the pass phrase using the iFolder Management console.

However, if the user wants to change to a new pass phrase (for security reasons) and the user does not have the data locally, make sure the user understands that the only way to change the pass phrase is to delete the data from the iFolder server and have the iFolder client encrypt the data and send it up to the server again.

> If the user does not have the data stored locally, have the user synchronize the data to the local hard drive; then proceed with the process to change the pass phrase.