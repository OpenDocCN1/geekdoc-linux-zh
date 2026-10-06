/etc/cron.daily/slocate.cron recreates the database every night so that a Simple search frequently does not find files that were created during the day, since the last run of-updateddb. If updatedb is not run regularly, Simple search will not work properly.

# Advanced Search

A minimal Advanced Search command requires the name of a directory that you want to start the search from (the root of the search) and a filename to search for. Figure 7-14 shows the Start in text box as /usr/; the Advanced Search tool enters your home directory in this location by default. Change the Start in folder as you like, and enter a filename in the Finds file named text box (you can use wildcard characters). You can click Find at this point, and the results of your search will be appended to any existing Search Results window, which opens-automatically if it is not already open.

You can add search criteria to a basic search by clicking the pop-up menu at Add Rule, selecting a criterion, and clicking Add. A new criterion line appears. Fill in text boxes on the new criterion line as appropriate (just you entered the name of the file to search for in the File name text box), and, necessary, enable the check box so that a check mark appears. Turn off a criterion line by removing the Enable check mark; remove a criterion by clicking the associated Remove button. Each of the criteria you specify is ANDed with the next so that a file must meet criteria to appear in the Search Results window. Refer to find on page 1165 for more information on search criteria and how find works.

![](bbox=[0.293, 0.555, 0.807, 0.873])

Figure 7-15 Font Preferences window