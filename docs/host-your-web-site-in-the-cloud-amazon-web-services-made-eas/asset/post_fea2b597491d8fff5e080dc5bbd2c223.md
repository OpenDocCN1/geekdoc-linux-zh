
Server version: 5.1.45-log MySQL Community Server (GPL)

Type 'help;' or '\h' for help. Type '\c' to clear the buffer.

mysql>

Congratulations, you did it! You've launched a DB Instance and connected to it. Now you can verify that RDS created an empty database for you:

```
mysql>show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| innodb             |
| mydata             |
| mysql              |
+--------------------+
4 rows in set (0.00 sec)

mysql>use mydata;
Database changed
mysql>show tables;
Empty set (0.00 sec)
```

## Import Some Data

The next step is to populate the database with some data. I happened to have a file with the URLs of about 200,000 RSS feeds handy, so I used that. First, I created a table for the data:

```
mysql>create table feeds (feedid int(11), url varchar(255));
Query OK, 0 rows affected (0.08 sec)
```

Then I imported the data into the DB Instance:

```
mysql>load data local infile "feeds.txt" into table feeds fields
   ->terminated by "," enclosed by '"';
Query OK, 215825 rows affected (4.53 sec)
Records: 215825  Deleted: 0  Skipped: 0  Warnings: 0
```

And verified that it was present:

```
mysql>select * from feeds order by rand() limit 10;
+------+-----+
| feedid | url |
+------+-----+
| 333143 | http://www.livejournal.com/users/so_delicate/data/atom/ |
| 166339 | http://www.vivat.be/rss_n1.asp?section=7 |
| 422894 | http://sociable.blogspot.com/atom.xml |
| 276630 | http://www.livejournal.com/users/faizmagic/data/atom/ |
| 530872 | http://blogs.guardian.co.uk/games/index.xml |
| 423608 | http://rss-lebanon.com/blogs/xmlsrv/rss2.php?blog=2 |
| 547146 | http://fabooffer.com/articles/dwi-law/rss.xml |
| 213177 | http://randomnumbers.us/wp-rss2.php |
| 500848 | http://feeds.healthvowomen.org/rwahr_c_newshcp |
| 347547 | http://www.livejournal.com/users/_clearblur_/data/atom/ |
+------+-----+
10 rows in set (1.08 sec)
```

You probably have some interesting data of your own, so feel free to use it for this step.

## Administering RDS

Now that you know how to interact with your DB Instance, let's have a quick look at the various ways in which you can administer your instances.

### Monitor Instance Performance

Head back over to the console and click on the instance. Then head towards the bottom of the page and click on the **Monitoring** tab. Figure 9.10 shows what my screen looked like.

DB Instance: mydb

- Description
- **Monitoring**
- Recent Events

Graphs are for 1 DB instance that is available. Times are displayed in UTC.

Time Range: Last Hour ▼ Refresh

![](img/4a5ba0dd041e08e6a67fa31d52309995_305_0.png)

You can see that I loaded enough data to move the line on the graph labeled **Avg Free Storage**. The other graphs show momentary blips which correspond to the increased system load or network traffic related to the data that I loaded and then queried.

### Initiate a Snapshot Backup

Let's make a snapshot backup before moving forward. Right-click on the DB Instance and choose **Take Snapshot**, as Figure 9.11 shows.

![](img/4a5ba0dd041e08e6a67fa31d52309995_306_0.png)

Figure 9.11. Taking a snapshot backup

Enter a name for the DB Snapshot and press the **Yes, Take Snapshot** button.

The console will automatically switch to the **DB Snapshots** page and your new snapshot should be present, with a status of *creating*. The status will change to *available* after a few minutes.

The snapshots always reflect the state of the database at the time the snapshot was started. There’s no need to flush data to disk or to suspend the application. You can click on the **Recent Events** tab in the lower half of the console to see the events generated when the snapshot was taken, as shown in Figure 9.12.

![](img/4a5ba0dd041e08e6a67fa31d52309995_306_1.png)

Figure 9.12. Recent events pertaining to our snapshot

### Scale-up Processing

Let’s pretend that you’ve used this DB Instance for testing, and you’re now ready to move it into production. You’re really happy with the system and expect to see a veritable flood of users on the first day. Because you’ll be drinking champagne and eating cake while this is happening, you decide to scale up the processing power in advance of the flood. Right-click the DB Instance and select the **Modify** option; you'll be led to the screen shown in Figure 9.13.

![](img/4a5ba0dd041e08e6a67fa31d52309995_307_0.png)

Figure 9.13. Scaling up a DB Instance

Select the new DB Instance Class and check **Apply Immediately**, then press the **OK** button. The state of the DB Instance will change to **modifying**, and a new entry will appear in the **Recent Events** tab to indicate that the Instance Class is being modified. Once the modification is complete, the state will be **available** and a corresponding event will appear. As you can see from my event log—shown in Figure 9.14—the entire scaling operation took just six minutes.

![](img/4a5ba0dd041e08e6a67fa31d52309995_308_0.png)

If you receive less traffic than you expected, you can scale down to a smaller and less expensive DB Instance type in the same way.

You can increase the amount of storage allocated to the instance using the same **Modify** operation, but you can never decrease it.

### Scale-up Storage

After you return from your champagne and cake, you check your RDS monitoring and see that your free storage is now down to less than 1GB. Time to add more! Right-click the DB Instance and choose **Modify**. This time, change the **Allocated Storage** to a larger value, as shown in Figure 9.15. Remember to check **Apply Immediately**.

![](img/4a5ba0dd041e08e6a67fa31d52309995_308_1.png)

Your instance will remain operational and accessible while Amazon RDS adds more storage, so you can do this at any time. Again, use the **Recent Events** tab to check on the progress of the modification. My event log showed that increasing allocated storage from 5GB to 8GB took less than five minutes. The increased storage allocation is visible in the Monitoring tab, as you can see in Figure 9.16.

![](img/4a5ba0dd041e08e6a67fa31d52309995_309_0.png)

### Create a DB Instance from a DB Snapshot or to a Point in Time

The AWS Management Console also allows you to create a DB Instance from any of your DB Snapshots or to the exact state in which it was at any point in time within the backup retention period. You can initiate these operations from the **DB Snapshots** and **DB Instances** pages, respectively.

### Convert to Multi-AZ

You can convert your Single-AZ DB Instance to a Multi-AZ DB Instance (and vice versa) at any time. You can initiate this process from the console by invoking the **Modify** operation and changing the value of the **Multi-AZ Deployment** setting, as shown in Figure 9.17.

![](img/4a5ba0dd041e08e6a67fa31d52309995_309_1.png)

The conversion from Single-AZ to Multi-AZ took just seven minutes for my sample instance with 8GB of allocated storage. The state of the DB Instance will transition from **available** to **modifying** (and back) during the modification process, but the DB Instance remains online.

### Delete DB Instances

The final step in the life cycle of a DB Instance is deletion. Amazon RDS allows you to take a final snapshot of your instance so that you can capture its state just before you terminate it, as Figure 9.18 shows.

![](img/4a5ba0dd041e08e6a67fa31d52309995_310_0.png)

The state of the DB Instance will transition from **available** to **deleting** before the instance disappears entirely.

### And That’s a Wrap

At this point you should know enough about Amazon RDS to start migrating your existing MySQL-powered application. You can export the data from your existing database and then import it into a new DB Instance using the information in the section called “Access the DB Instance” and the section called “Import Some Data”.

You’ll need to alter your existing code to use the new connection string, and you’ll have to set up your DB Security Group to allow network access from your application layer.
