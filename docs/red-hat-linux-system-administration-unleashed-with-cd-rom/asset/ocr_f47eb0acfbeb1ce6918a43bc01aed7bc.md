# Incremental Backups On the Same Tape as Full Backups

Never, never store incremental backups on the same tape as the full! Bad idea. One small defect or minor accident with the tape and it can be rendered entirely useless.

After the end of the first week, new media (we'll call them set-2) are introduced and the backup process is repeated. The third week, set-2 is replaced with set-3. Then, set-4 makes an appearance. You now have four complete sets of backups that cover the entire previous month. Every single file that was present on the system when the backups were done is right there, ready to be restored if needed. Some files are present only on the four full backups. Other files appear only once on one of the various incremental tapes.

# Deciding On Set Capacity

You keep adding sets until you have enough. How many are enough? It depends on how much archival capacity you want to have. There's no such thing as too much if you can afford the costs of the media. Another factor to consider is the life expectancy of your data. From how far back in time are files going to be needed? Will anyone ever need last month's version of a particular file? Or the version of a file that changes daily as it existed last Tuesday? Or would last week's Sunday version be better? The number of sets (also known as the pool) will determine how far back in time your data can be retrieved.

Whenever you get to the point where you have a large enough archive saved, the original set-1 re-enters the writing process, and this cycle is then repeated for as many times as writing to any given tape is safe. When you decide that set-1 has reached its maximum number of writes limit, the retired set-1 then goes into the archives. If you need to maintain a complete, permanent archival copy, then no tape is ever recycled. Used tapes, after they are verified, of course, get moved to the archives when the cycle reaches them.

```
Sample WorkStation Backup Medium Rotation Schedule
Sun Tue Wed Thu Fri Sat
week 1 set-1 full incr incr incr incr incr
week 2 set-2 full incr incr incr incr incr
week 3 set-3 full incr incr incr incr incr
week 4 set-4 full incr incr incr incr incr
: : : : : : :
week X set-1 full incr incr incr incr incr
```

This strategy will give you a minimum of the past X weeks' (less one day) worth of files, depending on how many media (tapes) there are in your pool. The last three groups of media are often referred to as the Son (last version), Father (previous version to the Son), and Grandfather (previous version to the Father). If each day uses a separate medium, even with recycling at the start of week 5, you would be keeping almost an entire month's data