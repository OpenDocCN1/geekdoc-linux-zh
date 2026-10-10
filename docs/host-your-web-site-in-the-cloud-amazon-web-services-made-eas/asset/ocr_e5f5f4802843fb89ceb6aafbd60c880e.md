![](bbox=[0.38, 0.06, 0.88, 0.44])

Figure 9.11. Taking a snapshot backup

Enter a name for the DB Snapshot and press the **Yes, Take Snapshot** button.

The console will automatically switch to the **DB Snapshots** page and your new snapshot should be present, with a status of *creating*. The status will change to *available* after a few minutes.

The snapshots always reflect the state of the database at the time the snapshot was started. There’s no need to flush data to disk or to suspend the application. You can click on the **Recent Events** tab in the lower half of the console to see the events generated when the snapshot was taken, as shown in Figure 9.12.

![](bbox=[0.12, 0.75, 0.85, 0.86])

Figure 9.12. Recent events pertaining to our snapshot

# # Scale-up Processing

Let’s pretend that you’ve used this DB Instance for testing, and you’re now ready to move it into production. You’re really happy with the system and expect to see a veritable flood of users on the first day. Because you’ll be drinking champagne and eating cake while this is happening, you decide to scale up the processing