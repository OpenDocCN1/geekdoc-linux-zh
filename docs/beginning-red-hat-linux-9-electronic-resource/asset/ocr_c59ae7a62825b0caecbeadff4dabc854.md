![](bbox=[0.21, 0.08, 0.81, 0.56])

Here, we've set the **read only** field to No to make it a writeable share; the **browseable** field to Yes, to allow the contents of the `/share` directory to be visible; and the **available** field to Yes, to "enable" the share (that is, make it available to users). We've also added a comment to remind us what the share is for.

When you're done, click on the **Commit Changes** button to commit these settings to the Samba configuration file.

> If you like, you can click on the **Advanced View** button in the *SHARES* screen to set further settings (for example, you can insert a space-delimited list of users into the *valid users* or *invalid users* textboxes, to control which users are allowed or denied access to the Samba share). You can also click the **VIEW** button to view the complete contents of the `/etc/samba/smb. confE` configuration file.

+   5. Restart the Samba service, so that the configuration changes can take effect. To do this, click on **STATUS** button and then click on the **Restart smbd** button to restart the service. Wait for the page to reload, and then click on the **Restart nmbd** button to restart that service too.