+   Tools
+   The tools page provides a few extra GroundWork tools. Here you can export your settings to a file and also delete groups of hosts or services based on a pattern.

+   Performance
+   On the performance page you can configure options for graphs and other metrics.

# Commit Changes to Nagios

Since GroundWork maintains its settings in a separate database, changes you make in the Web interface don’t directly load into Nagios. Whenever you make a change in the Web interface, you must commit it. The commit process translates GroundWork’s configuration into valid Nagios files. To commit your changes, select Configuration from the main tab, then select the Control tab at the top of the page. From there select the Commit link in the left pane. You will have the option to back up your old configuration if you want; otherwise click the Commit button to update the Nagios config and restart Nagios.

# Configure Contact List

After you set up your initial set of hosts, you will want to configure a contact to get the alerts. Select the Configuration tab, and then select the Contacts tab. Click the Contacts link in the left pane to expand it and reveal the New, Copy, and Modify options. Since we want to add a new contact, click New. Figure 8-5 gives an example of a contact entry. Fill out your contact’s information and either set the notification period and other options manually or select a contact template from the drop-down menu that suits you. If none of the available options does suit you, you can also add a new contact template from the left pane with the settings you want to use. I chose generic-contact-2 because it has a good set of defaults for 24x7 monitoring.

GroundWork will set up a default contact group called nagiosadmin. The default templates that are already set up with GroundWork will use this contact group for notifications, so if you don’t want to do much tweaking,