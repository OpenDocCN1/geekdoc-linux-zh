Example:

![](bbox=[0.53, 0.11, 0.68, 0.2])

*Figure 14-18: Tripwire detects intrusion by comparing the content of a file and monitoring its attributes.*

# The Tripwire Database

The *Tripwire database* contains baselines, which are the snapshots of files and directories noted at a specific time. When usage becomes abnormal, problems can be easily detected by comparing the latest files and directories with the earlier snapshots. After a Tripwire is installed and configured, the database should be initialized. To initialize the Tripwire database, execute the following command: `/usr/sbin/tripwire --init`. While initializing the database, Tripwire creates a collection of filesystem objects based on certain specifications mentioned in the policy file. An integrity check should be done after initializing the database. To view the entire database, enter the command `/usr/sbin/twprint -md` 
`--print-dbfile | less`.

# The tw.cfg File

The tw.cfg file is the Tripwire configuration file. Before generating the tw.cfg file, you can modify the configuration options in the tw.cfg.txt file to suit your requirements. The following table lists some of the configuration options.

| Use This Option | To Do This |
| :--- | :--- |
| POLFILE | Modify the location of the policy file, tw.pol. |
| DBFILE | Modify the location of the database file, [hostname].twd. |
| REPORTFILE | Modify the location of the report file, [hostname].[date].twr. |
| SITEKEYFILE | Modify the location of the site key file. |
| LOCALKEYFILE | Modify the location of the local key file. |
| EDITOR | Specify the editor called by Tripwire when the database is updated. |
| MAILPROGRAM | Specify the mail program used by Tripwire. |
| MAILMETHOD | Specify the mail protocol used by Tripwire. |

You cannot create the tw.cfg file if the Tripwire file locations are not properly specified in the tw.cfg.txt file.