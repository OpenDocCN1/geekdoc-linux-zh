# TIPS

Does a push or pull replication trigger interrupt the WINS server(s) operations?

+   No. Replication occurs in the background and the process does not hinder the work of the WINS servers. You may see a performance decrease among the servers during the process, but they are still operational. If you need to use a push or pull replication trigger, you should wait until nonpeak network hours, which are typically early in the morning or late in the evening when network traffic and server requests are low.

Can I save the backup file in any location on your volume?

+   Yes, you can browse to any location on your volume to save the WINS backup file. If you do not store the backup file in the default location, you should keep records so that you know exactly where the WINS database file, along with other database files, is stored. Many administrators choose to store backup files on other hard drives or even removable media.

![](bbox=[0.01, 0.46, 0.48, 0.81])

![](bbox=[0.51, 0.46, 0.98, 0.81])

# BACKING UP THE DATABASE

+   To back up the database, choose Action®Back Up Database.

Browse to the backup folder you want to use.

Click OK.





11